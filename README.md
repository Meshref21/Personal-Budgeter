# Personal Budgeter

A full-stack personal finance web application built with Django and Django REST Framework. Track income and expenses, manage budgets, set financial goals, and visualize spending patterns — all in one place.

---

<table>
  <tr>
    <td>
      <img src="PersonalBudgeter/images/Screenshot From 2026-05-24 01-22-22.png" width="100%" style="border-radius:12px;">
    </td>
    <td>
      <img src="PersonalBudgeter/images/Screenshot From 2026-05-24 01-22-48.png" width="100%" style="border-radius:12px;">
    </td>
  </tr>

  <tr>
    <td>
      <img src="PersonalBudgeter/images/Screenshot From 2026-05-24 01-23-25.png" width="100%" style="border-radius:12px;">
    </td>
    <td>
      <img src="PersonalBudgeter/images/Screenshot From 2026-05-24 01-31-07.png" width="100%" style="border-radius:12px;">
    </td>
  </tr>
</table>


## Features

- **Authentication** — Register, login, and logout with Django's built-in auth system
- **Transactions** — Add income and expense entries with category, payment method, and description
- **Budget Management** — Create, edit, and delete budgets by category and period (weekly/monthly/yearly)
- **Financial Goals** — Set savings targets with deadlines and track progress visually
- **Reports** — Generate interactive charts (pie, bar, doughnut) filtered by date range and transaction type
- **REST API** — JSON endpoints for transactions, budgets, users, and blog posts via Django REST Framework

---

## Tech Stack

| Layer     | Technology                        |
|-----------|-----------------------------------|
| Backend   | Python 3, Django 5.2              |
| API       | Django REST Framework             |
| Database  | SQLite (development)              |
| Frontend  | Vanilla HTML/CSS/JS (no framework)|
| Auth      | Django built-in authentication    |

---

## Project Structure

```
PersonalBudgeter/
├── MainDjangoProject/        # Project settings, root URLs, WSGI/ASGI
├── API/                      # REST API endpoints and serializers
├── Home/                     # Dashboard view
├── addTransactions/          # Transaction model, views, and templates
├── CreateEditBudget/         # Budget model, CRUD views, and templates
├── createGoals/              # Goal model, CRUD views, and templates
├── viewReport/               # Report page (chart-based)
├── login/                    # Login and logout views
├── registerUser/             # Registration view
├── static/
│   ├── css/style.css         # Global theme (Obsidian Ember)
│   ├── navbar_footer.js      # Shared navbar and footer injector
│   ├── goals.js              # Goal page interactivity
│   └── viewReportFetch.js    # Report chart logic
└── manage.py
```

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Meshref21/Personal-Budgeter.git
cd PersonalBudgeter
```

### 2. Create and activate a virtual environment

```bash
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Apply migrations

```bash
python manage.py migrate
```

### 5. Create a superuser (optional, for admin access)

```bash
python manage.py createsuperuser
```

### 6. Run the development server

```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000/login/` to get started.

---

## API Endpoints

| Method | Endpoint                  | Description                  |
|--------|---------------------------|------------------------------|
| GET/POST | `/api/transaction/`     | List or create transactions  |
| GET/POST | `/api/createeditbudget/`| List or create budgets       |
| GET/POST | `/api/userinformation/` | List registered users        |
| GET/POST | `/api/blogposts/`       | List or create blog posts    |
| GET      | `/api/users/`           | Raw Django user list (JSON)  |

> All transaction endpoints are filtered to the currently authenticated user.

---

## Pages

| URL                | Page              |
|--------------------|-------------------|
| `/login/`          | Sign In           |
| `/register/`       | Create Account    |
| `/home/`           | Dashboard         |
| `/transactions/`   | Transactions      |
| `/create-budget/`  | Budget Manager    |
| `/goals/`          | Financial Goals   |
| `/viewreport/`     | Reports           |
| `/admin/`          | Django Admin      |

---

## Requirements

```
Django
djangorestframework
pillow
requests
environs
```
---

---

### 📄 Software Requirements Specification (SRS)
The SRS document defines the functional and non-functional requirements of the system, including use cases, constraints, and expected behavior.

- File: [SRS](https://docs.google.com/document/d/1NFLOk_AhQ8rIMm4fg24Iorr5v2k80RKpIg6kWsfk26Y)

### 📐 Software Design Specification (SDS)
The SDS document describes the system architecture, components, data flow, and design decisions used to implement the requirements.

- File: [SDS](https://docs.google.com/document/d/1RbGrsFK0z6SSkzjjFF3j0cczkkRGEdBFcEP03kNSBTU)



## Design Diagrams

This project is documented with a full Software Design Specification (SDS) following the C4 model for architecture and UML for class and sequence diagrams.

---

### Architecture — C4 Model

The architecture is broken down across three levels: Context, Container, and Component.

![Architecture Diagrams](https://cdn.discordapp.com/attachments/1455589482689728703/1507870641196634262/collage.png?ex=6a137977&is=6a1227f7&hm=694de346a24636893df843844758325db6acbc6f79a4775740b9818d4ea404cb)

**Context:** The Customer interacts with the Budgeting System, which in turn requests data from an external Bank API.

**Container:** The system is split into a Web Application, a Mobile Application, an API Application, and a SQL Database — all serving the same customer.

**Component:** Inside the API Application, key components include the Sign-in/Sign-up Controller, Security Component, Accounts Summary, and Budgeting Controller.

---

### Class Diagram

The full class diagram covers six domain areas: User Management, Transactions, Budgeting, Goals, Reports, and Notifications. Each area follows the Entity / Control / Boundary (ECB) separation pattern.

<img src="PersonalBudgeter/images/personal budgeting system.svg" alt="Description" width="400">

Key classes and their roles:

| Class | Stereotype | Responsibility |
|---|---|---|
| `User` | Entity | Stores user profile and handles auth logic |
| `AuthController` | Control | Validates credentials, registers users |
| `Transaction` | Entity | Base class for Income and Expense |
| `Budget` | Entity | Tracks spending limits and remaining balance |
| `Goal` | Entity | Savings target with deadline and progress |
| `Report` | Entity | Aggregates and filters transactions |
| `Notification` | Entity | Stores and manages budget alerts |

---

### Sequence Diagram Sample
#### User Story #4 — Create/Edit Budget

<img src="PersonalBudgeter/images/Screenshot From 2026-05-24 02-06-06.png" alt="Description" width="400">

---

### Design Patterns Applied

| Pattern | Where Used | Benefit |
|---|---|---|
| MVC | Entire app (Boundary / Control / Entity) | Separates UI, logic, and data |
| Template Method | `Transaction` → `Income` / `Expense` | Shared structure, specialized details |
| Singleton | `AuthController` | Single login session, prevents conflicts |

---

## Notes

- `DEBUG = True` and a hardcoded `SECRET_KEY` are present in `settings.py` — **do not deploy to production without addressing these.**
- The database is SQLite by default, suitable for development only.
- The `RegisterUser` model is a legacy artifact; actual user authentication uses Django's built-in `User` model.
- Timezone is set to `Africa/Cairo` in `settings.py` — update as needed.

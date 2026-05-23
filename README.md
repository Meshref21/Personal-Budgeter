# 💰 Personal Budgeter

A full-stack personal finance web application built with Django and Django REST Framework. Track income and expenses, manage budgets, set financial goals, and visualize spending patterns — all in one place.

---

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
git clone <your-repo-url>
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

## Notes

- `DEBUG = True` and a hardcoded `SECRET_KEY` are present in `settings.py` — **do not deploy to production without addressing these.**
- The database is SQLite by default, suitable for development only.
- The `RegisterUser` model is a legacy artifact; actual user authentication uses Django's built-in `User` model.
- Timezone is set to `Africa/Cairo` in `settings.py` — update as needed.

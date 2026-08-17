# Bzuayehu Furniture

Bzuayehu Furniture is a digital platform for a furniture business.

The project provides:

- A customer-facing website
- A protected admin area
- A Django REST API
- A PostgreSQL database
- A Telegram bot
- Email and Telegram notifications
- Search-engine-friendly public pages

The system is designed for customers who are looking for household furniture and may not already know about the shop.

---

## 1. Project Goals

The system should help Bzuayehu Furniture:

- Reach more potential customers.
- Make the shop easier to discover through Google and other search engines.
- Let customers browse products without physically visiting the shop first.
- Show product images, prices, availability, colors, materials, dimensions, and customization information.
- Allow customers to place guest orders without registering.
- Support custom furniture requests.
- Give customers phone, email, and Telegram contact options.
- Allow the shop to manage products and customer requests from a protected admin area.
- Provide the same product/order information to both the website and Telegram bot.

---

## 2. Technology Stack

| Area | Technology |
|---|---|
| Backend | Python + Django |
| API | Django REST Framework |
| Database | PostgreSQL |
| Frontend | HTML + CSS + Tailwind CSS + JavaScript |
| Telegram | Python Telegram Bot integration |
| Development environment | Docker + Docker Compose |
| Version control | Git + GitHub |

---

## 3. Architecture

```text
                          BZUAYEHU FURNITURE
                                  |
                 +----------------+----------------+
                 |                                 |
             Website                          Telegram Bot
                 |                                 |
                 +----------------+----------------+
                                  |
                           Django REST API
                                  |
                               Services
                                  |
                            PostgreSQL DB
                                  |
                    +-------------+-------------+
                    |                           |
                 Orders                      Notifications
                                                /                                                  Email   Telegram

Admin
  |
  v
Django Admin / Protected Admin UI
  |
  v
Django
  |
  v
PostgreSQL
```

### Important rule

The website and Telegram bot must use the **same backend and database**.

Do not create one product database for the website and another product database for Telegram.

---

## 4. Main Project Structure

```text
bzuayehu project/
│
├── backend/
│   ├── Dockerfile.dev
│   ├── requirements.txt
│   ├── manage.py
│   ├── config/
│   └── apps/
│
├── frontend/
│   ├── templates/
│   ├── static/
│   └── components/
│
├── telegram_bot/
│
├── docs/
│
├── docker-compose.yml
├── README.md
├── ONBOARDING.md
├── CONTRIBUTING.md
├── CLAUDE.md
├── .env.example
└── .gitignore
```

---

## 5. Documentation Map

Read the documents in this order:

1. `ONBOARDING.md`
2. `CONTRIBUTING.md`
3. `docs/01-local-setup.md`
4. `docs/02-architecture.md`
5. `docs/03-database-design.md`
6. `docs/04-api-specification.md`
7. `docs/05-ui-ux-design.md`
8. `docs/06-seo.md`
9. `docs/07-testing.md`
10. `docs/08-deployment.md`
11. `CLAUDE.md` for AI-assisted development rules

---

## 6. Quick Start

```bash
git clone <repository-url>
cd "bzuayehu project"

cp .env.example .env

docker compose up --build
```

In another terminal:

```bash
docker compose exec backend python manage.py check
docker compose exec backend python manage.py migrate
docker compose exec backend python manage.py createsuperuser
```

Open:

- Website/backend: `http://127.0.0.1:8000/`
- Admin: `http://127.0.0.1:8000/admin/`

---

## 7. Important Development Rule

Do not manually create or change application database tables with ad-hoc SQL during normal development.

Use:

```text
Django model
    ↓
makemigrations
    ↓
migration file
    ↓
migrate
    ↓
PostgreSQL
```

The database design in `docs/03-database-design.md` is the reference before changing models.

---

## 8. Security

Never commit:

- `.env`
- Database passwords
- Production Django secret keys
- Telegram bot tokens
- Email passwords
- Production server credentials

If a secret is exposed, rotate it immediately.

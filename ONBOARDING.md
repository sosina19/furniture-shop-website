# Bzuayehu Furniture — Developer Onboarding

Welcome to the Bzuayehu Furniture project.

This guide is for a developer who has just cloned the repository and needs to get the project running.

You do not need to understand the whole system before starting. Follow the steps in order.

---

# 1. What Are We Building?

Bzuayehu Furniture is a website and Telegram-based customer platform for a furniture shop.

Customers can:

- Discover the shop.
- Browse furniture.
- Browse by category.
- Search and filter products.
- Open product details.
- See prices and availability.
- See standard colors and materials.
- Request custom colors, materials, and dimensions.
- Place an order without creating an account.
- Contact the shop.
- Leave product reviews.

The shop can:

- Manage products.
- Manage categories.
- Manage images.
- Manage standard colors and materials.
- Manage availability.
- Manage orders.
- Manage reviews.
- Manage customer inquiries.
- Manage business/contact information.
- Receive order notifications by email and Telegram.

---

# 2. What You Need on Your Computer

Install:

- Git
- Docker
- Docker Compose
- A code editor such as VS Code

For the Docker development environment, you do **not** need to install PostgreSQL directly on the host.

You also do not need to manually install backend Python packages on the host when using Docker.

---

# 3. Clone the Repository

```bash
git clone <repository-url>
cd "bzuayehu project"
```

Check the project:

```bash
ls
```

Expected main files/folders:

```text
backend/
frontend/
telegram_bot/
docs/
docker-compose.yml
README.md
ONBOARDING.md
CONTRIBUTING.md
CLAUDE.md
.env.example
.gitignore
```

---

# 4. Create Your Local Environment File

The repository contains:

```text
.env.example
```

Create your private local file:

```bash
cp .env.example .env
```

Open it:

```bash
nano .env
```

You can also open it in VS Code.

---

# 5. Configure .env

Example:

```env
POSTGRES_DB=bzuayehu_db
POSTGRES_USER=bzuayehu_user
POSTGRES_PASSWORD=your_local_database_password
POSTGRES_HOST=db
POSTGRES_PORT=5432

DJANGO_SECRET_KEY=your_local_secret_key
DJANGO_DEBUG=True

TELEGRAM_BOT_TOKEN=

EMAIL_HOST=
EMAIL_PORT=587
EMAIL_HOST_USER=
EMAIL_HOST_PASSWORD=
EMAIL_USE_TLS=True
```

## Important

Each developer can have their own `.env`.

Do not ask other developers for your private local secret values.

### PostgreSQL

```env
POSTGRES_DB=bzuayehu_db
```

Database name.

```env
POSTGRES_USER=bzuayehu_user
```

Local Docker PostgreSQL user.

```env
POSTGRES_PASSWORD=...
```

Local Docker PostgreSQL password.

```env
POSTGRES_HOST=db
```

This is important.

`db` is the Docker Compose service name.

Inside Docker:

```text
Django container
      |
      v
     db
      |
      v
PostgreSQL container
```

Do not use `localhost` for the Django-to-PostgreSQL container connection.

```env
POSTGRES_PORT=5432
```

PostgreSQL's internal Docker port.

### Django

```env
DJANGO_SECRET_KEY=...
```

Django's application secret.

For local development, each developer can have a different key.

```env
DJANGO_DEBUG=True
```

Use `True` only for development.

### Telegram

```env
TELEGRAM_BOT_TOKEN=
```

Add the real token only when working on the Telegram integration.

Never commit it.

### Email

Email variables can remain empty until real SMTP/email notification integration is configured.

---

# 6. Start Docker

From the project root:

```bash
docker compose up --build
```

Keep that terminal running.

---

# 7. Open Another Terminal

Go to the project root:

```bash
cd "bzuayehu project"
```

Check the containers:

```bash
docker compose ps
```

You should see services such as:

```text
bzuayehu_backend
bzuayehu_db
```

with a status similar to:

```text
Up
```

---

# 8. Check Django

```bash
docker compose exec backend python manage.py check
```

Expected:

```text
System check identified no issues
```

If there is an error, stop and resolve it before continuing.

---

# 9. Apply Migrations

```bash
docker compose exec backend python manage.py migrate
```

This creates Django's required tables.

Later it will also create the Bzuayehu application tables.

---

# 10. Create an Admin Account

```bash
docker compose exec backend python manage.py createsuperuser
```

The credentials here are for Django Admin.

They are not:

- PostgreSQL credentials
- Docker credentials
- customer credentials

---

# 11. Open the Project

Website/backend development address:

```text
http://127.0.0.1:8000/
```

Admin:

```text
http://127.0.0.1:8000/admin/
```

---

# 12. Understand the Development Containers

The development environment currently uses:

```text
Docker Compose
   |
   +-- db
   |    PostgreSQL
   |
   +-- backend
        Django + DRF
```

The Telegram bot can be added as another service when its implementation starts.

---

# 13. Why requirements.txt Still Exists

Docker removes the need for each developer to manually install Python dependencies on the host, but the backend still needs a dependency list.

`backend/requirements.txt` tells the Docker backend image:

> Install these Python packages.

The Dockerfile performs this:

```dockerfile
COPY requirements.txt .
RUN pip install -r requirements.txt
```

So:

```text
requirements.txt
      ↓
Dockerfile
      ↓
Backend image
      ↓
Backend container
```

---

# 14. Database Development Workflow

Before changing database structure:

1. Read `docs/03-database-design.md`.
2. Update the Django model.
3. Create migrations.
4. Apply migrations.
5. Test.

Commands:

```bash
docker compose exec backend python manage.py makemigrations
docker compose exec backend python manage.py migrate
```

---

# 15. API Development Workflow

Before changing or creating an API endpoint:

1. Read `docs/04-api-specification.md`.
2. Confirm the endpoint purpose.
3. Confirm request data.
4. Confirm response data.
5. Confirm permissions.
6. Implement serializer.
7. Implement view/viewset.
8. Add URL route.
9. Add validation.
10. Add tests.
11. Update API documentation if the contract changed.

---

# 16. Frontend Development Workflow

Frontend uses:

- HTML
- CSS
- Tailwind CSS
- JavaScript

Before major UI work:

Read:

```text
docs/05-ui-ux-design.md
```

Use the API for application data.

---

# 17. Telegram Bot Development Workflow

The Telegram bot must use the Django API.

Correct:

```text
Telegram Bot
      |
      v
Django API
      |
      v
PostgreSQL
```

Do not create a separate product/order database for Telegram.

---

# 18. Notification Workflow

When an order is created:

```text
Customer
   |
   v
Django API
   |
   v
Create Order + OrderItem
   |
   v
Notification Service
   |
   +---- Email
   |
   +---- Telegram
   |
   v
NotificationLog
```

An order must remain saved even if a notification fails.

---

# 19. Useful Commands

### Start

```bash
docker compose up
```

### Build and start

```bash
docker compose up --build
```

### Start in background

```bash
docker compose up -d
```

### Stop

```bash
docker compose down
```

### View containers

```bash
docker compose ps
```

### View backend logs

```bash
docker compose logs backend
```

### View database logs

```bash
docker compose logs db
```

### Enter backend container

```bash
docker compose exec backend bash
```

### Django shell

```bash
docker compose exec backend python manage.py shell
```

### Django check

```bash
docker compose exec backend python manage.py check
```

### Migrations

```bash
docker compose exec backend python manage.py makemigrations
docker compose exec backend python manage.py migrate
```

---

# 20. Reset Local Database

Warning: this deletes the local Docker PostgreSQL volume.

```bash
docker compose down -v
```

Then:

```bash
docker compose up --build
docker compose exec backend python manage.py migrate
```

Only do this when you intentionally want a fresh local database.

---

# 21. Git Rules

Before committing:

```bash
git status
```

Do not commit `.env`.

Check:

```bash
git status --ignored
```

The `.gitignore` should contain `.env`.

---

# 22. First-Day Checklist

- [ ] Install Git
- [ ] Install Docker
- [ ] Clone repository
- [ ] Create `.env`
- [ ] Fill local environment values
- [ ] Run `docker compose up --build`
- [ ] Verify `docker compose ps`
- [ ] Run `manage.py check`
- [ ] Run migrations
- [ ] Create superuser
- [ ] Open the website
- [ ] Open Django Admin
- [ ] Read `docs/01-local-setup.md`
- [ ] Read `docs/02-architecture.md`
- [ ] Read `docs/03-database-design.md`
- [ ] Read `docs/04-api-specification.md`

After this, the developer is ready to pick a feature.

---

# 23. Before Changing Something

Ask:

> Which part of the system am I changing?

| Change | Read first |
|---|---|
| Database/model | `docs/03-database-design.md` |
| API | `docs/04-api-specification.md` |
| Website/UI | `docs/05-ui-ux-design.md` |
| SEO | `docs/06-seo.md` |
| Testing | `docs/07-testing.md` |
| Deployment | `docs/08-deployment.md` |
| Team workflow | `CONTRIBUTING.md` |
| AI-assisted development | `CLAUDE.md` |

---

# 24. Important Principle

Do not guess what a field, endpoint, or workflow is supposed to do.

Check the documentation first.

If the requirements have changed:

1. Update the relevant documentation.
2. Agree on the new design.
3. Update the implementation.
4. Update tests.

This keeps the project and its documentation synchronized.
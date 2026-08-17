# Local Development Setup

## Docker Services

```text
db
  PostgreSQL 16

backend
  Django + Django REST Framework
```

The Telegram bot becomes a separate service when its implementation is added.

## Environment Variables

Required local variables:

```env
POSTGRES_DB=bzuayehu_db
POSTGRES_USER=bzuayehu_user
POSTGRES_PASSWORD=...
POSTGRES_HOST=db
POSTGRES_PORT=5432

DJANGO_SECRET_KEY=...
DJANGO_DEBUG=True
```

Optional integration variables:

```env
TELEGRAM_BOT_TOKEN=

EMAIL_HOST=
EMAIL_PORT=587
EMAIL_HOST_USER=
EMAIL_HOST_PASSWORD=
EMAIL_USE_TLS=True
```

## Start

```bash
docker compose up --build
```

## Verify

```bash
docker compose ps
docker compose exec backend python manage.py check
```

## Migrations

```bash
docker compose exec backend python manage.py migrate
```

## Admin

```bash
docker compose exec backend python manage.py createsuperuser
```

Open `/admin/`.

## Important Docker Detail

Django connects to PostgreSQL using:

```env
POSTGRES_HOST=db
```

because `db` is the Compose service name.

Do not change this to `localhost` for container-to-container communication.

## Host PostgreSQL

A host PostgreSQL installation is not required for the Docker environment.

Avoid exposing PostgreSQL to the host unless there is a specific reason.


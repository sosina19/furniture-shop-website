# Deployment

## Production Components

- Django backend
- PostgreSQL database
- Reverse proxy/web server
- Static/media storage
- Telegram bot
- Domain
- HTTPS
- Secure environment/secret management

## Production Secrets

Never commit:

- production database credentials
- Django production secret key
- Telegram bot token
- email credentials

## Database

Production PostgreSQL should have:

- backups
- restricted access
- strong credentials
- migration procedure

## Deployment Flow

1. Pull reviewed code.
2. Build/update containers.
3. Apply migrations.
4. Collect static files.
5. Restart services.
6. Verify backend.
7. Verify public site.
8. Verify admin.
9. Verify notifications.
10. Verify Telegram integration.

## Rollback

Keep a known-good version available so failed deployments can be rolled back.

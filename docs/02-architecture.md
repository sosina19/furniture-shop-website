# System Architecture

## Main Components

1. Website
2. Django backend/API
3. PostgreSQL
4. Admin
5. Telegram bot
6. Notification services

## Diagram

```text
Customer
   |
   +------ Website ------+
   |                     |
   +------ Telegram -----+
             |
             v
        Django API
             |
       +-----+------+
       |            |
       v            v
  PostgreSQL   Notification Service
                    |
               +----+----+
               |         |
             Email    Telegram
```

## Backend Responsibilities

- Business logic
- Data validation
- Database access
- API
- Authentication/authorization
- Orders
- Reviews
- Inquiries
- Notifications

## Frontend Responsibilities

- Presentation
- Navigation
- Forms
- Product browsing
- Search/filter UI
- Ordering UI
- Reviews UI
- Responsive design

## Admin

Django Admin is the initial management interface.

A custom Tailwind admin UI can be added later if required.

## Shared Data

Website and Telegram bot always use the same backend/database.


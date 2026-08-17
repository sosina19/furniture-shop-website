# AI / Developer Workflow Guidelines

This file contains project-specific guidelines for AI-assisted development and developer assistance.

## 1. Follow the Existing Design

Before changing:

- database models
- API contracts
- authentication
- order workflow
- notifications

read the relevant documentation in `docs/`.

## 2. Do Not Invent Requirements

The implementation should follow the approved project requirements.

If a requirement is not documented, do not silently add a major new feature.

## 3. Database

Use Django models and migrations for application schema changes.

Important business rule:

```text
Product = what the shop normally offers
OrderItem = what the customer actually requested
```

Custom values must remain possible.

## 4. API

Maintain the documented API contract.

Do not change response/request structures without updating:

- implementation
- tests
- API documentation

## 5. Security

Never print or expose:

- database passwords
- Django production secret keys
- Telegram bot tokens
- email passwords

Never put secrets in source code.

## 6. Code Style

Prefer:

- readable Python
- small functions
- explicit naming
- validation
- tests
- comments only where useful

Avoid unnecessary abstractions for simple functionality.

## 7. Before Finishing Work

Run appropriate checks and tests.

Update documentation if behavior changed.

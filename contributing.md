# Contributing to Bzuayehu Furniture

## 1. General Rule

Before changing code, understand the relevant documentation and existing implementation.

Do not introduce a new architecture or dependency without checking whether the project already has a solution.

---

## 2. Branches

Use a feature branch for work.

Example:

```bash
git checkout -b feature/product-management
```

Suggested naming:

```text
feature/...
fix/...
docs/...
refactor/...
test/...
```

---

## 3. Commits

Use clear commit messages.

Good:

```text
feat: add product category model
fix: validate custom order dimensions
docs: update onboarding instructions
test: add order creation tests
```

Avoid vague messages such as:

```text
changes
stuff
update
final
```

---

## 4. Before Opening a Pull Request

Run:

```bash
docker compose exec backend python manage.py check
docker compose exec backend python manage.py test
```

If API/frontend tests exist, run those too.

Review:

```bash
git diff
git status
```

Do not commit:

- `.env`
- secrets
- temporary test data
- debug files
- generated local database files

---

## 5. Database Changes

Any model change should include migrations.

```bash
docker compose exec backend python manage.py makemigrations
docker compose exec backend python manage.py migrate
```

Commit migration files.

Do not edit already-applied migration history just to hide a change.

---

## 6. API Changes

If an endpoint changes:

- Update implementation.
- Update tests.
- Update `docs/04-api-specification.md`.
- Consider frontend and Telegram impact.

---

## 7. Documentation Changes

Documentation is part of the project.

If behavior changes, update the appropriate `.md` file in the same feature work.

# Testing

## Backend

Test:

- models
- validation
- relationships
- API endpoints
- permissions
- order creation
- custom values
- availability
- notification handling

## Database

Verify:

- foreign keys
- unique constraints
- required/optional fields
- delete behavior
- migrations

## Frontend

Test:

- responsive design
- product browsing
- search/filter
- product details
- order forms
- custom options
- validation
- error/loading states

## Telegram

Test:

- `/start`
- categories
- product browsing
- product details
- order flow
- inquiries
- API communication

## Notifications

Test:

- email success
- email failure
- Telegram success
- Telegram failure
- NotificationLog records
- order persistence when a notification fails

## Acceptance Examples

- Customer can browse without registering.
- Product Order Now pre-fills the order form.
- Navigation Order opens an empty form.
- Customer can request a non-standard color.
- Customer can request custom dimensions.
- Product-specific availability time is shown.
- Admin can manage products and orders.
- Orders remain stored even if notification delivery fails.

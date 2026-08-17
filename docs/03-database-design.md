# Database Design

## Current Models

1. User (Django built-in)
2. Category
3. Product
4. ProductImage
5. Color
6. Material
7. ProductColor
8. ProductMaterial
9. Order
10. OrderItem
11. Review
12. Inquiry
13. BusinessSetting
14. NotificationLog

## User

Admin/staff authentication.

Customers do not register in Version 1.

## Category

Fields:

- id
- name
- description
- image
- is_active
- created_at
- updated_at

One Category -> many Products.

## Product

Fields:

- id
- category_id
- name
- description
- price
- availability
- estimated_availability_days
- availability_note
- is_featured
- is_new
- length
- width
- height
- customization_available
- customization_description
- seo_title
- seo_description
- created_at
- updated_at

Availability values:

```text
AVAILABLE
OUT_OF_STOCK
MADE_TO_ORDER
DISCONTINUED
```

## ProductImage

Fields:

- id
- product_id
- image
- alt_text
- is_primary
- display_order
- created_at

## Color

Standard color options.

Fields:

- id
- name
- hex_code
- is_active
- created_at

## Material

Standard materials.

Fields:

- id
- name
- description
- is_active
- created_at

## ProductColor

- product_id
- color_id

Unique pair.

## ProductMaterial

- product_id
- material_id

Unique pair.

## Order

Guest order.

Fields:

- id
- customer_name
- customer_phone
- customer_email
- status
- customer_acknowledged_delay
- customer_note
- created_at
- updated_at

Statuses:

```text
NEW
CONTACTED
CONFIRMED
IN_PRODUCTION
READY
COMPLETED
CANCELLED
```

## OrderItem

Fields:

- id
- order_id
- product_id
- quantity
- color_id
- material_id
- custom_color
- custom_material
- length
- width
- height
- customization_note
- unit_price

Custom values are allowed even if they are not in the standard Color/Material tables.

## Review

Fields:

- id
- product_id
- customer_name
- rating
- comment
- status
- created_at
- updated_at

Statuses:

```text
PENDING
APPROVED
REJECTED
```

## Inquiry

Fields:

- id
- customer_name
- phone
- email
- product_id (optional)
- subject
- message
- status
- created_at

Statuses:

```text
NEW
READ
RESPONDED
CLOSED
```

## BusinessSetting

Stores:

- business_name
- description
- phone
- email
- telegram_username
- address
- google_maps_url
- business_hours
- facebook_url
- instagram_url
- updated_at

## NotificationLog

Fields:

- id
- order_id (optional)
- inquiry_id (optional)
- notification_type
- recipient
- subject
- message_summary
- status
- sent_at
- error_message
- created_at

Types:

```text
EMAIL
TELEGRAM
```

Statuses:

```text
PENDING
SENT
FAILED
```

## Relationships

```text
Category 1 ---- * Product
Product 1 ---- * ProductImage
Product * ---- * Color via ProductColor
Product * ---- * Material via ProductMaterial
Product 1 ---- * Review
Order 1 ---- * OrderItem
OrderItem * ---- 1 Product
Inquiry * ---- 0..1 Product
Order/Inquiry 1 ---- * NotificationLog
```

## Core Principle

`Product` describes the normal catalog item.

`OrderItem` stores the exact customer request.

That is why custom color/material/dimensions belong in OrderItem.

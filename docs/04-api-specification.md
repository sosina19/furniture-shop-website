# API Specification

## Base Prefix

```text
/api/v1/
```

## Products

```text
GET    /api/v1/products/
GET    /api/v1/products/{id}/
POST   /api/v1/products/          admin
PATCH  /api/v1/products/{id}/     admin
DELETE /api/v1/products/{id}/     admin/policy
```

## Categories

```text
GET    /api/v1/categories/
GET    /api/v1/categories/{id}/
POST   /api/v1/categories/       admin
PATCH  /api/v1/categories/{id}/  admin
DELETE /api/v1/categories/{id}/  admin/policy
```

## Colors

```text
GET    /api/v1/colors/
POST   /api/v1/colors/            admin
PATCH  /api/v1/colors/{id}/       admin
DELETE /api/v1/colors/{id}/       admin
```

## Materials

```text
GET    /api/v1/materials/
POST   /api/v1/materials/         admin
PATCH  /api/v1/materials/{id}/    admin
DELETE /api/v1/materials/{id}/    admin
```

## Images

```text
GET    /api/v1/products/{product_id}/images/
POST   /api/v1/products/{product_id}/images/ admin
PATCH  /api/v1/images/{id}/                 admin
DELETE /api/v1/images/{id}/                 admin
```

## Orders

```text
POST   /api/v1/orders/
GET    /api/v1/orders/          admin
GET    /api/v1/orders/{id}/     admin
PATCH  /api/v1/orders/{id}/     admin
```

Guest order creation supports:

- customer name
- phone
- email
- product
- quantity
- standard/custom color
- standard/custom material
- dimensions
- customization note

## Reviews

```text
POST   /api/v1/reviews/
GET    /api/v1/products/{id}/reviews/
GET    /api/v1/reviews/          admin
PATCH  /api/v1/reviews/{id}/    admin
```

## Inquiries

```text
POST   /api/v1/inquiries/
GET    /api/v1/inquiries/        admin
GET    /api/v1/inquiries/{id}/   admin
PATCH  /api/v1/inquiries/{id}/  admin
```

## Business Settings

```text
GET    /api/v1/business-settings/
PATCH  /api/v1/business-settings/ admin
```

## Permissions

### Public

- Read public products/categories
- Read approved reviews
- Create guest orders
- Create reviews
- Create inquiries

### Admin

- Catalog CRUD
- Category/color/material management
- Image management
- Order management
- Review moderation
- Inquiry management
- Business settings

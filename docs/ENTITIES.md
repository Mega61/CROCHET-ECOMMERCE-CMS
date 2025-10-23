# Strapi Entities Documentation

This document describes all the generated Strapi content types for the Crochet Ecommerce CMS.

## Generated Entities

All entities have been successfully generated and built. The following content types are now available in your Strapi admin panel:

### 1. Category (Collection Type)
**Location:** [src/api/category/content-types/category/schema.json](src/api/category/content-types/category/schema.json)

**API Endpoint:** `/api/categories`

**Fields:**
- `name` (String, Required, Unique) - Category name
- `slug` (UID from name, Required) - URL-friendly identifier
- `description` (Text) - Category description
- `image` (Media - Single, Images only) - Category image
- `products` (Relation - One-to-Many) - Products in this category

**Draft & Publish:** Enabled

---

### 2. Tag (Collection Type)
**Location:** [src/api/tag/content-types/tag/schema.json](src/api/tag/content-types/tag/schema.json)

**API Endpoint:** `/api/tags`

**Fields:**
- `name` (String, Required, Unique) - Tag name
- `slug` (UID from name, Required) - URL-friendly identifier
- `products` (Relation - Many-to-Many) - Tagged products

**Draft & Publish:** Enabled

---

### 3. Product (Collection Type)
**Location:** [src/api/product/content-types/product/schema.json](src/api/product/content-types/product/schema.json)

**API Endpoint:** `/api/products`

**Fields:**
- `name` (String, Required) - Product name
- `slug` (UID from name, Required) - URL-friendly identifier
- `description` (Rich Text, Required) - Full product description
- `shortDescription` (Text, Required) - Brief summary for catalog
- `images` (Media - Multiple, Images only) - Product photos
- `featuredImage` (Media - Single, Required, Images only) - Main product image
- `price` (Decimal, Required, Min: 0) - Product price
- `estimatedTimeHours` (Decimal, Required, Min: 0) - Time required to complete
- `difficulty` (Enumeration, Default: Beginner) - Options: Beginner, Intermediate, Advanced
- `materials` (Text) - Materials used
- `dimensions` (String) - Size/dimensions of finished product
- `isAvailable` (Boolean, Default: true) - Whether product is currently available
- `category` (Relation - Many-to-One) - Product category
- `tags` (Relation - Many-to-Many) - Product tags
- `orders` (Relation - One-to-Many) - Associated orders

**Draft & Publish:** Enabled

---

### 4. Time Slot (Collection Type)
**Location:** [src/api/time-slot/content-types/time-slot/schema.json](src/api/time-slot/content-types/time-slot/schema.json)

**API Endpoint:** `/api/time-slots`

**Fields:**
- `weekStartDate` (Date, Required) - Start of the work week
- `weekEndDate` (Date, Required) - End of the work week
- `status` (Enumeration, Required, Default: Available) - Options: Available, Reserved, Completed
- `maxProjects` (Integer, Required, Default: 1, Min: 1) - Maximum projects you can handle that week
- `currentProjects` (Integer, Default: 0, Min: 0) - Current number of reserved projects
- `notes` (Text) - Internal notes about the time slot
- `orders` (Relation - One-to-Many) - Associated orders

**Draft & Publish:** Disabled (operational data)

---

### 5. Customer (Collection Type)
**Location:** [src/api/customer/content-types/customer/schema.json](src/api/customer/content-types/customer/schema.json)

**API Endpoint:** `/api/customers`

**Fields:**
- `name` (String, Required) - Customer name
- `email` (Email, Required, Unique) - Customer email
- `phone` (String) - Customer phone number
- `address` (Text) - Customer address
- `notes` (Text) - Internal notes about customer
- `orders` (Relation - One-to-Many) - Customer's orders

**Draft & Publish:** Disabled (operational data)

---

### 6. Order (Collection Type)
**Location:** [src/api/order/content-types/order/schema.json](src/api/order/content-types/order/schema.json)

**API Endpoint:** `/api/orders`

**Fields:**
- `orderNumber` (String, Required, Unique) - Unique order identifier
- `customerName` (String, Required) - Customer's name
- `customerEmail` (Email, Required) - Customer's email
- `customerPhone` (String) - Customer's phone number
- `deliveryAddress` (Text, Required) - Shipping address
- `customizationNotes` (Rich Text) - Special requests/customizations
- `status` (Enumeration, Required, Default: Pending) - Options: Pending, Confirmed, In Progress, Completed, Cancelled
- `totalPrice` (Decimal, Required, Min: 0) - Total order price
- `submittedAt` (DateTime) - Order submission timestamp
- `completedAt` (DateTime) - Order completion timestamp
- `product` (Relation - Many-to-One) - Ordered product
- `timeSlot` (Relation - Many-to-One) - Reserved time slot
- `customer` (Relation - Many-to-One) - Associated customer

**Draft & Publish:** Disabled (operational data)

---

### 7. Site Settings (Single Type)
**Location:** [src/api/site-setting/content-types/site-setting/schema.json](src/api/site-setting/content-types/site-setting/schema.json)

**API Endpoint:** `/api/site-setting`

**Fields:**
- `siteName` (String, Required, Default: "Crochet Ecommerce") - Website name
- `logo` (Media - Single, Images only) - Site logo
- `masterEmail` (Email, Required) - Email where orders are sent
- `contactEmail` (Email, Required) - Public contact email
- `phone` (String) - Contact phone number
- `aboutText` (Rich Text) - About section content
- `termsAndConditions` (Rich Text) - Terms and conditions
- `shippingPolicy` (Rich Text) - Shipping policy

**Draft & Publish:** Disabled (configuration data)

---

## Entity Relationships

```
Category (1) ──→ (∞) Product
Tag (∞) ←──→ (∞) Product
Product (1) ──→ (∞) Order
TimeSlot (1) ──→ (∞) Order
Customer (1) ──→ (∞) Order
```

---

## Project Structure

```
src/api/
├── category/
│   ├── content-types/category/
│   │   └── schema.json
│   ├── controllers/
│   │   └── category.ts
│   ├── services/
│   │   └── category.ts
│   └── routes/
│       └── category.ts
├── tag/
│   ├── content-types/tag/
│   │   └── schema.json
│   ├── controllers/
│   │   └── tag.ts
│   ├── services/
│   │   └── tag.ts
│   └── routes/
│       └── tag.ts
├── product/
│   ├── content-types/product/
│   │   └── schema.json
│   ├── controllers/
│   │   └── product.ts
│   ├── services/
│   │   └── product.ts
│   └── routes/
│       └── product.ts
├── time-slot/
│   ├── content-types/time-slot/
│   │   └── schema.json
│   ├── controllers/
│   │   └── time-slot.ts
│   ├── services/
│   │   └── time-slot.ts
│   └── routes/
│       └── time-slot.ts
├── customer/
│   ├── content-types/customer/
│   │   └── schema.json
│   ├── controllers/
│   │   └── customer.ts
│   ├── services/
│   │   └── customer.ts
│   └── routes/
│       └── customer.ts
├── order/
│   ├── content-types/order/
│   │   └── schema.json
│   ├── controllers/
│   │   └── order.ts
│   ├── services/
│   │   └── order.ts
│   └── routes/
│       └── order.ts
└── site-setting/
    ├── content-types/site-setting/
    │   └── schema.json
    ├── controllers/
    │   └── site-setting.ts
    ├── services/
    │   └── site-setting.ts
    └── routes/
        └── site-setting.ts
```

---

## Next Steps

### 1. Start the Development Server

```bash
npm run develop
```

This will:
- Start Strapi in development mode
- Create the database tables
- Generate TypeScript types
- Open the admin panel at http://localhost:1337/admin

### 2. Create Your First Admin User

When you first visit the admin panel, you'll be prompted to create an admin account.

### 3. Configure Content Types

All content types are now available in the Content-Type Builder in your admin panel. You can:
- View and modify field configurations
- Add new fields if needed
- Configure API permissions in Settings → Roles → Public

### 4. Configure API Permissions

Go to Settings → Roles → Public and enable the following endpoints for public access:

**For Frontend (Public Role):**
- `category`: find, findOne
- `tag`: find, findOne
- `product`: find, findOne
- `time-slot`: find (to show available slots)
- `order`: create (to allow order submission)
- `site-setting`: find

**For Admin Only:**
- Keep all other endpoints restricted to authenticated users

### 5. Set Up Email Notifications

To receive order notifications:

1. Install an email provider plugin (e.g., @strapi/provider-email-nodemailer)
2. Configure it in `config/plugins.js` or `config/plugins.ts`
3. Create a lifecycle hook in the Order content type to send emails on creation

Example lifecycle hook location: `src/api/order/content-types/order/lifecycles.ts`

### 6. Populate Initial Data

Add your first:
- Categories (e.g., "Amigurumi", "Blankets", "Accessories")
- Tags (e.g., "Baby", "Home Decor", "Gift")
- Products with images and descriptions
- Time Slots for upcoming weeks
- Site Settings (configure your email, about text, etc.)

### 7. Test the API

You can test the API endpoints using:
- Strapi's built-in API documentation at http://localhost:1337/documentation (if you install the documentation plugin)
- Postman or similar tools
- Your frontend application

---

## API Query Examples

### Get All Available Products

```
GET /api/products?filters[isAvailable][$eq]=true&populate=*
```

### Get Product with Category and Tags

```
GET /api/products?filters[slug][$eq]=cute-bunny&populate[category]=*&populate[tags]=*&populate[images]=*&populate[featuredImage]=*
```

### Get Available Time Slots

```
GET /api/time-slots?filters[status][$eq]=Available&filters[currentProjects][$lt]=maxProjects
```

### Create an Order

```
POST /api/orders
Content-Type: application/json

{
  "data": {
    "orderNumber": "ORD-2024-001",
    "customerName": "Jane Doe",
    "customerEmail": "jane@example.com",
    "customerPhone": "555-1234",
    "deliveryAddress": "123 Main St, City, State 12345",
    "customizationNotes": "Please use pink yarn",
    "totalPrice": 45.99,
    "submittedAt": "2024-01-15T10:30:00.000Z",
    "product": 1,
    "timeSlot": 2,
    "customer": 1
  }
}
```

---

## TypeScript Support

After running `npm run develop`, Strapi will generate TypeScript types in:
- `types/generated/contentTypes.d.ts`
- `types/generated/components.d.ts`

These types can be used in your custom controllers, services, and middleware for full type safety.

---

## Troubleshooting

### TypeScript Errors

If you see TypeScript errors about content types not being assignable, this is normal before the first build. The types are generated when Strapi runs for the first time.

### Database Connection Issues

Make sure your database configuration is correct in your `.env` file. For development, Strapi defaults to SQLite which requires no additional configuration.

### Permission Issues

If your frontend can't access certain endpoints, check the API permissions in Settings → Roles → Public.

---

## Additional Resources

- [Strapi Documentation](https://docs.strapi.io)
- [Strapi REST API Documentation](https://docs.strapi.io/dev-docs/api/rest)
- [Strapi Content API](https://docs.strapi.io/dev-docs/api/content-api)
- [Strapi Lifecycle Hooks](https://docs.strapi.io/dev-docs/backend-customization/models#lifecycle-hooks)

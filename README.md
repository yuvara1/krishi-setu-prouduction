# AGRITRADE Project Documentation

## 1. Project Overview

AGRITRADE is a digital marketplace platform connecting farmers and retailers for crop trading. It streamlines bidding, ordering, payments, and notifications, ensuring transparency and efficiency in agricultural commerce.

## 2. Architecture

- **Client:** React (Vite), modern SPA, multi-role dashboards
- **Server:** Spring Boot (Java), REST APIs, PostgreSQL database
- **Database:** PostgreSQL, production-ready schema

### Folder Structure

```
client/
  src/
    pages/
    components/
    hooks/
    layouts/
    services/
    utils/
server/
  agritrade/
    src/main/java/org/agri/agritrade/
      controller/
      dto/
      entity/
      exception/
      mapper/
      repository/
      security/
      service/
      util/
    src/main/resources/
      static/
        schema.sql
        endpoints.txt
      application.properties
```

## 3. Key Features

- User authentication (JWT, roles: Farmer, Retailer, Admin)
- Crop batch management (listing, status, organic, location)
- Bidding system (retailer bids, status tracking)
- Order processing (confirmation, delivery, payment status)
- Payment integration (Razorpay, status tracking)
- Notifications (real-time, read/unread)
- Audit logs for operations
- Admin dashboard for user and order management

## 4. Database Schema (PostgreSQL)

- **users:** User info, roles, authentication
- **crop_batches:** Crop details, farmer, pricing, status
- **bids:** Retailer bids, amounts, status
- **orders:** Order details, links to bids, payment, delivery
- **payments:** Payment records, methods, status
- **notifications:** User notifications, type, read status
- **audit_logs:** Change tracking, user, operation, old/new values

### Sample Table: users

| Column       | Type         | Description                 |
| ------------ | ------------ | --------------------------- |
| id           | BIGSERIAL    | Primary key                 |
| username     | VARCHAR(50)  | Unique, required            |
| password     | VARCHAR(255) | Hashed                      |
| email        | VARCHAR(100) | Unique, required            |
| full_name    | VARCHAR(100) |                             |
| phone_number | VARCHAR(15)  |                             |
| role         | user_role    | Enum: FARMER/RETAILER/ADMIN |
| address      | TEXT         |                             |
| created_at   | TIMESTAMP    | Default now                 |
| updated_at   | TIMESTAMP    | Default now                 |

## 5. API Endpoints

See [server/agritrade/src/main/resources/static/endpoints.txt](server/agritrade/src/main/resources/static/endpoints.txt) for full list.

### Example:

- `POST /api/auth/register` — Register new user
- `POST /api/auth/login` — Login, receive JWT
- `GET /api/crops` — List available crops
- `POST /api/bids` — Place a bid
- `POST /api/orders` — Create order
- `POST /api/payments` — Make payment
- `GET /api/notifications` — Fetch notifications

## 6. Build & Run Instructions

### Client

- Install dependencies: `npm install`
- Start dev server: `npm run dev`

### Server

- Configure DB in [application.properties](server/agritrade/src/main/resources/application.properties)
- Build: `./mvnw clean install`
- Run: `./mvnw spring-boot:run`

## 7. Security

- JWT authentication
- Role-based access control
- CORS configuration

## 8. Additional Notes

- Audit logs for compliance
- Triggers for updated_at, order/payment numbers
- Views for reporting (active crops, order summary)

---

For detailed schema, see [schema.sql](server/agritrade/src/main/resources/static/schema.sql).
For API details, see [endpoints.txt](server/agritrade/src/main/resources/static/endpoints.txt).

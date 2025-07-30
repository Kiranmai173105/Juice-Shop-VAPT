 # Reconnaissance Notes – OWASP Juice Shop

## 1. Application Overview
- **URL:** `http://localhost:3000/#/`
- **Technology Stack:** Angular, Node.js, REST API
- **Purpose:** E-commerce site for juice products
- **Authentication:** Anonymous browsing allowed / Login required for checkout

---

## 2. Key Functionalities
- Home / Browse Products
- Login / Signup
- Search Products
- Add to Basket / Checkout
- Submit Feedback
- User Profile Management
- Admin Portal (if discovered)

---

## 3. Discovered Endpoints

### Public Endpoints

| Endpoint | Method | Description | Notes |
|----------|--------|-------------|-------|
| `http://localhost:3000/rest/products` | `GET` | Fetches product list | Returns full product details |
| `http://localhost:3000/rest/product/<id>` | `GET` | Fetch product details by ID | Possible IDOR check |
| `http://localhost:3000/rest/user/login` | `POST` | User login | Accepts JSON credentials |

### Authenticated Endpoints

| Endpoint | Method | Description | Notes |
|----------|--------|-------------|-------|
| `http://localhost:3000/rest/basket` | `GET` | Retrieve user's basket | Requires valid session token |
| `http://localhost:3000/rest/basket/<id>` | `POST`/`DELETE` | Add/remove items from basket | Check for authorization bypass |
| `http://localhost:3000/rest/feedback` | `POST` | Submit user feedback | Check for stored XSS or SQLi |

---

## 4. Parameters and Observations

### Login Request

```http
POST http://localhost:3000/rest/user/login
Content-Type: application/json

{
  "email": "test@test.com",
  "password": "123456"
}

## 📦 Setup Instructions

**Note:** Backend and mobile folders are uploaded as ZIP files. Extract them before running.

1. Extract `backend.zip` → `backend/`
2. Extract `mobile.zip` → `mobile/expense_tracker/`
3. Follow installation steps below
# 📡 Expense Tracker API Documentation

Base URL: `http://localhost:3000/api`

## 🔐 Authentication Endpoints

### 1. Register User
Creates a new user account.

**Endpoint:** `POST /register`

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Success Response:** `201 Created`
```json
{
  "message": "User created"
}
```

**Error Response:** `400 Bad Request`
```json
{
  "error": "User exists"
}
```

---

### 2. Login User
Authenticates user and returns JWT token.

**Endpoint:** `POST /login`

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Success Response:** `200 OK`
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Error Response:** `400 Bad Request`
```json
{
  "error": "Invalid credentials"
}
```

---

## 💰 Expense Endpoints (Protected)

All expense endpoints require JWT authentication.

**Authorization Header:**
```
Authorization: Bearer <your-jwt-token>
```

---

### 3. Get All Expenses
Retrieves all expenses for authenticated user.

**Endpoint:** `GET /expenses`

**Headers:** 
- `Authorization: Bearer <token>`

**Success Response:** `200 OK`
```json
{
  "expenses": [
    {
      "_id": "507f1f77bcf86cd799439011",
      "title": "Lunch",
      "amount": 250,
      "category": "Food",
      "description": "Office lunch with team",
      "date": "2026-01-10T10:30:00.000Z",
      "userId": "507f191e810c19729de860ea"
    }
  ],
  "total": 250
}
```

---

### 4. Add Expense
Creates a new expense.

**Endpoint:** `POST /expenses`

**Headers:** 
- `Authorization: Bearer <token>`
- `Content-Type: application/json`

**Request Body:**
```json
{
  "title": "Groceries",
  "amount": 500,
  "category": "Shopping",
  "description": "Weekly groceries",
  "date": "2026-01-10T18:00:00.000Z"
}
```

**Success Response:** `201 Created`
```json
{
  "_id": "507f1f77bcf86cd799439012",
  "title": "Groceries",
  "amount": 500,
  "category": "Shopping",
  "description": "Weekly groceries",
  "date": "2026-01-10T18:00:00.000Z",
  "userId": "507f191e810c19729de860ea"
}
```

---

### 5. Update Expense
Updates an existing expense.

**Endpoint:** `PUT /expenses/:id`

**Headers:** 
- `Authorization: Bearer <token>`
- `Content-Type: application/json`

**URL Parameters:**
- `id` - Expense ID

**Request Body:**
```json
{
  "title": "Updated Groceries",
  "amount": 600,
  "category": "Shopping",
  "description": "Updated description",
  "date": "2026-01-10T18:00:00.000Z"
}
```

**Success Response:** `200 OK`
```json
{
  "_id": "507f1f77bcf86cd799439012",
  "title": "Updated Groceries",
  "amount": 600,
  "category": "Shopping",
  "description": "Updated description",
  "date": "2026-01-10T18:00:00.000Z",
  "userId": "507f191e810c19729de860ea"
}
```

---

### 6. Delete Expense
Deletes an expense.

**Endpoint:** `DELETE /expenses/:id`

**Headers:** 
- `Authorization: Bearer <token>`

**URL Parameters:**
- `id` - Expense ID

**Success Response:** `200 OK`
```json
{
  "message": "Deleted"
}
```

---

## ⚠️ Error Responses

**401 Unauthorized**
```json
{
  "error": "Access denied"
}
```

**400 Bad Request**
```json
{
  "error": "Invalid token"
}
```

**500 Internal Server Error**
```json
{
  "error": "Server error"
}
```

---

## 🧪 Testing with Postman

1. **Register/Login** to get JWT token
2. **Copy the token**
3. Add to Authorization header: `Bearer <token>`
4. Test all expense endpoints

---

## 📝 Notes

- All dates are in ISO 8601 format
- Amounts are stored as numbers
- Passwords are hashed with bcrypt
- JWT tokens expire based on server configuration
- Description field is optional (default: empty string)
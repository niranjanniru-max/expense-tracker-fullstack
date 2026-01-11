## 📦 Setup Instructions

**Note:** Backend and mobile folders are uploaded as ZIP files. Extract them before running.

1. Extract `backend.zip` → `backend/`
2. Extract `mobile.zip` → `mobile/expense_tracker/`
3. Follow installation steps below


Base URL: `http://localhost:3000/api`
## ✨ Features

### 🔐 Authentication & Security (6 Features)
- ✅ User Registration with Email/Password
- ✅ Secure Login with JWT Tokens
- ✅ Password Encryption using bcrypt
- ✅ Persistent Session (Auto-login after app restart)
- ✅ Secure Logout
- ✅ Token-based API Authentication

### 💰 Expense Management (8 Features)
- ✅ Add New Expense
- ✅ Edit Existing Expense
- ✅ Delete Expense with Confirmation Dialog
- ✅ View All Expenses in Organized List
- ✅ Expense Title (required field)
- ✅ Amount with Validation
- ✅ Category Selection (5 predefined + unlimited custom)
- ✅ Expense Description/Notes (up to 150 characters)

### 🔍 Filtering & Search (7 Features)
- ✅ Real-time Search by Title
- ✅ Real-time Search by Category
- ✅ Filter by Month (All 12 months: Jan-Dec)
- ✅ Filter by Year (2021-2026, 6 years available)
- ✅ Auto-default to Current Month on app open
- ✅ Clear Search Button
- ✅ Combined Month + Year Filtering

### 📊 Sorting & Organization (3 Features)
- ✅ Sort by Date (Newest First)
- ✅ Sort by Amount (Highest First)
- ✅ Visual Checkmark for Active Sort Option

### 📈 Analytics & Insights (4 Features)
- ✅ Total Monthly Spending Display
- ✅ Transaction Count Display
- ✅ Category-wise Spending Breakdown
- ✅ Animated Counter (Smooth number transitions)

### 🎨 UI/UX Features (12 Features)
- ✅ Dark Mode Support
- ✅ Light Mode Support
- ✅ Theme Persistence (Remembers user choice)
- ✅ Smooth Fade Animations
- ✅ Slide Transitions
- ✅ Scale Animations on Floating Action Button
- ✅ Material Design 3
- ✅ Beautiful Gradient Backgrounds
- ✅ Loading Indicators
- ✅ Helpful Error Messages
- ✅ Empty State Displays
- ✅ Confirmation Dialogs (Prevents accidental actions)

### 📝 Form Features (7 Features)
- ✅ Date Picker
- ✅ Time Picker
- ✅ Category Dropdown
- ✅ Custom Category Input
- ✅ Character Counter for Descriptions
- ✅ Real-time Form Validation
- ✅ Clear Validation Error Messages

### 🔌 Backend API (6 Endpoints)
- ✅ POST `/api/register` - Create new user
- ✅ POST `/api/login` - Authenticate user
- ✅ GET `/api/expenses` - Fetch all expenses
- ✅ POST `/api/expenses` - Create expense
- ✅ PUT `/api/expenses/:id` - Update expense
- ✅ DELETE `/api/expenses/:id` - Delete expense

### 🗄️ Database (2 Collections)
- ✅ Users Collection (email, hashed password)
- ✅ Expenses Collection (title, amount, category, description, date, userId)

### 🛡️ Security Features (5 Features)
- ✅ JWT Token Authentication
- ✅ Password Hashing with bcrypt
- ✅ Protected API Endpoints
- ✅ User-specific Data Access
- ✅ Input Validation (Frontend + Backend)

### 📱 Additional Features (5 Features)
- ✅ Pull-to-Refresh
- ✅ About Screen with App Info
- ✅ Currency Formatting (₹1,250.00)
- ✅ Forgot Password UI
- ✅ Register/Login Toggle

---

**Total Features: 65+**

---

## 🎯 Categories

**Predefined Categories:**
- 🍔 Food
- 🚗 Transport  
- 🛍️ Shopping
- 📄 Bills
- 🎬 Entertainment

**Custom Categories:** Unlimited - users can create their own!

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


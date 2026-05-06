# 🔐 Accounts Module

> Handles user authentication for both **Patients** and **Doctors** using JWT (JSON Web Tokens).

---

## 📋 Overview

This module provides separate authentication flows for two user types — **Patients** and **Doctors**. Each has dedicated register, login, and logout endpoints. Authentication is powered by `djangorestframework-simplejwt` with token blacklisting support for secure logouts.

---

## 🔗 API Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|:---:|
| `POST` | `/auth/p/register/` | Register a new patient | ❌ |
| `POST` | `/auth/d/register/` | Register a new doctor | ❌ |
| `POST` | `/auth/p/login/` | Patient login | ❌ |
| `POST` | `/auth/d/login/` | Doctor login | ❌ |
| `POST` | `/auth/p/logout/` | Patient logout | ✅ |
| `POST` | `/auth/d/logout/` | Doctor logout | ✅ |
| `POST` | `/auth/token/` | Obtain JWT token pair | ❌ |
| `POST` | `/auth/token/refresh/` | Refresh access token | ❌ |

---

## 📦 Request / Response Examples

### Register Patient
```json
// POST /auth/p/register/
{
    "username": "john_patient",
    "password": "securePass123",
    "email": "john@example.com",
    "first_name": "John",
    "last_name": "Doe"
}

// Response 201
{
    "message": "User registered successfully",
    "user": { ... },
    "token": {
        "access": "eyJ...",
        "refresh": "eyJ..."
    }
}
```

### Login
```json
// POST /auth/p/login/
{
    "username": "john_patient",
    "password": "securePass123"
}

// Response 200
{
    "token": {
        "access": "eyJ...",
        "refresh": "eyJ..."
    }
}
```

### Logout
```json
// POST /auth/p/logout/
// Header: Authorization: Bearer <access_token>
{
    "refresh_token": "eyJ..."
}

// Response 205
{
    "message": "User logged out successfully"
}
```

---

## 📁 Files

| File | Description |
|------|-------------|
| `views.py` | API views for registration, login, logout |
| `serializers.py` | Patient and Doctor serializers |
| `urls.py` | URL patterns for auth endpoints |

---

## 👨‍💻 Author

**Vivek Kumar Verma** — [@vivekVerma2806](https://github.com/vivekVerma2806)

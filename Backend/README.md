# ⚙️ Backend — HealthStack API

> The backend engine powering HealthStack, built with **Django 5.0.7**, **Django REST Framework**, **Django Channels**, and **PostgreSQL**.

---

## 📁 Module Overview

| Module | Path | Description |
|--------|------|-------------|
| 🏥 **HealthStack** | `HealthStack/` | Core Django project — settings, URL routing, ASGI/WSGI config |
| 🔐 **Accounts** | `accounts/` | Patient & Doctor authentication (register, login, logout) |
| 📅 **Appointment** | `appointment/` | Appointment scheduling, booking, and management |
| 💬 **Chat** | `chat/` | Real-time WebSocket chat between users |
| 🏥 **Health App** | `health_app/` | Core data models — UserProfile, Patient, Doctor, Disease |
| 🧠 **MentalWellness** | `MentalWellness/` | Motivational quotes & doctor specialization tagging |

---

## 🚀 Quick Start

```bash
# From the project root
cd Backend

# Install dependencies
pip install -r ../requirements.txt

# Set up PostgreSQL database
# Create database: HealthStackDb

# Run migrations
python manage.py makemigrations
python manage.py migrate

# Start development server
python manage.py runserver
```

---

## 🔧 Configuration

### Database (PostgreSQL)

Configured in `HealthStack/settings.py`:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'HealthStackDb',
        'USER': 'postgres',
        'PASSWORD': '1234',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

### JWT Authentication

```python
SIMPLE_JWT = {
    'ACCESS_TOKEN_LIFETIME': timedelta(hours=24),
    'REFRESH_TOKEN_LIFETIME': timedelta(days=5),
    'BLACKLIST_AFTER_ROTATION': True,
}
```

### CORS Origins

```python
CORS_ALLOWED_ORIGINS = [
    "http://127.0.0.1:5500",
    "http://localhost:5173",
    "http://localhost:3000",
]
```

### WebSocket / Channels

- **ASGI Application:** `HealthStack.asgi.application`
- **Channel Layer:** `InMemoryChannelLayer` (use Redis in production)
- **Server:** Daphne

---

## 🗺️ URL Routing

| Prefix | App | Description |
|--------|-----|-------------|
| `/admin/` | Django Admin | Admin interface |
| `/auth/` | `accounts` | Authentication endpoints |
| `/chat/` | `chat` | Chat REST API + WebSocket |
| `/mentalwellness/` | `MentalWellness` | Wellness endpoints |
| `/appointment/` | `appointment` | Appointment CRUD |
| `/` | `health_app` | Core app routes |

---

## 🗃️ Data Models

### `health_app` — Core Models

```
UserProfile (AbstractUser)
├── dateOfBirth, gender, mobileNumber
├── first_name, middle_name, last_name
└── address

Patient (extends UserProfile)
├── bloodGroup (A+, A-, B+, B-, AB+, AB-, O+, O-)
└── isSpecialDisease

Doctor (extends UserProfile)
├── experience (max 50 years)
├── degree (MBBS, MD, DO, BDS, PhD, etc.)
├── speciality
└── doctor_tags (auto-generated array)

Disease
├── name (unique)
└── is_special (boolean)
```

### `appointment` — Scheduling Models

```
Day
└── name (Monday–Sunday)

Appointment
├── doctor (FK → Doctor)
├── day (FK → Day)
├── address, start_time
└── created_at

TakeAppointment
├── user (FK → Patient)
├── appointment (FK → Appointment)
├── phone_number
└── date
```

### `chat` — Messaging Models

```
ChatSession
├── chat_id (unique, 64 chars)
├── user1, user2 (FK → Patient)
└── created_time

Message
├── sender, receiver (FK → Patient)
├── body (text)
├── created_time
└── seen (boolean)
```

---

## 🧪 Running Tests

```bash
python manage.py test
```

---

## 👨‍💻 Author

**Vivek Kumar Verma** — [@vivekVerma2806](https://github.com/vivekVerma2806)

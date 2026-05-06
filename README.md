<div align="center">

# 🏥 HealthStack

### A Modern Healthcare Platform for the Digital Age

[![Django](https://img.shields.io/badge/Django-5.0.7-092E20?style=for-the-badge&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://reactjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

*A unified healthcare and communication platform with real-time chat, video consultations, appointment scheduling, and mental wellness features.*

---

</div>

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [API Documentation](#-api-documentation)
- [Environment Variables](#-environment-variables)
- [Contributing](#-contributing)
- [License](#-license)
- [Author](#-author)

---

## 🌟 Overview

**HealthStack** is a comprehensive digital healthcare platform designed to bridge the gap between patients and healthcare providers. Built with modern web technologies, it offers a seamless experience for managing healthcare interactions — from booking appointments and real-time messaging to video consultations and mental wellness support.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔐 **Dual Authentication** | Separate registration & login flows for Patients and Doctors with JWT tokens |
| 📅 **Smart Appointments** | Doctors create time slots by day; patients book, view, and cancel appointments |
| 💬 **Real-time Chat** | WebSocket-powered instant messaging between patients and doctors |
| 🎥 **Video Calling** | Integrated video consultation system for remote healthcare |
| 🧠 **Mental Wellness** | Motivational quotes and mental health resources |
| 📊 **Analytics & Charts** | Interactive data visualization for health insights |
| 📂 **Reports Module** | Secure upload, management, and sharing of healthcare reports |
| 🏷️ **Smart Doctor Tags** | Auto-generated specialization tags based on degree and specialty |

---

## 🛠️ Tech Stack

### Backend
- **Framework:** [Django 5.0.7](https://www.djangoproject.com/) + [Django REST Framework](https://www.django-rest-framework.org/)
- **Database:** [PostgreSQL](https://www.postgresql.org/)
- **Authentication:** JWT via [SimpleJWT](https://django-rest-framework-simplejwt.readthedocs.io/)
- **Real-time:** [Django Channels](https://channels.readthedocs.io/) + WebSockets
- **ASGI Server:** [Daphne](https://github.com/django/daphne)
- **CORS:** [django-cors-headers](https://github.com/adamchainz/django-cors-headers)

### Frontend
- **Framework:** [React](https://reactjs.org/) + [TailwindCSS](https://tailwindcss.com/)
- **Build Tool:** Vite

### DevOps (Future Scope)
- **Containerization:** Docker
- **CI/CD:** GitHub Actions

---

## 📂 Project Structure

```
HealthStack/
├── Backend/
│   ├── HealthStack/          # Django project settings & configuration
│   │   ├── settings.py       # Database, JWT, CORS, Channels config
│   │   ├── urls.py           # Root URL routing
│   │   ├── asgi.py           # ASGI application (WebSocket support)
│   │   ├── wsgi.py           # WSGI application
│   │   └── utils/            # Shared utilities (API response helper)
│   │
│   ├── accounts/             # 🔐 User authentication module
│   │   ├── views.py          # Registration, Login, Logout (Patient & Doctor)
│   │   ├── serializers.py    # User data serialization
│   │   └── urls.py           # Auth API routes
│   │
│   ├── appointment/          # 📅 Appointment management module
│   │   ├── models.py         # Day, Appointment, TakeAppointment models
│   │   ├── views.py          # CRUD operations for appointments
│   │   ├── serializers.py    # Appointment serialization
│   │   └── urls.py           # Appointment API routes
│   │
│   ├── chat/                 # 💬 Real-time chat module
│   │   ├── models.py         # ChatSession, Message models
│   │   ├── consumers.py      # WebSocket consumer for real-time messaging
│   │   ├── routing.py        # WebSocket URL routing
│   │   ├── views.py          # Chat REST API endpoints
│   │   └── utils/            # Chat utilities (ID generation)
│   │
│   ├── health_app/           # 🏥 Core health application
│   │   ├── models.py         # UserProfile, Patient, Doctor, Disease models
│   │   ├── tokens.py         # JWT token generation utility
│   │   └── urls.py           # Core app routes
│   │
│   ├── MentalWellness/       # 🧠 Mental wellness module
│   │   ├── views.py          # Quotes & tag generation endpoints
│   │   ├── constants.py      # Degree-specialization mappings
│   │   └── urls.py           # Mental wellness routes
│   │
│   └── manage.py             # Django management script
│
├── frontend/
│   └── healthstackFront/     # React frontend application
│
├── CONTRIBUTORS.md           # Project contributors
└── requirements.txt          # Python dependencies
```

---

## 🚀 Getting Started

### Prerequisites

- **Python** 3.10+
- **PostgreSQL** 15+
- **Node.js** 18+ & npm
- **Git**

### 1. Clone the Repository

```bash
git clone https://github.com/vivekVerma2806/HealthStack.git
cd HealthStack
```

### 2. Backend Setup

```bash
# Create and activate virtual environment
python -m venv venv
source venv/bin/activate        # Linux/Mac
venv\Scripts\activate           # Windows

# Install dependencies
pip install -r requirements.txt

# Configure PostgreSQL
# Create a database named 'HealthStackDb' in PostgreSQL

# Run migrations
cd Backend
python manage.py makemigrations
python manage.py migrate

# Create superuser (optional)
python manage.py createsuperuser

# Start the development server
python manage.py runserver
```

### 3. Frontend Setup

```bash
cd frontend/healthstackFront

# Install dependencies
npm install

# Start the development server
npm run dev
```

### 4. Access the Application

| Service | URL |
|---------|-----|
| Backend API | `http://localhost:8000` |
| Admin Panel | `http://localhost:8000/admin` |
| Frontend | `http://localhost:5173` |

---

## 📡 API Documentation

### Authentication (`/auth/`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/auth/p/register/` | Register a new patient |
| `POST` | `/auth/d/register/` | Register a new doctor |
| `POST` | `/auth/p/login/` | Patient login (returns JWT) |
| `POST` | `/auth/d/login/` | Doctor login (returns JWT) |
| `POST` | `/auth/p/logout/` | Patient logout (blacklists token) |
| `POST` | `/auth/d/logout/` | Doctor logout (blacklists token) |
| `POST` | `/auth/token/` | Obtain JWT token pair |
| `POST` | `/auth/token/refresh/` | Refresh access token |

### Appointments (`/appointment/`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/appointment/add/` | Create appointment slots (Doctor) |
| `PUT` | `/appointment/update/` | Update an appointment |
| `GET` | `/appointment/get-my-appointments/?username=<user>` | Get doctor's appointments |
| `DELETE` | `/appointment/delete/<id>/` | Delete an appointment |
| `POST` | `/appointment/take-appointment/` | Book an appointment (Patient) |
| `DELETE` | `/appointment/cancel-appointment/<patient_id>/<appointment_id>/` | Cancel booking |
| `GET` | `/appointment/get-patient-appointments/?username=<user>` | Get patient's bookings |
| `GET` | `/appointment/get-scheduled-appointments/` | Get scheduled appointments |

### Chat (`/chat/`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/chat/create-session/` | Create a chat session |
| `GET` | `/chat/messages/<chat_id>/` | Get chat messages |
| `DELETE` | `/chat/delete-session/<chat_id>/` | Delete a chat session |
| `DELETE` | `/chat/delete-message/<message_id>/` | Delete a message |

### WebSocket

| Protocol | Endpoint | Description |
|----------|----------|-------------|
| `WS` | `ws://localhost:8000/ws/chat/<sender_username>/` | Real-time chat connection |

### Mental Wellness (`/mentalwellness/`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/mentalwellness/motivational-quote/` | Get a random motivational quote |
| `GET` | `/mentalwellness/mentalwellness-quote/` | Get a mental wellness quote |

---

## ⚙️ Environment Variables

Configure these in `Backend/HealthStack/settings.py`:

| Variable | Default | Description |
|----------|---------|-------------|
| `SECRET_KEY` | (auto-generated) | Django secret key |
| `DEBUG` | `True` | Debug mode |
| `DATABASE_NAME` | `HealthStackDb` | PostgreSQL database name |
| `DATABASE_USER` | `postgres` | Database user |
| `DATABASE_PASSWORD` | `1234` | Database password |
| `DATABASE_HOST` | `localhost` | Database host |
| `DATABASE_PORT` | `5432` | Database port |

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork** the repository
2. **Create** your feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<div align="center">

## 👨‍💻 Author

**Vivek Kumar Verma** — [@vivekVerma2806](https://github.com/vivekVerma2806)

⭐ Star this repo if you found it helpful!

</div>

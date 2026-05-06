# 🎨 Frontend — HealthStack

> React-based frontend for the HealthStack healthcare platform.

---

## 📋 Overview

This is the frontend application for HealthStack, built with **React** and **TailwindCSS**. It provides the user interface for patients and doctors to interact with the platform — including authentication, appointment management, real-time chat, and health data visualization.

---

## 🛠️ Tech Stack

- **Framework:** React 18
- **Styling:** TailwindCSS
- **Build Tool:** Vite
- **HTTP Client:** Axios / Fetch API
- **WebSocket:** Native WebSocket API for real-time chat

---

## 🚀 Getting Started

```bash
cd frontend/healthstackFront

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

### Development URLs

| Service | URL |
|---------|-----|
| Frontend Dev Server | `http://localhost:5173` |
| Backend API | `http://localhost:8000` |

---

## 🔗 API Integration

The frontend connects to the Django backend at:
- **REST API:** `http://localhost:8000/`
- **WebSocket:** `ws://localhost:8000/ws/chat/<username>/`

Ensure CORS is configured in the backend `settings.py` to allow requests from the frontend origin.

---

## 👨‍💻 Author

**Vivek Kumar Verma** — [@vivekVerma2806](https://github.com/vivekVerma2806)

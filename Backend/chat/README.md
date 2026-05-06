# 💬 Chat Module

> Real-time messaging system using **Django Channels** and **WebSockets**.

---

## 📋 Overview

This module provides a real-time chat system between users (patients and doctors). It uses **WebSockets** via Django Channels for instant message delivery, with REST API endpoints for session management and message history retrieval.

---

## 🏗️ Architecture

```
┌─────────────┐     WebSocket      ┌──────────────────┐
│   Client A   │ ◄───────────────► │                  │
│  (Patient)   │                   │  ChatRoomConsumer │
└─────────────┘                    │  (Django Channels)│
                                   │                  │
┌─────────────┐     WebSocket      │  In-Memory        │
│   Client B   │ ◄───────────────► │  Channel Layer    │
│  (Doctor)    │                   │                  │
└─────────────┘                    └──────────────────┘
                                          │
                                          ▼
                                   ┌──────────────┐
                                   │  PostgreSQL   │
                                   │  (Messages)   │
                                   └──────────────┘
```

### How it works:
1. Client connects via WebSocket at `ws://localhost:8000/ws/chat/<sender_username>/`
2. Server accepts and maps the username → channel name
3. Client sends a message with `receiver_username` and `message`
4. Server stores the message in PostgreSQL
5. If receiver is online, message is forwarded instantly via their WebSocket
6. Offline messages are stored and retrievable via REST API

---

## 🗃️ Data Models

### ChatSession
| Field | Type | Description |
|-------|------|-------------|
| `chat_id` | CharField (64, unique) | Unique session identifier |
| `user1` | ForeignKey → Patient | First participant |
| `user2` | ForeignKey → Patient | Second participant |
| `created_time` | DateTimeField | Auto-set on creation |

### Message
| Field | Type | Description |
|-------|------|-------------|
| `sender` | ForeignKey → Patient | Message sender |
| `receiver` | ForeignKey → Patient | Message receiver |
| `body` | TextField | Message content |
| `created_time` | DateTimeField | Auto-set on creation |
| `seen` | BooleanField | Read receipt status (default: `False`) |

---

## 🔗 REST API Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|:----:|
| `POST` | `/chat/create-session/` | Create or retrieve a chat session | ✅ |
| `GET` | `/chat/messages/<chat_id>/` | Get all messages in a session | ✅ |
| `DELETE` | `/chat/delete-session/<chat_id>/` | Delete a chat session | ✅ |
| `DELETE` | `/chat/delete-message/<message_id>/` | Delete a specific message | ✅ |

## 🔌 WebSocket Endpoint

| Protocol | URL | Description |
|----------|-----|-------------|
| `WS` | `ws://localhost:8000/ws/chat/<sender_username>/` | Connect to chat |

### WebSocket Message Format

**Send:**
```json
{
    "message": "Hello Doctor!",
    "receiver_username": "dr_smith"
}
```

**Receive:**
```json
{
    "message": "Hello Doctor!",
    "sender_username": "john_patient"
}
```

---

## 📁 Files

| File | Description |
|------|-------------|
| `models.py` | ChatSession and Message models |
| `consumers.py` | WebSocket consumer for real-time messaging |
| `routing.py` | WebSocket URL routing |
| `views.py` | REST API views for chat management |
| `serializers.py` | Message serializer |
| `urls.py` | REST API URL patterns |
| `utils/getChatId.py` | Chat ID generation utility |

---

## 👨‍💻 Author

**Vivek Kumar Verma** — [@vivekVerma2806](https://github.com/vivekVerma2806)

# 📅 Appointment Module

> Complete appointment scheduling system for doctor-patient interactions.

---

## 📋 Overview

This module enables **Doctors** to create appointment slots across multiple days and **Patients** to browse, book, and cancel those appointments. It includes full CRUD operations with a structured Day → Appointment → Booking hierarchy.

---

## 🗃️ Data Models

### Day
| Field | Type | Description |
|-------|------|-------------|
| `name` | CharField (choices) | Day of the week (Monday–Sunday) |

### Appointment
| Field | Type | Description |
|-------|------|-------------|
| `doctor` | ForeignKey → Doctor | Assigned doctor |
| `day` | ForeignKey → Day | Day of the week |
| `address` | CharField | Clinic/hospital address |
| `start_time` | CharField | Appointment start time |
| `created_at` | DateTimeField | Auto-set on creation |

### TakeAppointment
| Field | Type | Description |
|-------|------|-------------|
| `user` | ForeignKey → Patient | Patient booking |
| `appointment` | ForeignKey → Appointment | Linked appointment slot |
| `phone_number` | CharField | Patient contact number |
| `date` | DateTimeField | Booking timestamp |

---

## 🔗 API Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|:----:|
| `POST` | `/appointment/add/` | Create appointment slots (Doctor) | ✅ |
| `PUT` | `/appointment/update/` | Update appointment details | ✅ |
| `GET` | `/appointment/get-my-appointments/?username=<user>` | Get doctor's appointments | ✅ |
| `GET` | `/appointment/get-my-appointments/<pk>/` | Get single appointment | ✅ |
| `DELETE` | `/appointment/delete/<id>/` | Delete an appointment | ✅ |
| `POST` | `/appointment/take-appointment/` | Book an appointment (Patient) | ✅ |
| `DELETE` | `/appointment/cancel-appointment/<patient_id>/<appt_id>/` | Cancel a booking | ✅ |
| `GET` | `/appointment/get-patient-appointments/?username=<user>` | Get patient's bookings | ✅ |
| `GET` | `/appointment/get-scheduled-appointments/` | Get doctor's scheduled bookings | ✅ |

---

## 📦 Request Examples

### Create Appointment (Doctor)
```json
// POST /appointment/add/
// Header: Authorization: Bearer <access_token>
{
    "days": ["Monday", "Wednesday", "Friday"],
    "start_time": "10:00 AM",
    "address": "City Hospital, Room 204"
}
```

### Book Appointment (Patient)
```json
// POST /appointment/take-appointment/
{
    "patient_id": 5,
    "appointment_id": 12,
    "phone_number": "+91-9876543210"
}
```

---

## 📁 Files

| File | Description |
|------|-------------|
| `models.py` | Day, Appointment, TakeAppointment models |
| `views.py` | All appointment CRUD view functions |
| `serializers.py` | Appointment & TakeAppointment serializers |
| `urls.py` | URL patterns for appointment endpoints |
| `admin.py` | Admin registration for models |

---

## 👨‍💻 Author

**Vivek Kumar Verma** — [@vivekVerma2806](https://github.com/vivekVerma2806)

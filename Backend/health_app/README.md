# 🏥 Health App Module

> Core data models and user management for the HealthStack platform.

---

## 📋 Overview

This is the foundational module of HealthStack. It defines the core data models — **UserProfile**, **Patient**, **Doctor**, and **Disease** — that all other modules depend on. It also contains the JWT token generation utility and serves as the custom user model for Django authentication.

---

## 🗃️ Data Models

### UserProfile (AbstractUser)

Base user model extending Django's `AbstractUser`. Configured as `AUTH_USER_MODEL = 'health_app.UserProfile'`.

| Field | Type | Description |
|-------|------|-------------|
| `username` | CharField | Unique username (inherited) |
| `email` | EmailField | User email (inherited) |
| `password` | CharField | Hashed password (inherited) |
| `first_name` | CharField (200) | First name |
| `middle_name` | CharField (200) | Middle name (optional) |
| `last_name` | CharField (200) | Last name (optional) |
| `dateOfBirth` | DateField | Date of birth |
| `gender` | CharField (1) | `M` (Male), `F` (Female), `O` (Other) |
| `mobileNumber` | CharField (17) | Phone number |
| `address` | CharField (300) | Residential address |
| `created` | DateTimeField | Auto-set on creation |
| `updated` | DateTimeField | Auto-updated on save |

### Patient (extends UserProfile)

| Field | Type | Description |
|-------|------|-------------|
| `bloodGroup` | CharField (4) | Blood group (A+, A-, B+, B-, AB+, AB-, O+, O-) |
| `isSpecialDisease` | BooleanField | Has special disease flag |

### Doctor (extends UserProfile)

| Field | Type | Description |
|-------|------|-------------|
| `experience` | IntegerField | Years of experience (max: 50) |
| `degree` | CharField (50) | Medical degree (MBBS, MD, DO, BDS, PhD, etc.) |
| `speciality` | CharField (100) | Specialization area |
| `doctor_tags` | ArrayField | Auto-generated specialization tags |

**Supported Degrees:** MBBS, MD, DO, DNB, MS, BDS, MDS, PhD, MPH, DM, MCh, BAMS, BHMS, BPT, MPT, BVSc, MSc, DGO, FRCS, MRCP, DCH, DPH, DDS

### Disease

| Field | Type | Description |
|-------|------|-------------|
| `name` | CharField (255, unique) | Disease name |
| `is_special` | BooleanField | Whether it's a special/private disease |

---

## 🔧 Utilities

### `tokens.py` — JWT Token Generation

```python
from health_app.tokens import get_token_for_user

token = get_token_for_user(user)
# Returns: { "access": "...", "refresh": "..." }
```

---

## 📁 Files

| File | Description |
|------|-------------|
| `models.py` | UserProfile, Patient, Doctor, Disease models |
| `tokens.py` | JWT token generation utility |
| `urls.py` | Core app URL patterns |
| `admin.py` | Admin registration |
| `serializers.py` | Data serializers |

---

## 👨‍💻 Author

**Vivek Kumar Verma** — [@vivekVerma2806](https://github.com/vivekVerma2806)

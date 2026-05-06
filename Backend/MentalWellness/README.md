# 🧠 Mental Wellness Module

> Motivational quotes, mental health resources, and smart doctor specialization tagging.

---

## 📋 Overview

This module serves two purposes:
1. **Mental Wellness Quotes** — Provides random motivational and mental wellness quotes via API endpoints
2. **Smart Doctor Tagging** — Automatically generates relevant specialization tags for doctors based on their degree and specialty text using a comprehensive degree-to-specialization mapping

---

## 🔗 API Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|:----:|
| `GET` | `/mentalwellness/motivational-quote/` | Get a random motivational quote | ❌ |
| `GET` | `/mentalwellness/mentalwellness-quote/` | Get a mental wellness quote | ❌ |

---

## 🏷️ Doctor Tag Generation

The `generate_tags_from_specialty()` function analyzes a doctor's specialty text and automatically generates relevant tags using a built-in mapping of **23 medical degrees** to their fields and keywords.

### Example

```python
from MentalWellness.views import generate_tags_from_specialty

tags = generate_tags_from_specialty("cardiology specialist")
# Returns: ["Specialized Medicine", "physician", "internal medicine",
#           "pediatrics", "cardiology", "neurology", "psychiatry",
#           "Super Speciality Medicine", "nephrology", "endocrinology",
#           "gastroenterology"]
```

### Supported Degree Mappings

| Degree | Field | Sample Keywords |
|--------|-------|-----------------|
| MBBS | General Medicine | primary care, general practitioner |
| MD | Specialized Medicine | physician, cardiology, neurology |
| DO | Osteopathic Medicine | holistic, musculoskeletal |
| MS | Surgery | general surgery, orthopedics, ENT |
| BDS | Dental Surgery | dentist, oral health |
| PhD | Medical Research | research, academic, laboratory |
| DM | Super Speciality Medicine | cardiology, nephrology |
| MCh | Super Speciality Surgery | neurosurgery, plastic surgery |
| BAMS | Ayurvedic Medicine | ayurveda, herbal medicine |
| BHMS | Homeopathic Medicine | homeopathy, alternative medicine |
| BPT | Physiotherapy | rehabilitation, exercise |
| DGO | Gynecology & Obstetrics | women's health, pregnancy |
| DCH | Pediatrics | child care, children's health |

*...and 10 more degrees. See `constants.py` for the full mapping.*

---

## 📁 Files

| File | Description |
|------|-------------|
| `views.py` | Quote endpoints and tag generation function |
| `constants.py` | Degree choices and degree-to-specialization mapping |
| `urls.py` | URL patterns for wellness endpoints |

---

## 👨‍💻 Author

**Vivek Kumar Verma** — [@vivekVerma2806](https://github.com/vivekVerma2806)

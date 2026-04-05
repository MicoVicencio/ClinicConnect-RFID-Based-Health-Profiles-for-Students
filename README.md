# 🏥 ClinicConnect: RFID-Based Health Profiles for Students

> **System #04 · Health Management**
> Capstone Project — Bachelor of Science in Computer Science
> Cainta Catholic College

---

## 📖 Overview

**ClinicConnect** is an RFID-based student health management system that replaces slow, paper-based medical records with instant digital health profile retrieval. When a student's ID card is scanned, their full medical history, allergies, and emergency contacts appear immediately for clinic staff — and parents are automatically notified via EmailJS whenever their child visits the clinic.

ClinicConnect reduces critical delays in emergencies by eliminating the need to search through physical documents, enabling school clinic personnel to act faster and smarter.

---

## ✨ Features

- **Instant RFID Health Retrieval** — Scanning a student's RFID card (range: 3–10 cm) instantly loads their complete health profile for clinic staff.
- **Digital Health Records** — Stores medical history, allergies, medications, and emergency contact details in a structured SQLite database.
- **Web-Based Clinic Interface** — Clinic personnel manage and view health records through a clean HTML/CSS/JS web interface.
- **Automated Parent Notifications** — EmailJS automatically sends email alerts to parents/guardians whenever a student receives clinic attention.
- **Faster Emergency Response** — Eliminates paper searching, reducing critical delays when students need urgent medical care.

---

## 🛠️ Technologies Used

| Category      | Technologies                             |
|---------------|------------------------------------------|
| **Languages** | Python, HTML, CSS, JavaScript            |
| **Database**  | SQLite                                   |
| **APIs**      | EmailJS                                  |
| **Hardware**  | RFID Reader, RFID Cards                  |

---

## 🏗️ System Architecture

```
[Student RFID Card Scan]  (3–10 cm range)
          │
          ▼
[RFID Reader (USB/Serial)]
          │
          ▼
  [Python Backend]
    ┌─────┴──────┐
    ▼             ▼
[SQLite DB]   [Web Server (localhost)]
 (Health        │
  Records)       ▼
            [HTML/CSS/JS
             Clinic Interface]
                  │
                  ▼
            [EmailJS API]
                  │
                  ▼
        [Parent/Guardian Email Alert]
```

---

## ⚙️ How It Works

1. A student visits the school clinic.
2. The clinic staff scans the student's RFID card on the reader.
3. The Python backend reads the card UID and queries the SQLite database.
4. The student's **full health profile** is instantly displayed on the clinic web interface — including medical history, allergies, current medications, and emergency contacts.
5. Clinic staff logs the visit and any treatment administered.
6. EmailJS automatically sends an email notification to the student's parent or guardian.
7. All visit records are stored permanently in the database for future reference.

---

## 🗂️ Database Schema

### `students` Table
| Column          | Type    | Description                      |
|-----------------|---------|----------------------------------|
| id              | INTEGER | Primary key (auto-increment)     |
| rfid_uid        | TEXT    | Unique RFID card identifier      |
| full_name       | TEXT    | Student's full name              |
| grade           | TEXT    | Grade level                      |
| section         | TEXT    | Section                          |
| date_of_birth   | TEXT    | Date of birth                    |
| parent_email    | TEXT    | Guardian's email for alerts      |
| emergency_contact | TEXT  | Emergency contact number         |

### `health_records` Table
| Column       | Type    | Description                         |
|--------------|---------|-------------------------------------|
| record_id    | INTEGER | Primary key (auto-increment)        |
| rfid_uid     | TEXT    | Foreign key → students.rfid_uid     |
| allergies    | TEXT    | Known allergies                     |
| medications  | TEXT    | Current medications                 |
| medical_history | TEXT | Medical conditions / history       |
| blood_type   | TEXT    | Student's blood type                |

### `clinic_visits` Table
| Column        | Type     | Description                        |
|---------------|----------|------------------------------------|
| visit_id      | INTEGER  | Primary key (auto-increment)       |
| rfid_uid      | TEXT     | Foreign key → students.rfid_uid    |
| visit_date    | DATETIME | Date and time of clinic visit      |
| complaint     | TEXT     | Reason for visit                   |
| treatment     | TEXT     | Treatment given                    |
| nurse_notes   | TEXT     | Additional nurse observations      |

---

## 📋 Prerequisites

- Python 3.x
- RFID reader module (range: 3–10 cm, e.g., RC522 or USB HID reader)
- RFID cards / student ID cards with embedded chip
- EmailJS account (for parent email notifications)
- A modern web browser (Chrome, Firefox, Edge)

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/your-repo/clinicconnect.git
cd clinicconnect
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

Required packages:
```
pyserial      # RFID reader communication
flask         # Web server (or equivalent)
```
> **Note:** `sqlite3` is included in the Python standard library.

### 3. Configure EmailJS
- Create an account at [emailjs.com](https://www.emailjs.com/).
- Set up an email template for clinic visit notifications.
- Update your credentials in `config.js`:
```javascript
const EMAILJS_SERVICE_ID  = "your_service_id";
const EMAILJS_TEMPLATE_ID = "your_template_id";
const EMAILJS_PUBLIC_KEY  = "your_public_key";
```

### 4. Configure the RFID Reader
Update the serial port in `config.py`:
```python
RFID_PORT = "COM3"         # Windows
# RFID_PORT = "/dev/ttyUSB0"  # Linux/Mac
BAUD_RATE  = 9600
```

### 5. Run the Backend Server
```bash
python app.py
```

### 6. Open the Clinic Interface
Navigate to `http://localhost:5000` in a web browser on the clinic workstation.

---

## 📧 Email Notification Template

When a student is seen at the clinic, the following information is sent automatically to the parent/guardian:

> **Subject:** Clinic Visit Alert — [Student Name]
>
> Dear Parent/Guardian,
>
> This is to inform you that **[Student Name]** from **[Grade & Section]** visited the school clinic on **[Date & Time]**.
>
> **Complaint:** [Complaint]
> **Treatment Administered:** [Treatment]
>
> Please contact the school clinic for further details.

---

## 🔒 Privacy & Security

- Student health records are stored locally in an SQLite database — no data is sent to external servers except for email notifications.
- Only registered clinic staff with access to the clinic workstation can view health records.
- RFID cards do not store any personal data; all sensitive information resides in the local database.

---

## 👥 Team

| Name | Role |
|------|------|
| Alvarado, John Zymond D. | BSCS Student |
| Arado, Nemuel Adrian | BSCS Student |
| Bañas, JhonPaul B. | BSCS Student |
| Gabilo, Carl Allen R. | BSCS Student |
| Vicencio, Mico D. | Group Leader / Main Programmer |

---

## 🏫 Institution

**Cainta Catholic College**
Bachelor of Science in Computer Science — BSCS Tech Expo

---

*Built with ❤️ by BSCS Students of Cainta Catholic College*

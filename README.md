#  CampusCare — Mental Health Early Support System

> A university-wide mental health platform connecting students, counselors, the Dean of Students, and administrators in one secure, role-based system.

---

##  About the Project

CampusCare is a web-based **Mental Health Early Support System** built for university environments. It provides an early warning and intervention platform that monitors student wellbeing through daily mood check-ins, academic attendance, and coursework performance — flagging students who may be silently struggling before situations become critical.

The system is designed around a simple truth: **most students do not ask for help until it is too late.** CampusCare bridges that gap by giving counselors and the Dean of Students the data and tools they need to reach out first.

---

##  Live Portals

The system is divided into four role-based portals, each with its own login and dashboard:

| Portal | Role | Access |
|---|---|---|
| **Student Portal** | Students | Daily check-ins, journal, wellbeing history, request counselor |
| **Counselor Portal** | Counselors | Manage sessions, view student trends, write notes, accept/decline requests |
| **Dean of Students Portal** | Dean | Monitor flagged students, track cases, post resources, generate reports |
| **Admin Console** | System Admin | Full user management, counselor assignment, system monitoring, announcements |

---

##  Key Features

### For Students
- Daily **Mental Health Check-In** — 10 clinically-informed questions scored and tracked over time
- Personal **Wellbeing Progress Chart** — see trends across multiple check-ins
- Private **Journal** with guided writing prompts
- **Request a Counselor** directly from the portal
- View semester **attendance and coursework marks** per unit

### For Counselors
- Accept or decline student counseling requests
- View assigned students' wellbeing trends and academic performance
- Write **confidential session notes** (private to the counselor only)
- Mark session attendance (attended / missed / upcoming)
- Wellness trend charts per student

### For the Dean of Students
- Dashboard summary: total students needing help, new alerts, high/medium/low risk flags
- **Risk-level flagging** based on attendance (40%+ absence) and academic performance (grades below 40)
- Case status tracking: Open → In Progress → Follow-Up → Resolved
- Follow-up reminders with urgent priority flags
- Post welfare resources to the student resource hub
- Generate and export welfare reports as CSV

### For Administrators
- Full **user management** across all roles
- **Counselor assignment** — view student requests and assign the right counselor
- System monitoring and login activity logs
- Resource management — upload and manage wellness content
- Broadcast **announcements** to all users
- Database backup and recovery tools
- Usage reports and analytics

---

##  Privacy & Safety

- Detailed therapy notes, private counselor records, and psychiatric information are **never visible** to the Dean or Admin — only the counselor assigned to the student can access them
- Student check-in responses are stored per-session and only surfaced as aggregated scores to support staff
- All passwords are **hashed using PHP `password_hash()`** (bcrypt) — plain-text passwords are never stored
- Role-based access control enforced at both the front end and the PHP session layer

---

##  Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | HTML, CSS, JavaScript|
| **Backend** | PHP  |
| **Database** | MySQL (MariaDB via XAMPP) |
| **Charts** | Chart.js |
| **Icons** | Font Awesome 6 |
| **Fonts** | Google Fonts  Poppins |
| **Local Server** | XAMPP (Apache + MySQL) |

---

##  Database Schema

The system uses the following tables:

```
students          — student accounts and credentials
counselors        — counselor accounts and department info
dean              — Dean of Students account
admins            — system administrator accounts
units             — the 8 units/courses students are enrolled in
semesters         — semester records (4-month cycles)
enrollments       — which student is enrolled in which unit per semester
attendance        — per-student, per-unit, per-class attendance records
grades            — CAT1 (15), CAT2 (15), Assignment (10), Exam (60) per unit
counselor_requests— student counselor requests and assignment status
```

**Early warning thresholds:**
- Absence rate **≥ 40%** in any unit → flagged At Risk
- Total score **< 40 / 100** in any unit → failing (grade F)
- 3+ failing units OR 40%+ overall absence → academic At Risk flag shown to counselor and Dean

---

## Getting Started

### Prerequisites
- [XAMPP](https://www.apachefriends.org/) (Apache + MySQL)
- A modern browser (Chrome, Firefox, Edge)

### Setup

1. **Clone the repository** into your XAMPP htdocs folder:
   ```bash
   git clone https://github.com/yourusername/campuscare.git
   cd xampp/htdocs/campuscare
   ```

2. **Start XAMPP** — make sure both Apache and MySQL are running.

3. **Create the database** — open `http://localhost/phpmyadmin`, create a new database called `campuscare_db`, then run the SQL files in order:
   ```
   database/01_create_tables.sql
   database/02_seed_users.sql       ← generated by generate_seeds.php
   database/03_seed_attendance.sql  ← generated by generate_attendance.php
   ```

4. **Run the seed generators** to create hashed passwords:
   - Visit `http://localhost/campuscare/generate_seeds.php`
   - Copy the SQL output → paste into phpMyAdmin → click Go
   - **Delete `generate_seeds.php` immediately after**

5. **Access the system**:
   ```
   http://localhost/campuscare/Home.html
   ```

---

##  Demo Credentials

> These are development credentials only. Change all passwords before any real deployment.

| Role | Login Field | Value | Password |
|---|---|---|---|
| Student | Admission No | `ADM-2024-001` | `ADM-2024-001` |
| Counselor | Staff ID | `CSL-001` | `CSL-001` |
| Dean | Email | `z.cheli@university.edu` | `Dean@2026` |
| Admin | Username | `admin` | `Admin@2026` |

---

##  Project Structure

```
campuscare/
├── Home.html                  # Landing page with portal selection
├── About.html
├── Services.html
├── Resources.html
├── Contact.html
│
├── student-login.html         # Student login page
├── student-login.php          # Student auth handler
├── student-portal.html        # Student dashboard
├── studentportal.css
│
├── counselor-login.html
├── counselor-login.php
├── counselor-portal.html
├── counselorportal.css
│
├── dean-login.html
├── dean-login.php
├── dean-portal.php            # Dean portal (PHP session auth)
├── dean-portal.css
│
├── admin-login.html
├── admin-login.php
├── admin-portal.php           # Admin portal (PHP session auth)
├── adminportal.css
├── script.js                  # Admin portal JavaScript
│
├── checkin.html               # Mental health check-in form
│
├── db.php                     # Database connection (not committed)
├── admin-api.php              # Admin data API
├── admin-logout.php
├── dean-logout.php
│
├── generate_seeds.php         # Password hash generator (delete after use)
├── generate_attendance.php    # Attendance data generator (delete after use)
│
└── style.css                  # Shared styles
```





##  User Roles Summary

```
Admin          → Full system control, no access to student therapy data
Dean           → Welfare overview, risk flags, case tracking — no therapy notes
Counselor      → Full student support tools, private session notes
Student        → Personal wellbeing tools, academic view, counselor request
```

---

##  License

This project was developed as a university-level software engineering project.  
© 2026 CampusCare — Mental Health Early Support System. All rights reserved.

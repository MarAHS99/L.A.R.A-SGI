# 🐄 L.A.R.A SGI — Integrated Management System

> **A real-world fullstack business management system** built for a meat byproducts distributor in Miramar, Argentina.
> Designed and developed solo. Currently in active production use by the client.

---

## 📸 Screenshots

| Dashboard — Monthly Summary | Profitability by Product |
|---|---|
| ![Dashboard](screenshots/lara-1.png) | ![Profitability](screenshots/lara-2.png) |

| Invoice Creation | Accounts Receivable |
|---|---|
| ![Invoice](screenshots/lara-3.png) | ![Accounts](screenshots/lara-4.png) |

| Daily Closing Report |
|---|
| ![Closing](screenshots/lara-5.png) |

---

## 🧩 What is L.A.R.A SGI?

L.A.R.A SGI (Integrated Management System) is an internal business management system built to fully replace an Excel-based workflow for a meat byproducts distribution company in Miramar, Argentina.

The system covers the complete operational cycle: invoice creation with automatic balance and delivery payment tracking, per-product profitability analysis, client account management grouped by location, vendor account tracking, field worker expense logging, and period-based analytical reporting with Excel export.

Packaged as a **native Windows desktop application** — no browser required, no internet connection, no external servers.

---

## ⚙️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python · FastAPI · SQLAlchemy |
| Database | SQLite (local, embedded) |
| Frontend | Vanilla JavaScript · HTML · CSS |
| Design | Custom design system — CSS variables · dark/light mode · Syne / DM Sans / DM Mono |
| Desktop | PyWebView (native window) |
| Packaging | PyInstaller · Inno Setup |
| Security | PBKDF2-HMAC-SHA256 · rate limiting · role-based access |

---

## ✅ Features

**Authentication & Access Control**
- Cookie-based session login with PBKDF2-HMAC-SHA256 password hashing
- Rate limiting: 5 failed attempts → 60s lockout
- Two-role system: `admin` (full access) / `viewer` (read-only)
- Middleware-level write protection for viewer role

**Invoice Management**
- Create, edit, and delete invoices with semantic ID generation (`LOC-YYYY-MM-DD-CLIENT-NNN`)
- Automatic previous balance calculation with high-debt alert
- Automatic delivery payment registration (flagged AUTO, non-deletable)
- Optional invoice notes, "Pay now" checkbox, keyboard shortcuts (`Ctrl+S`, `Enter`)
- Last price per client auto-filled on new invoice
- Paginated history (75/page) with date, client and location filters

**Purchases**
- Per-supplier purchase logging with optional unit count
- Backend-calculated subtotals

**Field Worker Expenses**
- Expense logging per workday: date, worker, amount, location, notes
- Automatically discounted in closing report and analytics

**Analytics Dashboard**
- Period-over-period comparison (last 3 days / week / month / year)
- Gross margin = revenue − purchases
- Net margin = revenue − purchases − field worker expenses
- Per-product profitability: kg sold · revenue · cost · margin $ · margin %
- Inactive clients report (15 / 30 / 60 / 90 days)

**Closing Report**
- Date-range filters with location → client breakdown
- Net total = revenue − purchases − field worker expenses

**Excel Export**
- Product grid with fixed per-supplier columns
- Client accounts receivable
- Field worker expenses detail
- Supplier accounts payable
- Net margin highlighted block

**UI/UX**
- Dark / light mode toggle (persists via localStorage)
- Sidebar client quick-access
- Full keyboard navigation on invoice form

---

## 🚀 Running Locally

```bash
git clone https://github.com/MarAHS99/LARA-SGI.git
cd LARA-SGI

pip install -r requirements.txt

cp .env.example .env
# Edit .env with your credentials

# Run migrations (first time only)
python migratecancomp.py
python migratev06.py
python migrate_gastos_achurero.py

python app_launcher.py
```

---

## 📦 Packaging as .exe

```bash
pip install pyinstaller
pyinstaller lara.spec
# Output: dist/LARA/LARA.exe

# Generate installer: open lara_installer.iss with Inno Setup → F9
# Output: installer/LARA_Menudencias_v1.0.exe
```

The database is stored in `AppData\Local\LARAMenudencias\lara.db` and is **preserved on uninstall**.

---

## 🔐 Environment Variables

```env
LARA_USER=admin_username
LARA_PASSWORD=admin_password
LARA_USER_LUIS=viewer_username
LARA_PASSWORD_LUIS=viewer_password
```

Copy `.env.example` as `.env` and fill in your values.

---

## 🏗️ Architecture

```
Client (PyWebView native window)
        │
        ▼
FastAPI (REST API · localhost only)
        │
        ├── SQLAlchemy ORM → SQLite (embedded, AppData)
        └── Static files (HTML · CSS · JS)
```

---

## 🌐 Español

Sistema de gestión integral para una distribuidora de achuras en Miramar, Argentina. Reemplaza completamente el flujo manual en Excel. Incluye gestión de ventas, compras, cuentas corrientes, gastos de achureros, análisis de rentabilidad, cierre por períodos y exportación a Excel. Empaquetado como aplicación de escritorio nativa para Windows.

---

## 👨‍💻 Developer

**Marcelo Nazareth Aguirre** — Fullstack Developer · La Plata, Argentina

[![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/marcelo-nazareth-aguirre-aa4a94251/)
[![GitHub](https://img.shields.io/badge/GitHub-%23121011.svg?style=flat&logo=github&logoColor=white)](https://github.com/MarAHS99)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:aguirre.marcelo.ext@gmail.com)

---

## 📄 License

© 2026 Marcelo Nazareth Aguirre. All Rights Reserved.

---

*Built with Python · FastAPI · SQLAlchemy · SQLite · HTML · CSS · JavaScript · PyWebView · PyInstaller*

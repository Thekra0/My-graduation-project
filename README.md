# Secure Payment Gateway Integration

> Final Graduate Project — Information Security (ISEC 470)
> A security-focused, full-stack payment gateway integration built and tested within the **PayPal Sandbox** environment.

## 📌 Overview

The rapid growth of e-commerce has increased the demand for secure, reliable, and user-friendly online payment systems. Many small and medium-scale platforms struggle to implement effective security controls due to limited resources and the absence of structured security frameworks.

This project presents the design and implementation of a **secure payment gateway integration system**, developed as a web application operating within the PayPal Sandbox environment. Rather than claiming full regulatory compliance, the project adopts recognized standards — **PCI-DSS**, **OWASP ASVS**, and the **NIST Cybersecurity Framework** — as guiding references throughout the design and development process.

The system follows a complete software engineering lifecycle: feasibility analysis, requirements gathering (including a user/merchant survey), functional/structural/behavioral modeling, architectural design, secure implementation, and testing.

## 🔐 Key Security Features

- **JWT-based authentication** for stateless, controlled session management
- **Secure password hashing** with bcrypt (no plaintext credential storage)
- **TLS/HTTPS-encrypted communication** between client and server
- **Verified PayPal webhook signature handling** to prevent forged/replayed payment notifications
- **Rate limiting & hardened HTTP headers** (Helmet.js, CORS configuration)
- **Server-side input validation** to mitigate injection-based attacks
- **Continuous dependency auditing** for known vulnerabilities

## 🏗️ Architecture

The system follows a **modular monolithic architecture**, built with **Node.js / Express.js** on the backend, separating concerns into distinct service modules:

| Module | Responsibility |
|---|---|
| `AuthService` | User registration, login, JWT issuance & verification |
| `PaymentService` | Order creation, payment capture, webhook verification |
| `PayPalAPI` | Integration layer with PayPal Sandbox (access tokens, order/capture calls) |

### Class Diagram
![Class Diagram](images/class_diagram.png)

### Use-Case Diagram
![Use-Case Diagram](images/usecase_diagram.png)

## 🔄 System Behavior (Sequence Diagrams)

**User Login Flow** — credential submission through JWT issuance:
![User Login Sequence](images/seq_login.png)

**Payment Order Creation** — authenticated user initiating a PayPal Sandbox order:
![Payment Order Creation Sequence](images/seq_payment_order.png)

**Payment Capture & Webhook Handling** — asynchronous, signature-verified webhook processing:
![Payment Capture and Webhook Handling Sequence](images/seq_webhook.png)

## 🖥️ User Interface

| Shopping Cart Review | Account Verification |
|---|---|
| ![Shopping Cart](images/ui_cart_multi.png) | ![Account Creation](images/ui_account_create.png) |

| Sign-In | Payment Result |
|---|---|
| ![Sign In](images/ui_signin.png) | ![Payment Authorized](images/ui_payment_success.png) |

**Failed transactions are also clearly communicated to the user:**
![Payment Failure](images/ui_payment_failure.png)

## 🧱 Tech Stack

- **Backend:** Node.js, Express.js, Sequelize (PostgreSQL)
- **Authentication:** JWT, bcrypt password hashing
- **Payments:** PayPal Sandbox API (orders, capture, webhooks)
- **Security Middleware:** Helmet.js, CORS, express-rate-limit
- **Transport Security:** HTTPS/TLS (local development certificates)
- **Testing:** Jest, Supertest
- **Frontend:** Vanilla HTML/JS

## 📁 Repository Structure

```
.
├── backend/
│   ├── config/         # DB & PayPal configuration
│   ├── controllers/     # Auth, payment, webhook controllers
│   ├── middleware/       # Auth guard, rate limiter, logger
│   ├── models/           # Sequelize models (User, Transaction)
│   ├── routes/            # Express routes
│   ├── services/           # PayPal & transaction business logic
│   ├── scripts/             # DB backup/restore scripts
│   ├── tests/                # Jest test suites (injection, payment, webhook)
│   ├── docs/                  # Security framework mapping (PCI-DSS, OWASP ASVS, NIST CSF)
│   ├── server.js
│   ├── package.json
│   └── .env.example
├── frontend/
│   ├── index.html
│   └── app.js
├── images/              # Diagrams & UI screenshots used in this README
├── Final_Graduate_Report.pdf
└── README.md
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v18+)
- PostgreSQL
- A PayPal Developer Sandbox account ([developer.paypal.com](https://developer.paypal.com))

### Setup

```bash
# 1. Clone the repo
git clone https://github.com/<your-username>/secure-payment-gateway-integration.git
cd secure-payment-gateway-integration/backend

# 2. Install dependencies
npm install

# 3. Configure environment variables
cp .env.example .env
# then edit .env with your own DATABASE_URL, JWT_SECRET, and PayPal Sandbox credentials

# 4. Run the server
npm run dev
```

The frontend (`frontend/index.html`) can be served with any static server (e.g. VS Code Live Server) and points to `https://localhost:5000/api` by default — update `API_BASE` in `frontend/app.js` if your backend runs elsewhere.

> ⚠️ **Never commit your real `.env` file or PayPal credentials.** The `.gitignore` in this repo already excludes `.env`, certificates, and `node_modules`.

## 📚 Methodology

The project was developed using a structured software engineering process:

1. **Problem Domain & Feasibility Analysis** — risk identification across encryption, authentication, input validation, and webhook handling
2. **Requirements Analysis** — including a user & merchant survey to capture usability and security expectations
3. **Modeling** — use-case, class, and sequence diagrams
4. **UI/UX Design** — following usability heuristics (error recovery, minimalist design, help & documentation)
5. **Architectural Design** — modular monolithic backend with clear security-control mapping
6. **Implementation** — secure coding practices mapped to OWASP ASVS / PCI-DSS guidance
7. **Testing & Validation** — functional and security-oriented testing (see `backend/tests/`), with documented limitations and recommendations for future work

## 🎓 Learning Outcomes

- Applying secure web development practices in a real integration context
- Analyzing cybersecurity risks specific to online payment systems
- Evaluating security posture through structured testing
- Implementing secure, verified integration with a third-party payment provider (PayPal)

## 📄 Full Report

The complete final graduate report — including detailed risk analysis, requirements documentation, full architectural design, code listings, and testing results — is available here: [`Final_Graduate_Report.pdf`](./Final_Graduate_Report.pdf)

Additional security-framework mapping documents (PCI-DSS, OWASP ASVS, NIST CSF, Secure SDLC, backup/restore procedure, version control) are available in [`backend/docs`](./backend/docs).

## 👥 Team

| Name | ID |
|---|---|
| Tmader Salem | 202100640 |
| Munirah Hamoud Alshammari | 20220542 |
| Shahd Saad Alharbi | 202204322 |
| Wafa Mohammed | 202100971 |
| Shatha Abdulrahman | 202202964 |
| Deema Khaled Almoka | 202100256 |
| Thikra Yousef Alsalhani | 202200150 |

**Supervisor:** Dr. Maha Al-Qanun

---
*This project was developed for educational purposes as part of the Information Security program (ISEC 470) and operates entirely within the PayPal Sandbox test environment. It does not claim production-level security or regulatory compliance.*

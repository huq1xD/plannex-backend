# PlanNex Backend

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

RESTful API backend for **PlanNex** — an online task management platform inspired by Trello. Built with Node.js, Express, Prisma ORM, and Socket.IO.

---

## ✨ Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Framework | Express.js |
| Database | PostgreSQL + Prisma ORM |
| Authentication | JWT (Access + Refresh Token) |
| Real-time | Socket.IO |
| Email | Nodemailer (Gmail SMTP) |
| OAuth | Google OAuth 2.0 |
| Payment | VNPay (Sandbox) |

---

## 🏗️ Architecture
```
/src
├── /controllers   # Xử lý HTTP request, trả response
├── /services      # Business logic
├── /routes        # Định nghĩa API endpoints
├── /middleware    # Auth (JWT), error handling
├── /validators    # Validate request body
├── /sockets       # Real-time với Socket.IO
└── /shared        # Prisma client và các module dùng chung
```

**Data Flow:**

`Client → Express API → Middleware (Auth, Validate) → Controller → Service → Prisma → PostgreSQL`

---

## ⚙️ Installation & Setup

**Prerequisites:**
- Node.js v18+
- PostgreSQL
- ngrok (để test VNPay IPN ở local)

**1. Clone repo:**
```bash
git clone https://github.com/huq1xD/plannex-backend.git
cd plannex-backend
```

**2. Cài dependencies:**
```bash
npm install
```

**3. Setup environment variables:**
```bash
cp .env.example .env
```
Mở file `.env` và điền các giá trị thật (xem hướng dẫn trong `.env.example`).

**4. Chạy migration database:**
```bash
npx prisma migrate dev
```

**5. Chạy server:**
```bash
npm start
```
Server chạy tại `http://localhost:3000`

---

## 🔑 Environment Variables

Xem file [`.env.example`](./.env.example) để biết danh sách đầy đủ. Các service cần tự đăng ký:

| Service | Đăng ký tại |
|---|---|
| Google OAuth | https://console.cloud.google.com |
| VNPay Sandbox | https://sandbox.vnpayment.vn/devreg |
| Gmail App Password | https://myaccount.google.com/apppasswords |
| ngrok (VNPay IPN) | https://ngrok.com |

---

## 📡 API Endpoints

> Base URL: `http://localhost:3000`

| Method | Endpoint | Mô tả |
|---|---|---|
| POST | `/auth/register` | Đăng ký tài khoản |
| POST | `/auth/login` | Đăng nhập |
| GET | `/auth/google` | Đăng nhập bằng Google |
| POST | `/payment/vnpay` | Tạo link thanh toán VNPay |
| GET | `/payment/vnpay-return` | VNPay callback |



---
title: Arsitektur Aplikasi
navigation: true
---

# 🏗️ Arsitektur Aplikasi Mlijo

Mlijo adalah platform langganan sayur berbasis lokasi yang menghubungkan pembeli dan tukang sayur secara langsung dengan fitur sosial login, membership, dan sistem poin loyalitas.

---

## 🧱 Struktur Layer Aplikasi

Client (Web / Mobile)
↓
API Gateway (Express.js)
↓
Controller Layer
↓
Service Layer (Business Logic)
↓
Repository Layer (Prisma ORM)
↓
Database (PostgreSQL)

---

## 🛠️ Teknologi yang Digunakan

| Layer                  | Teknologi                           |
| ---------------------- | ----------------------------------- |
| Frontend (Opsional)    | React / React Native                |
| Backend API            | Node.js + Express.js                |
| ORM & DB Access        | Prisma ORM                          |
| Database               | PostgreSQL                          |
| Autentikasi            | OAuth2 (Google/Facebook)            |
| Lokasi                 | Geolocation API, GeoHash, Haversine |
| Deployment             | Railway / Render / Vercel           |
| File Upload (opsional) | Cloudinary / Supabase Storage       |

---

## 📦 Struktur Folder Backend

📁 src
┣ 📁 controllers -> Request handler untuk routing API
┣ 📁 services -> Business logic
┣ 📁 repositories -> Prisma query wrapper
┣ 📁 middlewares -> Auth, logger, error handler
┣ 📁 routes -> Semua endpoint API
┣ 📁 utils -> Helper (geo calc, jwt, etc)
┣ 📁 prisma -> Prisma schema & migrations
┣ 📄 server.ts -> Entry point server

---

## 🧩 Modul Utama

### 1. 🔐 Auth Module

- Login dengan Google/Facebook
- JWT issuance
- Middleware autentikasi & otorisasi

### 2. 👥 User & Profile Module

- CRUD user
- Update lokasi & profil
- Verifikasi akun (membership)

### 3. 🥬 Vegetable Module

- CRUD produk sayur oleh penjual
- Filter & search produk

### 4. 🛒 Order Module

- Pemesanan oleh pembeli
- Riwayat transaksi
- Total harga & status

### 5. 📍 Nearby Seller Module

- Perhitungan jarak Haversine
- Radius pencarian penjual (misal: 3 km)
- Sorting berdasarkan rating atau stok

### 6. 🤝 Membership Module

- Hubungan 1:1 antara pembeli & tukang sayur
- Verifikasi keanggotaan

### 7. 🎁 Loyalty Point Module

- Akumulasi poin berdasarkan pesanan
- Sistem reward poin

---

## 🔄 Alur Data (Contoh Order)

[Client] -> POST /api/orders
-> controller.order.create
-> service.order.createOrder
-> repository.order.create
-> Prisma insert to DB
<- response { orderId, total, status }

---

## 🔍 Skema Deployment (Sederhana)

Client Web/App
↓
Vercel / Expo / Netlify

Backend API
↓
Render / Railway / Fly.io

Database
↓
PostgreSQL

CDN/Storage (opsional)
↓
Cloudinary / Supabase Storage

---

## ✅ Keamanan

- Autentikasi JWT
- Rate limiting API
- Validasi input dengan Zod/Joi
- CORS whitelist
- Prisma query sanitization

---

## 🧪 Testing & CI/CD

- Unit test dengan Vitest / Jest
- E2E test (Supertest / Postman)
- GitHub Actions untuk lint, test, deploy

---

## 📚 Referensi Tambahan

- [`schema.prisma`](./prisma/schema.prisma)
- [`docs/api.md`](./docs/api.md)
- [`docs/database.md`](./docs/database.md)

---

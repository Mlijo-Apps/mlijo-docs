---
title: Autentikasi
navigation: true
---

# Endpoint Autentikasi

## `POST /api/auth/login`

Login pengguna menggunakan email dan password.

**Request:**
```json
{
  "email": "user@email.com",
  "password": "******"
}
```

**Response:**
```json
{
  "token": "jwt-token"
}
```

---

## `POST /api/auth/register`

Registrasi pengguna baru.
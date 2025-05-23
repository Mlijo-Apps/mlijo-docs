---
title: 🔄 Flow & ERD Mlijo
navigation: true
---

Dokumen ini menjelaskan alur pengguna dalam aplikasi dan relasi antar entitas pada database menggunakan Prisma + PostgreSQL.

---

## 🔁 Flow Pengguna (User Journey)

### 1. 🔐 Registrasi & Login

- Pengguna membuka aplikasi
- Klik “Login dengan Google”
- Backend memverifikasi token OAuth
- Jika pengguna baru → data disimpan di tabel `User`
- Redirect ke dashboard pembeli / penjual

### 2. 🛍️ Pembeli Menemukan Penjual

- Berdasarkan lokasi (`Profile.latitude` & `longitude`)
- Backend menghitung penjual terdekat dengan Haversine formula
- Pembeli memilih penjual untuk dijadikan langganan

### 3. 🤝 Membuat Langganan (Membership)

- Pembeli klik “Langganan” ke penjual A
- Backend menyimpan relasi ke tabel `Membership`
- Pembeli sekarang bisa memesan ke penjual A

### 4. 🥬 Pesan Sayur

- Pembeli memilih produk dari daftar `Vegetable` milik penjual
- Tambahkan ke keranjang, kirim `POST /orders`
- Data masuk ke tabel `Order` dan `OrderItem`

### 5. 🎁 Dapatkan Poin

- Setelah pesanan sukses, backend menambahkan poin loyalitas ke `LoyaltyPoint`

---

## 🧩 ERD (Entity Relationship Diagram)

┌────────────┐ 1 ┌────────────┐
│ User │──────────────▶│ Profile │
│────────────│ └────────────┘
│ id (PK) │
│ email │
│ name │
│ role │
└────┬───────┘
│
│1
▼
┌────────────┐
│ Vegetable │◀──────────────┐
│────────────│ │
│ id (PK) │ │
│ name │ │
│ price │ │
│ sellerId │──────────────▶│ User (SELLER)
└────────────┘ │
│
┌───────────────────────────┘
│
│1 N
▼ ▼
┌────────────┐ ┌────────────┐
│ Membership │ │ Order │
│────────────│ │────────────│
│ id (PK) │ │ id (PK) │
│ buyerId │ │ buyerId │
│ sellerId │ │ sellerId │
└────┬───────┘ │ totalPrice │
│ └────┬───────┘
│1 │1
▼ ▼
┌────────────┐ ┌────────────┐
│ Loyalty │ │ OrderItem │
│ Point │ │────────────│
│────────────│ │ id (PK) │
│ userId │ │ orderId │
│ points │ │ vegetableId│
└────────────┘ └────────────┘

---

## 📘 Tabel Inti

| Tabel          | Fungsi                                      |
| -------------- | ------------------------------------------- |
| `User`         | Data user login (pembeli & tukang sayur)    |
| `Profile`      | Lokasi & data tambahan user                 |
| `Vegetable`    | Produk sayur yang dijual                    |
| `Membership`   | Relasi langganan antara pembeli dan penjual |
| `Order`        | Transaksi pemesanan sayur                   |
| `OrderItem`    | Detail isi pesanan                          |
| `LoyaltyPoint` | Riwayat dan saldo poin pelanggan            |

---

## 📎 Catatan

- Role user dibedakan di field `User.role` → `BUYER` atau `SELLER`
- Fungsi lokasi menggunakan `latitude` dan `longitude` dari `Profile`
- Setiap relasi memiliki foreign key yang terhubung dengan baik

---

# Library Borrowing API

REST API sederhana untuk layanan pencatatan peminjaman buku perpustakaan. Dibangun menggunakan Node.js, Express.js, dan Supabase.

## Deskripsi Umum & Tujuan Proyek
Proyek ini dibuat untuk memenuhi tugas responsi Modul 1. Tujuannya adalah membangun layanan *backend* (API) yang dapat melakukan operasi CRUD pada data peminjaman buku, memfilter berdasarkan status (contoh: `Terlambat`), serta men-deploy API ini agar dapat diakses publik melalui Vercel.

## Struktur Data (Schema Database)
Aplikasi ini menggunakan Supabase (PostgreSQL) dengan tabel `loans` sebagai berikut:
- `id` (uuid, primary key)
- `member_name` (text, not null)
- `book_title` (text, not null)
- `borrow_date` (date, not null, default: `current_date`)
- `return_date` (date, nullable)
- `status` (text, not null, default: `'Dipinjam'`)

## Contoh Request & Response

### 1. Menambahkan Peminjaman Baru
**Request:**
`POST /api/loans`
```json
{
  "member_name": "Laila Mutiara",
  "book_title": "Belajar PPB"
}
```
**Response (201 Created):**
```json
{
  "id": "abc-123-...",
  "member_name": "Laila Mutiara",
  "book_title": "Belajar PPB",
  "borrow_date": "2023-10-24",
  "return_date": null,
  "status": "Dipinjam"
}
```

### 2. Mengambil Semua Peminjaman (dengan Filter)
**Request:**
`GET /api/loans?status=Dipinjam`

**Response (200 OK):**
```json
[
  {
    "id": "abc-123-...",
    "member_name": "Laila Mutiara",
    "book_title": "Belajar PPB",
    "borrow_date": "2023-10-24",
    "return_date": null,
    "status": "Dipinjam"
  }
]
```

## Panduan Instalasi & Cara Menjalankan Lokal
1. Clone repository ini:
   ```bash
   git clone <url-repo-anda>
   cd perpustakaan-api
   ```
2. Instal dependensi:
   ```bash
   npm install
   ```
3. Setup Environment Variables:
   Ubah/buat file `.env` dan masukkan kredensial Supabase Anda.
   ```env
   SUPABASE_URL=url_supabase_anda
   SUPABASE_KEY=key_supabase_anda
   PORT=3000
   ```
4. Jalankan aplikasi:
   ```bash
   npm run dev
   ```
5. Akses API di `http://localhost:3000`.

## Link Hasil Deployment Vercel
[https://<nama-proyek-vercel-anda>.vercel.app](https://<nama-proyek-vercel-anda>.vercel.app)

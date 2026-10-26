# 📊 Student Grade Calculator

Aplikasi web untuk mengelola data mahasiswa, mata kuliah, dan penilaian akademik berbasis **Go (Golang)** dengan framework **Gin**. Frontend dibangun dengan HTML, CSS, dan JavaScript (jQuery) yang disajikan langsung oleh backend Go.

## 📁 Struktur Proyek

```
Tugas-Vibes-code/
├── go_vibe/
│   ├── cmd/
│   │   └── server/
│   │       └── main.go          # Titik entri aplikasi
│   ├── config/                  # Konfigurasi & koneksi database
│   ├── controllers/             # Controller (auth, student, course, grade, dashboard)
│   ├── middleware/              # Middleware (auth, CSRF, role)
│   ├── models/                  # Model data (user, student, course, grade)
│   ├── routes/
│   │   └── routes.go            # Routing API & halaman HTML
│   ├── services/                # Bisnis logic (perhitungan nilai)
│   ├── static/
│   │   ├── css/
│   │   │   └── style.css        # Styling aplikasi
│   │   └── js/
│   │       ├── main.js          # Helper global & autentikasi
│   │       ├── auth.js          # Login & register
│   │       ├── dashboard.js     # Data dashboard
│   │       ├── students.js      # Kelola data mahasiswa
│   │       ├── courses.js       # Kelola mata kuliah
│   │       └── grades.js        # Input & kelola nilai
│   ├── views/
│   │   ├── index.html           # Dashboard
│   │   ├── login.html           # Halaman login
│   │   ├── register.html        # Halaman pendaftaran
│   │   ├── students.html        # Data mahasiswa
│   │   ├── courses.html         # Data mata kuliah
│   │   └── grades.html          # Hasil & input nilai
│   ├── utils/                   # Utilitas (JWT, dll.)
│   ├── .env                     # Variabel lingkungan
│   ├── .env.example             # Contoh variabel lingkungan
│   ├── go.mod
│   └── go.sum
└── README.md
```

## 🚀 Cara Menjalankan

### Prasyarat
- [Go](https://golang.org/dl/) versi 1.21 atau lebih baru
- PostgreSQL (opsional, untuk penyimpanan data)

### Langkah-langkah

1. **Masuk ke direktori proyek Go**
   ```powershell
   cd "C:\Users\User\OneDrive\Documents\Pelatihan BLKPP\Tugas-Vibes-code\go_vibe"
   ```

2. **Pastikan file `.env` sudah ada**
   File `.env` sudah tersedia dengan konfigurasi default. Ubah `DATABASE_URL` jika menggunakan database lokal.

3. **Jalankan server**
   ```powershell
   go run ./cmd/server/
   ```

4. **Buka di browser**
   ```
   http://localhost:8080
   ```

> Port default adalah `8080` (dari `APP_PORT` di file `.env`).

## 🔐 Autentikasi & Role

Aplikasi memiliki 3 role pengguna:

| Role | Akses | Fitur Khusus |
|------|-------|--------------|
| **Mahasiswa** | Lihat data sendiri | Lihat nilai dan statistik pribadi |
| **Dosen** | Kelola data akademik | Tambah/edit/hapus mahasiswa, mata kuliah, dan nilai |
| **Admin** | Akses penuh | Sama seperti Dosen |

### Cara Membuat Akun
1. Buka `http://localhost:8080/register`
2. Isi formulir pendaftaran (pilih role: Mahasiswa, Dosen, atau Admin)
3. Klik **Daftar Akun**
4. Login di `http://localhost:8080/login`

## 📱 Halaman yang Tersedia

| Halaman | URL | Keterangan |
|---------|-----|------------|
| Dashboard | `/` | Ringkasan statistik & distribusi nilai |
| Login | `/login` | Masuk ke sistem |
| Register | `/register` | Daftar akun baru |
| Data Mahasiswa | `/students` | Kelola data mahasiswa (Dosen/Admin) |
| Data Mata Kuliah | `/courses` | Kelola mata kuliah (Dosen/Admin) |
| Hasil & Input Nilai | `/grades` | Input dan lihat penilaian (Dosen/Admin) |

## ⚙️ Konfigurasi (.env)

| Variabel | Deskripsi | Contoh |
|----------|-----------|--------|
| `APP_PORT` | Port server | `8080` |
| `DATABASE_URL` | Koneksi PostgreSQL | `postgres://user:pass@localhost:5432/db` |
| `JWT_SECRET` | Kunci rahasia JWT | `replace-with-random-secret` |
| `JWT_EXPIRES_in` | Masa berlaku token | `15m` |
| `COOKIE_SECURE` | Cookie hanya HTTPS | `false` (development) |
| `COOKIE_SAME_SITE` | Kebijakan same-site cookie | `lax` |

## 🧮 Rumus Penilaian

Nilai akhir dihitung secara otomatis oleh backend dengan bobot:

```
Nilai Akhir = (Tugas × 0.20) + (Kuis × 0.20) + (UTS × 0.25) + (UAS × 0.35)
```

Grade ditetapkan berdasarkan nilai akhir:

| Nilai | Grade | Predikat |
|-------|-------|----------|
| 85 – 100 | A | Sangat Baik |
| 80 – 84.99 | AB | Baik Sekali |
| 75 – 79.99 | B | Baik |
| 70 – 74.99 | BC | Cukup Baik |
| 65 – 69.99 | C | Cukup |
| 50 – 64.99 | D | Kurang |
| 0 – 49.99 | E | Sangat Kurang |

## 🛠️ Teknologi yang Digunakan

- **Backend:** Go 1.27.1, Gin Framework, GORM, PostgreSQL
- **Frontend:** HTML5, CSS3, JavaScript (jQuery 3.7.1)
- **Autentikasi:** JWT (HttpOnly Cookie)
- **Keamanan:** CSRF Protection (Double Submit Cookie)

## 📦 Build (Opsional)

Untuk menghasilkan binary executable:

```powershell
go build -o bin/server ./cmd/server/
.\bin\server
```

## 👥 Kontribusi

Proyek ini dibuat sebagai bagian dari tugas pelatihan. Silakan kembangkan dan sesuaikan sesuai kebutuhan.

---

**© 2026 Student Grade Calculator — Pelatihan BLKPP**
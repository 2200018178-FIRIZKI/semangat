# Proyek Backend - SEMUA RIZKI

## Deskripsi Singkat

Proyek ini adalah backend API untuk aplikasi "SEMUA RIZKI" yang bertujuan untuk menyediakan fungsionalitas manajemen konten, kategori, klasifikasi otomatis, manajemen target/konsep, analisis, rekomendasi, serta autentikasi pengguna.

## Fitur Utama

* **Manajemen Kategori & Klasifikasi:**
    * Pembuatan, penampilan, dan pembaruan kategori.
    * Dukungan untuk hierarki kategori (parent-child).
    * (Rencana) Klasifikasi otomatis konten teks menggunakan Machine Learning/NLP.
* **Manajemen Data & Konten:**
    * Upload konten (gambar, teks, dll.).
    * Filter konten berdasarkan kategori.
    * Pembaruan metadata konten (misalnya, tags).
* **Analisis & Rekomendasi:**
    * (Rencana) Statistik kategori populer.
    * (Rencana) Rekomendasi konten berdasarkan histori pengguna.
* **Manajemen Target & Konsep:**
    * Pembuatan target/konsep (misalnya, "Teknogene").
    * Pemantauan progres pencapaian target.
* **Sistem File & Kualitas:**
    * Upload file dengan validasi kualitas.
    * Pengecekan metrik kualitas file.
* **Autentikasi & Keamanan:**
    * Registrasi dan login pengguna.
    * Penggunaan JSON Web Tokens (JWT) untuk otorisasi.

## Teknologi yang Digunakan

* **Bahasa Pemrograman:** Python 3.x
* **Framework:** Flask
* **Database:** PostgreSQL
* **ORM:** Flask-SQLAlchemy
* **Migrasi Database:** Flask-Migrate (Alembic)
* **Autentikasi:** Flask-JWT-Extended
* **Validasi & Serialisasi:** (Rencana) Marshmallow atau Pydantic
* **Machine Learning (Rencana):** Scikit-learn, TensorFlow, atau library Python lainnya.
* **Penyimpanan File (Rencana):** Penyimpanan cloud (misalnya AWS S3, Google Cloud Storage).

## Prasyarat

Sebelum memulai, pastikan Anda telah menginstal:

* Python (versi 3.8 atau lebih baru direkomendasikan)
* pip (Python package installer)
* PostgreSQL (server database)
* Git (sistem kontrol versi)
* pgAdmin4 atau DBeaver (atau tool manajemen database PostgreSQL lainnya, opsional)

## Panduan Setup dan Instalasi Lokal

1.  **Clone Repository:**
    ```bash
    git clone <URL_REPOSITORY_ANDA>
    cd semua_rizki_backend
    ```

2.  **Buat dan Aktifkan Virtual Environment:**
    ```bash
    # Windows
    python -m venv venv
    .\venv\Scripts\activate

    # macOS/Linux
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Install Dependensi:**
    Pastikan virtual environment Anda aktif, lalu install semua dependensi yang dibutuhkan dari file `requirements.txt`:
    ```bash
    pip install -r requirements.txt
    ```

4.  **Konfigurasi Variabel Lingkungan:**
    * Salin file `.env.example` (jika ada) menjadi `.env` atau buat file `.env` baru di root folder proyek.
    * Isi file `.env` dengan konfigurasi yang sesuai. Contoh minimal:
        ```env
        # .env
        FLASK_APP=run.py
        FLASK_ENV=development
        SECRET_KEY='GANTI_DENGAN_KUNCI_RAHASIA_ANDA_YANG_KUAT'
        SQLALCHEMY_DATABASE_URI='postgresql://USER:PASSWORD@HOST:PORT/DATABASE_NAME' # Sesuaikan!
        JWT_SECRET_KEY='GANTI_DENGAN_KUNCI_JWT_RAHASIA_ANDA_YANG_KUAT'
        ```
        **Penting:** Ganti `USER`, `PASSWORD`, `HOST`, `PORT`, dan `DATABASE_NAME` dengan detail koneksi PostgreSQL Anda. `SECRET_KEY` dan `JWT_SECRET_KEY` juga harus diisi dengan nilai acak yang kuat dan unik.

5.  **Setup Database:**
    * Pastikan server PostgreSQL Anda berjalan.
    * Buat database baru di PostgreSQL untuk proyek ini (misalnya, `semuarizki_db`) jika belum ada.
    * **Catatan:** Anda telah membuat tabel-tabel secara manual melalui pgAdmin4. Pastikan model SQLAlchemy yang akan Anda buat di `app/models/` **sesuai persis** dengan skema tabel yang sudah ada tersebut.

6.  **Inisialisasi dan Jalankan Migrasi Database dengan Flask-Migrate:**
    Flask-Migrate (Alembic) akan digunakan untuk mengelola perubahan skema database di masa mendatang.
    ```bash
    # Set FLASK_APP jika belum (di PowerShell, contoh)
    # $env:FLASK_APP = "run.py"
    # atau pastikan sudah ada di .flaskenv

    # Inisialisasi folder migrations (hanya sekali per proyek jika belum ada)
    flask db init

    # Buat file migrasi awal.
    # Karena tabel sudah ada, ini akan mencoba mencocokkan model dengan DB.
    # Pastikan model SQLAlchemy Anda sudah dibuat dan sesuai dengan DB.
    flask db migrate -m "Initial setup, tables created manually."

    # Terapkan migrasi ke database (ini akan membuat tabel alembic_version
    # dan mencatat revisi saat ini jika tabel sudah cocok dengan model)
    flask db upgrade
    ```
    Jika `flask db migrate` menghasilkan perubahan skema yang tidak diinginkan, periksa kembali definisi model SQLAlchemy Anda agar sesuai dengan tabel yang ada di database.

## Menjalankan Aplikasi

Setelah semua setup selesai, jalankan server development Flask:

```bash
flask run atau python run.py

Aplikasi akan berjalan secara default di http://127.0.0.1:5000/

1
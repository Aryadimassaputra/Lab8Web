# Lab8Web – Praktikum 8: PHP dan Database MySQL

**Nama:** _isi nama_  
**NIM:** _isi NIM_  
**Kelas:** _isi kelas_

Aplikasi CRUD sederhana untuk data barang menggunakan PHP + MySQL (XAMPP).

## Struktur Folder
```
lab8_php_database/
├── gambar/          (folder penyimpanan gambar barang)
├── database.sql
├── koneksi.php
├── index.php        (Read)
├── tambah.php       (Create)
├── ubah.php         (Update)
├── hapus.php        (Delete)
└── style.css
```

## 1. Persiapan – Menjalankan MySQL Server
Buka **XAMPP Control Panel**, klik **Start** pada modul **Apache** dan **MySQL**.

> Screenshot: `screenshots/01_xampp.png`

## 2. Mengakses phpMyAdmin
Buka `http://localhost/phpmyadmin/` di browser.

> Screenshot: `screenshots/02_phpmyadmin.png`

## 3. Membuat Database dan Tabel
Jalankan perintah SQL pada tab **SQL** (isi lengkap ada di `database.sql`):

```sql
CREATE DATABASE latihan1;

CREATE TABLE data_barang (
  id_barang int(10) auto_increment Primary Key,
  kategori varchar(30),
  nama varchar(30),
  gambar varchar(100),
  harga_beli decimal(10,0),
  harga_jual decimal(10,0),
  stok int(4)
);
```

> Screenshot: `screenshots/03_create_table.png`

## 4. Menambahkan Data Awal
```sql
INSERT INTO data_barang (kategori, nama, gambar, harga_beli, harga_jual, stok)
VALUES ('Elektronik', 'HP Samsung Android', 'hp_samsung.jpg', 2000000, 2400000, 5),
('Elektronik', 'HP Xiaomi Android', 'hp_xiaomi.jpg', 1000000, 1400000, 5),
('Elektronik', 'HP OPPO Android', 'hp_oppo.jpg', 1800000, 2300000, 5);
```

> Screenshot: `screenshots/04_select_data.png`

## 5. Membuat Folder Project
Buat folder `lab8_php_database` di `C:\xampp\htdocs\` (atau `d:\xampp\htdocs\`), lalu akses di `http://localhost/lab8_php_database/`.

> Screenshot: `screenshots/05_folder.png`

## 6. File Koneksi Database (`koneksi.php`)
Menghubungkan PHP ke MySQL memakai `mysqli_connect()`. Jika gagal, tampil pesan "Koneksi ke server gagal." Untuk mengetes, hilangkan komentar `#else echo "Koneksi berhasil";`.

> Screenshot: `screenshots/06_koneksi.png`

## 7. Menampilkan Data – Read (`index.php`)
Mengambil semua data dengan `SELECT * FROM data_barang`, lalu menampilkannya dalam tabel menggunakan `while` + `mysqli_fetch_array()`. Kolom **Aksi** berisi link Ubah dan Hapus; ada link **Tambah Barang** di atas tabel.

> Screenshot: `screenshots/07_index.png`

## 8. Menambah Data – Create (`tambah.php`)
Form (method POST, `enctype="multipart/form-data"`) berisi nama, kategori, harga jual, harga beli, stok, dan file gambar. Saat disubmit, gambar dipindah ke folder `gambar/` dengan `move_uploaded_file()`, lalu data disimpan dengan `INSERT INTO`, kemudian redirect ke `index.php`.

> Screenshot: `screenshots/08_tambah.png`

## 9. Mengubah Data – Update (`ubah.php`)
Data diambil berdasarkan `id` dari URL (`ubah.php?id=1`) dan ditampilkan pada form. Saat disimpan dijalankan `UPDATE data_barang SET ... WHERE id_barang = ...` (gambar hanya diganti jika ada file baru).

> Screenshot: `screenshots/09_ubah.png`

## 10. Menghapus Data – Delete (`hapus.php`)
Menjalankan `DELETE FROM data_barang WHERE id_barang = ...` berdasarkan `id` dari URL, lalu kembali ke `index.php`.

> Screenshot: `screenshots/10_hapus.png`

## Catatan Perbaikan dari Modul
- Kolom **Aksi** di `index.php` diperbaiki menjadi link Ubah/Hapus (di modul hanya menampilkan id_barang).
- Urutan kolom Harga Jual / Harga Beli di `index.php` disesuaikan dengan datanya.
- `is_select()` di `ubah.php` diperbaiki agar kategori yang tampil sesuai data.
- `enctype="multipart/form-data"` ditulis lengkap (di modul terpotong jadi `formdata`).
- Path gambar disimpan sebagai nama file saja, agar `gambar/` tidak ganda.
- Input diamankan (`mysqli_real_escape_string` / `(int)`) terhadap SQL injection.

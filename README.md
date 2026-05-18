# DATABASE MYSQL 

---

## PERINTAH DASAR DATABASE

```sql
SHOW DATABASES;              -- lihat semua database
CREATE DATABASE nama_db;     -- buat database baru
USE nama_db;                 -- pilih database
DROP DATABASE nama_db;       -- hapus database (permanent)
```

---

## TIPE DATA

### Number
| Tipe Data | Ukuran |
|-----------|--------|
| TINYINT | 1 byte |
| SMALLINT | 2 bytes |
| MEDIUMINT | 3 bytes |
| INT | 4 bytes |
| BIGINT | 8 bytes |

> `UNSIGNED` = hanya bilangan positif (mulai dari 0)

### Decimal
| Tipe | Contoh Nilai |
|------|-------------|
| DECIMAL(5,2) | 999.99 |
| DECIMAL(5,3) | 99.999 |

Format: `DECIMAL(total_digit, digit_dibelakang_koma)`

### Teks
| Tipe | Keterangan |
|------|------------|
| CHAR(n) | teks fixed length |
| VARCHAR(n) | teks max n karakter |
| TEXT | teks panjang |

### Lainnya
| Tipe | Keterangan |
|------|------------|
| DATE | format: YYYY-MM-DD |
| DATETIME | format: YYYY-MM-DD HH:MM:SS |
| BOOLEAN | TRUE / FALSE |

---

## DDL — Data Definition Language
> Perintah untuk mengatur **struktur** database/tabel

### CREATE TABLE
```sql
CREATE TABLE nama_tbl (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nama VARCHAR(100),
  harga DECIMAL(10,2),
  stok INT
) ENGINE = InnoDB;
```

### Lihat Struktur Tabel
```sql
SHOW TABLES;                       -- lihat semua tabel
DESC nama_tbl;                     -- lihat struktur tabel
SHOW CREATE TABLE nama_tbl;        -- lihat syntax pembuatan tabel
```

### ALTER TABLE
```sql
ALTER TABLE nama_tbl ADD COLUMN nama_col TEXT;          -- tambah kolom
ALTER TABLE nama_tbl DROP COLUMN nama_col;              -- hapus kolom
ALTER TABLE nama_tbl RENAME COLUMN lama TO baru;        -- rename kolom
ALTER TABLE nama_tbl MODIFY nama VARCHAR(30) AFTER id;  -- ubah tipe/posisi kolom
```

### Hapus Tabel
```sql
TRUNCATE nama_tbl;   -- hapus semua isi tabel (tabel tetap ada)
DROP nama_tbl;       -- hapus tabel permanent
```

> **Bedanya TRUNCATE vs DROP:**
> - `TRUNCATE` = mejanya kosong, tapi masih ada
> - `DROP` = mejanya dibuang sekalian

---

## DML — Data Manipulation Language
> Perintah untuk mengatur **isi** tabel

### INSERT — Memasukkan Data
```sql
-- 1 baris
INSERT INTO nama_tbl (kolom1, kolom2) VALUES (nilai1, nilai2);

-- Lebih dari 1 baris
INSERT INTO nama_tbl (kolom1, kolom2) VALUES
  (nilai1, nilai2),
  (nilai3, nilai4);
```

### SELECT — Mengambil Data
```sql
SELECT * FROM nama_tbl;                        -- semua kolom
SELECT kolom1, kolom2 FROM nama_tbl;           -- kolom tertentu
SELECT * FROM nama_tbl WHERE kolom = nilai;    -- dengan kondisi
SELECT * FROM nama_tbl ORDER BY kolom ASC;     -- urut naik
SELECT * FROM nama_tbl ORDER BY kolom DESC;    -- urut turun
SELECT * FROM nama_tbl LIMIT 5;               -- batasi hasil
```

### UPDATE — Mengubah Data
```sql
UPDATE nama_tbl SET kolom1 = nilai_baru WHERE id = 1;
```
> Selalu pakai `WHERE` saat UPDATE, kalau tidak semua baris akan berubah!

### DELETE — Menghapus Data
```sql
DELETE FROM nama_tbl WHERE id = 1;
```
> Selalu pakai `WHERE` saat DELETE, kalau tidak semua data akan terhapus!

---

## CONSTRAINT
```sql
PRIMARY KEY     -- identitas unik tiap baris
FOREIGN KEY     -- relasi antar tabel
NOT NULL        -- kolom wajib diisi
UNIQUE          -- nilai tidak boleh sama
AUTO_INCREMENT  -- angka otomatis naik
DEFAULT         -- nilai default kalau tidak diisi
```

---

## OPERATOR

### Perbandingan
```sql
=   != atau <>   >   <   >=   <=
```

### Logika
```sql
AND   OR   NOT
```

### Lainnya
```sql
BETWEEN nilai1 AND nilai2    -- antara dua nilai
IN (nilai1, nilai2)          -- salah satu dari daftar
LIKE '%kata%'                -- pencarian teks
IS NULL                      -- nilai kosong
```

---

## JOIN — Menggabungkan Tabel
```sql
-- INNER JOIN: data yang cocok di kedua tabel
SELECT * FROM tabel1
INNER JOIN tabel2 ON tabel1.id = tabel2.id;

-- LEFT JOIN: semua data tabel kiri + yang cocok dari kanan
SELECT * FROM tabel1
LEFT JOIN tabel2 ON tabel1.id = tabel2.id;

-- RIGHT JOIN: semua data tabel kanan + yang cocok dari kiri
SELECT * FROM tabel1
RIGHT JOIN tabel2 ON tabel1.id = tabel2.id;
```

---

## AGGREGATE FUNCTION
```sql
COUNT(*)         -- hitung jumlah baris
SUM(kolom)       -- total nilai
AVG(kolom)       -- rata-rata
MAX(kolom)       -- nilai terbesar
MIN(kolom)       -- nilai terkecil
```

Contoh:
```sql
SELECT COUNT(*) FROM produk;
SELECT AVG(harga) FROM produk;
SELECT MAX(harga) FROM produk WHERE kategori = 'elektronik';
```

---

## GROUP BY & HAVING
```sql
-- Kelompokkan data
SELECT kategori, COUNT(*) FROM produk GROUP BY kategori;

-- Filter setelah GROUP BY (pakai HAVING, bukan WHERE)
SELECT kategori, COUNT(*) FROM produk
GROUP BY kategori
HAVING COUNT(*) > 5;
```

---

*Made by sahla-amanah 🌿*

**📌 Materi:**
- Recap: `INNER JOIN`, `LEFT JOIN`
- Tambahan:
  - `RIGHT JOIN`, `FULL OUTER JOIN`
  - `SELF JOIN` (contoh: hierarki organisasi)
  - Perbedaan `ON` vs `USING`
---
### 🔹 INNER JOIN
Mengembalikan hanya baris yang cocok **di kedua tabel**.
```sql
SELECT * FROM foo INNER JOIN bar ON foo.id = bar.id;
```
✅ Hanya data yang cocok di kedua tabel yang ditampilkan.
### 🔹 LEFT JOIN (atau LEFT OUTER JOIN)
Mengembalikan semua baris dari tabel kiri, dan data dari tabel kanan jika cocok. Jika tidak cocok, akan bernilai `NULL`.
```sql
SELECT * FROM foo LEFT JOIN bar ON foo.id = bar.id;
```
✅ Selalu tampilkan semua data dari kiri, kanan boleh `NULL`.
### 🔹 RIGHT JOIN (atau RIGHT OUTER JOIN)
Kebalikan dari LEFT JOIN. Mengembalikan semua baris dari **tabel kanan**, dan data dari kiri jika cocok.
```sql
SELECT * FROM foo RIGHT JOIN bar ON foo.id = bar.id;
```
✅ Selalu tampilkan semua data dari kanan, kiri boleh `NULL`.
### 🔹 FULL OUTER JOIN
Menggabungkan hasil dari LEFT dan RIGHT JOIN. Semua baris dari kedua tabel dikembalikan, cocok atau tidak.
```sql
SELECT * FROM foo FULL OUTER JOIN bar ON foo.id = bar.id;
```
✅ Jika tidak cocok, sisi yang tidak ada pasangan akan `NULL`.
### 🔹 SELF JOIN
Digunakan untuk melakukan JOIN pada tabel itu sendiri. Contoh umum adalah struktur hierarki organisasi (bawahan vs atasan).
```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```
✅ Contoh: seorang karyawan (employee) dan manajernya (manager) dari tabel yang sama.
### 🔹 Perbedaan `ON` vs `USING`
#### ON
Digunakan ketika nama kolom **berbeda**.
```sql
SELECT * FROM a JOIN b ON a.kode = b.kode_b;
```
#### USING
Digunakan ketika nama kolom **sama** di kedua tabel.
```sql
SELECT * FROM a JOIN b ON a.kode = b.kode_b;
```
✅ lebih singkat, tapi hanya jika nama kolom sama di kedua tabel.

### 🛠️ Catatan Tambahan
 - `JOIN` sangat penting untuk menggabungkan data dari beberapa tabel.
 - Selalu pastikan relasi antar tabel jelas (foreign key / primary key).
 - Gunakan alias (`a`, `b`, `e`, `m`, dll) untuk meningkatkan keterbacaan query.

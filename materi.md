# PostgreSQL

Selamat datang di sesi lanjutan SQL! Dalam sesi ini, kamu akan mempelajari konsep-konsep SQL tingkat menengah hingga menengah+, lengkap dengan praktik langsung, tips optimisasi, dan mini project.

---

## 🕒 Struktur Sesi

| Sesi | Topik                             | Waktu      | Level     |
|------|-----------------------------------|------------|-----------|
| 1    | Recap Relasi & Join Lanjutan      | 20 menit   | Menengah  |
| 2    | Subquery & CTE                    | 30 menit   | Menengah  |
| 3    | Aggregation & Window Function     | 30 menit   | Menengah+ |
| 4    | Indexing, Performance, EXPLAIN    | 20 menit   | Menengah  |
| 5    | View, Function & Transaksi        | 30 menit   | Menengah+ |
| 6    | Mini Project: Inventory System    | 20 menit   | Menengah+ |
| 7    | Q&A / Debugging Session           | 10 menit   | Semua     |

---

## 📚 Detail Materi

### 🧩 1. Relasi Lanjutan & Advanced Join

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

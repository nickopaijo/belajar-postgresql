**📌 Materi:**
- Kapan dan kenapa pakai index
- Tipe index: B-Tree (default), Unique
- EXPLAIN ANALYZE
---
### 🔹 Kapan dan Kenapa Pakai Index
**Index** digunakan untuk mempercepat pencarian data (mirip daftar isi di buku).

Gunakan index jika:
 - Kolom sering digunakan di kondisi `WHERE`, `JOIN`, `ORDER BY`
 - Tabel besar, dan query menjadi lambat

Tanpa index, PostgreSQL harus melakukan sequential scan (baca semua baris satu per satu).

📌 Query tanpa index
```sql
SELECT * FROM customers WHERE name = 'Alice';
```
Jika kolom name tidak di-index, maka PostgreSQL akan baca seluruh tabel.

📌 Buat index di kolom `name`
```sql
CREATE INDEX idx_customers_name ON customers(name);
```
Setelah ini, query di atas akan jauh lebih cepat terutama kalau datanya besar.
### 🔹 Tipe Index: B-Tree (default), UNIQUE
B-Tree Index:
 - Default di PostgreSQL
 - Cocok untuk pencarian dengan `=`, `<`, `>`, `BETWEEN`, dll
```sql
CREATE INDEX idx_orders_total ON orders(total);
```
Index UNIQUE:
 - Menjamin tidak ada duplikasi
 - Otomatis dipakai untuk kolom `PRIMARY KEY`
```sql
CREATE UNIQUE INDEX idx_customers_unique_name ON customers(name);
```
Gagal insert jika ada nama duplikat.
### 🔹 EXPLAIN ANALYZE
`EXPLAIN` = Melihat rencana eksekusi query

`EXPLAIN ANALYZE` = Jalankan query dan tunjukkan biaya aktual (berapa cepat, apakah pakai index)

📌 Lihat performa query
```sql
EXPLAIN ANALYZE
SELECT * FROM customers WHERE name = 'Alice';
```
📌 Jika pakai index, hasilnya akan terlihat seperti ini
```sql
Index Scan using idx_customers_name on customers ...
```
📌 Kalau tidak ada index, akan muncul seperti ini
```sql
Seq Scan on customers ...
```

✅ Ini sangat penting untuk tuning query dan optimasi performa.

### 🛠️ Ringkasan Kapan Pakai Index
| Skenario | Perlu Index? |
|------|-----------------------------------|
| WHERE dengan kolom besar    | Ya      |
| JOIN antara 2 tabel besar	    | Ya                   |
| ORDER BY di kolom tertentu	    | Ya    |
| Tabel kecil (sedikit baris)	    | Tidak Wajib    |
| Kolom sering diubah/insert/update	    | Hati-hati! Bisa membuat overhead karena index terus berubah, solusinya melakukan reindex secara berkala    |

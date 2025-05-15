**📌 Materi:**
- GROUP BY, HAVING
- Fungsi agregat di window: RANK(), ROW_NUMBER(), LAG(), LEAD(), SUM() OVER (...)
---
### 🔹 GROUP BY & HAVING
`GROUP BY`: Mengelompokkan data berdasarkan 1 atau lebih kolom.

`HAVING`: Filter setelah GROUP BY (seperti WHERE, tapi untuk grup).
 -  Total pesanan per pelanggan.
```sql
SELECT customer_id, COUNT(*) AS total_orders
FROM orders
GROUP BY customer_id;
```
 -  Pelanggan yang memiliki lebih dari 1 pesanan
```sql
SELECT customer_id, COUNT(*) AS total_orders
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 1;
```
✅ Kalau pakai agregasi (COUNT, SUM, AVG), harus `GROUP BY`. Kalau mau filter hasil agregat → pakai `HAVING`.
### 🔹 Fungsi Agregat dalam Window
Window function melakukan agregasi tanpa mengelompokkan baris — jadi hasilnya tetap 1 baris per data.
 -  Tampilkan semua pesanan dengan ranking per pelanggan

📌 _`ROW_NUMBER()` → Nomor urut unik per grup_
```sql
SELECT 
  customer_id,
  total,
  ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY total DESC) AS row_num
FROM orders;
```
📌 _`RANK()` → Peringkat (boleh ada yang sama)_
```sql
SELECT 
  customer_id,
  total,
  RANK() OVER (PARTITION BY customer_id ORDER BY total DESC) AS rank
FROM orders;
```
📌 _`LAG()` → Ambil nilai baris sebelumnya_
```sql
SELECT 
  customer_id,
  total,
  LAG(total) OVER (PARTITION BY customer_id ORDER BY id) AS previous_total
FROM orders;
```
📌 _`LEAD()` → Ambil nilai baris sesudahnya_
```sql
SELECT 
  customer_id,
  total,
  LEAD(total) OVER (PARTITION BY customer_id ORDER BY id) AS next_total
FROM orders;
```
📌 _`SUM() OVER (...)` → Penjumlahan progresif (running total)_
```sql
SELECT 
  customer_id,
  total,
  SUM(total) OVER (PARTITION BY customer_id ORDER BY id) AS running_total
FROM orders;
```
📌 Semua `OVER (PARTITION BY ...)` artinya: hitung fungsi dalam kelompok masing-masing customer_id.

### 🛠️ Catatan Tambahan
  - Window function tidak membutuhkan GROUP BY, dan bisa tampil bersama data original.
  - Cocok untuk analisis data per individu (customer, karyawan, dll) yang berulang.

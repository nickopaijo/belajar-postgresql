**📌 Materi:**
- CREATE VIEW dan kapan menggunakannya
- Function sederhana: CREATE FUNCTION
- Transaksi: BEGIN, COMMIT, ROLLBACK
---
### 🔹 CREATE VIEW
`VIEW` adalah query yang disimpan, seperti tabel virtual. Digunakan agar:
 - Query rumit jadi mudah dipanggil ulang.
 - Konsistensi tampilan data di banyak tempat.
 - Menyembunyikan kolom sensitif (security layer).

📌 Buat view total pesanan per pelanggan
```sql
CREATE VIEW customer_order_summary AS
SELECT 
  c.id,
  c.name,
  COUNT(o.id) AS total_orders,
  COALESCE(SUM(o.total), 0) AS total_amount
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
GROUP BY c.id, c.name;
```
📌 Cara pakai
```sql
SELECT * FROM customer_order_summary;
```
### 🔹 CREATE FUNCTION
`FUNCTION` = blok kode SQL/PLpgSQL yang bisa dipanggil ulang, mirip "subprogram". Gunanya:
 - Abstraksi logic.
 - Reusable.
 - Bisa dikombinasikan dengan trigger, query, dsb.

📌 Fungsi untuk menghitung total pesanan berdasarkan `customer_id`
```sql
CREATE OR REPLACE FUNCTION get_total_order_amount(cust_id INT)
RETURNS NUMERIC AS $$
DECLARE
  v_total NUMERIC;
BEGIN
  SELECT COALESCE(SUM(total), 0) INTO v_total
  FROM orders
  WHERE customer_id = cust_id;
  RETURN v_total;
END;
$$ LANGUAGE plpgsql;
```
📌 Cara pakai
```sql
SELECT name, get_total_order_amount(id) AS total_spent
FROM customers;
```
### 🔹 TRANSAKSI: BEGIN, COMMIT, ROLLBACK
Transaksi = serangkaian perintah yang berjalan atomik (semua sukses, atau tidak sama sekali).
 - `BEGIN`: Mulai transaksi
 - `COMMIT`: Simpan semua perubahan
 - `ROLLBACK`: Batalkan semua perubahan jika ada error

📌 Tambah pesanan dan rollback kalau ada error
```sql
BEGIN;

INSERT INTO orders (customer_id, total) VALUES (1, 300.00);
-- Simulasi error: referensi customer_id tidak ada
INSERT INTO orders (customer_id, total) VALUES (999, 500.00);  -- ERROR

ROLLBACK;  -- Membatalkan dua perintah di atas
--Hasil: Tidak ada perubahan pada tabel orders
```
📌 Jika semuanya aman
```sql
BEGIN;

INSERT INTO orders (customer_id, total) VALUES (2, 400.00);
INSERT INTO orders (customer_id, total) VALUES (2, 250.00);

COMMIT;  -- Simpan
```
✅ Transaksi sangat penting untuk:
 - Data integrity.
 - Proses keuangan.
 - Banyak step yang harus jalan semua atau tidak sama sekali.

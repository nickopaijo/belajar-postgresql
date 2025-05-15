**📌 Materi:**
- Subquery dalam SELECT, FROM, WHERE
- CTE (WITH)
- CTE rekursif
---
### 🔹 Subquery
Subquery = Query di dalam query lain. Bisa digunakan dalam bagian `SELECT`, `FROM`, atau `WHERE`.
 -  Dalam `SELECT`. Untuk menampilkan hasil dari query lain sebagai kolom.
```sql
SELECT 
  name,
  (SELECT COUNT(*) FROM orders o WHERE o.customer_id = c.id) AS total_orders
FROM customers c;
```
 -  Dalam `FROM`. Untuk membentuk tabel sementara.
```sql
SELECT *
FROM (
  SELECT customer_id, COUNT(*) AS order_count
  FROM orders
  GROUP BY customer_id
) AS order_summary;
```
 -  Dalam `WHERE`. Untuk membatasi data berdasarkan hasil query lain.
```sql
SELECT name
FROM customers
WHERE id IN (SELECT customer_id FROM orders WHERE total > 100);
```
✅ Subquery bisa disebut juga sebagai "inner query" atau "nested query".
### 🔹 CTE (Common Table Expression)
CTE digunakan untuk membuat tabel sementara bernama, dengan kata kunci `WITH`.
```sql
WITH order_summary AS (
  SELECT customer_id, COUNT(*) AS total_orders
  FROM orders
  GROUP BY customer_id
)
SELECT c.name, o.total_orders
FROM customers c
JOIN order_summary o ON c.id = o.customer_id;
```
✅ CTE membuat query lebih rapi dan mudah dibaca, terutama query yang kompleks.
### 🔹 CTE Rekursif
Digunakan untuk query berulang pada struktur hierarkis seperti pohon (tree) atau organisasi.
```sql
WITH RECURSIVE org_chart AS (
  SELECT id, name, manager_id, 1 AS level
  FROM employees
  WHERE manager_id IS NULL  -- top level (CEO)

  UNION ALL

  SELECT e.id, e.name, e.manager_id, oc.level + 1
  FROM employees e
  JOIN org_chart oc ON e.manager_id = oc.id
)
SELECT * FROM org_chart;
```
✅ Rekursif artinya CTE memanggil dirinya sendiri.

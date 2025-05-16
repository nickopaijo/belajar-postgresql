# PostgreSQL

Selamat datang di sesi lanjutan SQL! Dalam sesi ini, kamu akan mempelajari konsep-konsep SQL tingkat menengah hingga menengah+, lengkap dengan praktik langsung, tips optimisasi, dan mini project.

---

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

## Struktur tabel dan isi tabel yang akan digunakan dalam materi
### 1. Tabel `customers`
```sql
CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  name TEXT
);

INSERT INTO customers (name) VALUES
('Alice'),
('Bob'),
('Charlie'),
('Diana');
```
### 2. Tabel `orders`
```sql
CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  customer_id INT REFERENCES customers(id),
  total NUMERIC
);

INSERT INTO orders (customer_id, total) VALUES
(1, 120.00),  -- Alice
(1, 80.00),   -- Alice
(2, 150.00),  -- Bob
(3, 90.00);   -- Charlie
```
### 3. Tabel `employees`
```sql
CREATE TABLE employees (
  id SERIAL PRIMARY KEY,
  name TEXT,
  manager_id INT REFERENCES employees(id)
);

INSERT INTO employees (name, manager_id) VALUES
('CEO', NULL),       -- id = 1
('CTO', 1),          -- id = 2
('CFO', 1),          -- id = 3
('Dev1', 2),         -- id = 4
('Dev2', 2),         -- id = 5
('Accountant', 3);   -- id = 6
```
---

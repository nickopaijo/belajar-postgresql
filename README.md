# PostgreSQL

---

| Sesi | Topik                             |
|------|-----------------------------------|
| 1    | Relasi & Join      |
| 2    | Subquery & CTE                    |
| 3    | Aggregation & Window Function     |
| 4    | Indexing, Performance, EXPLAIN    |
| 5    | View, Function & Transaksi        |
| 6    | Mini Project: Sistem inventaris    |

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

<!-- kunci jawaban terenkripsi dengan AES256 -->
<!-- Key: intisistemsaranasejahtera1234567 (UTF8)-->
<!-- IV: intisistemsaranasejahtera1234567890 (UTF8)-->
<!-- Mode: CBC -->
<!-- Input: Raw -->
<!-- Output: Hexadecimal -->

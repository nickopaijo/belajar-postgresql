**📌 Sistem Inventaris Toko**

Tugas:
- Query total penjualan per produk
- Buat view top_selling_products (Produk terlaris)
- Tambahkan function Total Penjualan Produk per ID
---

## Struktur tabel dan isi tabel yang digunakan
### 1. Struktur tabel `products` dan `sales`
```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price NUMERIC(10, 2) NOT NULL,
    stock INTEGER NOT NULL DEFAULT 0
);

CREATE TABLE sales (
    id SERIAL PRIMARY KEY,
    product_id INTEGER REFERENCES products(id),
    quantity INTEGER NOT NULL,
    sale_date DATE DEFAULT CURRENT_DATE
);
```
### 2. Isi tabel `products` dan `sales`
```sql
-- Produk
INSERT INTO products (name, price, stock) VALUES
('Laptop', 12000000, 10),
('Mouse', 150000, 50),
('Keyboard', 300000, 30),
('Monitor', 2000000, 15);

-- Penjualan
INSERT INTO sales (product_id, quantity, sale_date) VALUES
(1, 2, '2024-12-01'),
(2, 5, '2024-12-01'),
(1, 1, '2025-01-15'),
(3, 2, '2025-01-20'),
(2, 3, '2025-02-05');
```

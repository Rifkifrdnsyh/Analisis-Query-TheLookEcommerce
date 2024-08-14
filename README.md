# Analisis-Query-TheLookEcommerce

# 1. Produk Terlaris
SELECT
    p.name, 
    SUM(oi.product_id) AS total_quantity
FROM 
    bigquery-public-data.thelook_ecommerce.order_items oi
JOIN 
    bigquery-public-data.thelook_ecommerce.products p ON oi.product_id = p.id
GROUP BY 
    p.name
ORDER BY 
    total_quantity DESC

    Penjelasan:
    SELECT p.name, SUM(oi.product_id) AS total_quantity : memilih data dari tabel products dengan kolom name dan memberikan penjumlahan pada kolom product_id pada tabel orders_item lalu diberikan alias total_quantity
    FROM bigquery-public-data.thelook_ecommerce.order_items oi : mengakses dari tabel orders item dan diberikan alias oi
    JOIN bigquery-public-data.thelook_ecommerce.products p ON oi.product_id = p.id : Menggabungkan elemen dari array satu atau beberapa dimensi menggunakan pembatas yang ditentukan dengan tabel products yang diwakili kolom id dan tabel orders_item diwakili kolom product_id
    GROUP BY p.name: Mengelompokkan hasil berdasarkan nama produk. 
    ORDER BY total_quantity DESC: Mengurutkan hasil dari yang terlaris.

# 2. Jumlah Pembeli Pada Tahun 2024
SELECT 
    COUNT(*) AS new_users
FROM 
    Users
WHERE 
    created_at BETWEEN '2024-01-01' AND '2024-12-31'

    Penjelasan:
    COUNT(*): Menghitung total pengguna baru.
    WHERE created_at: Membatasi hasil hanya untuk pengguna yang mendaftar di tahun 2024.
    
    
    

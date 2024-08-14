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

# 3. Total Penjualan Pada Tahun 2024
SELECT 
    SUM(oi.product_id * p.retail_price) AS total_sales
FROM 
    bigquery-public-data.thelook_ecommerce.orders o
JOIN 
     bigquery-public-data.thelook_ecommerce.order_items oi ON o.order_id = oi.order_id
JOIN 
     bigquery-public-data.thelook_ecommerce.products p ON oi.product_id = p.id
WHERE 
    o.created_at BETWEEN '2024-01-01' AND '2024-12-31'

    Penjelasan:
    SUM(oi.quantity * p.price): Menghitung total penjualan dengan mengalikan jumlah item yang dipesan dengan harga produk.
    JOIN: digunakan untuk menggabungkan tabel Orders, Order_Items, dan Products berdasarkan kunci terkait.
    WHERE: membatasi hasil untuk tahun 2024.

# 4. Menampilkan Rincian Pesanan Complete
SELECT 
    o.order_id AS order_id,
    o.user_id,
    o.status,
    o.created_at
FROM 
   bigquery-public-data.thelook_ecommerce.orders o
   WHERE 
    o.status = 'Complete'
ORDER BY 
    o.created_at DESC

    Penjelasan:
    Where: Menampilkan rincian pesanan dengan status pembayaran Complete.
    Order by: Mengurutkan hasil berdasarkan tanggal pesanan terbaru.

# 5. Jumlah Pengguna Berdasarkan Jenis Kelamin
SELECT 
    gender,
    COUNT(id) AS total_users
FROM 
   bigquery-public-data.thelook_ecommerce.users 
GROUP BY 
    gender
ORDER BY 
    total_users DESC

    Penjelasa:
    COUNT(id): Menghitung jumlah id
    Group by: Mengurutkan berdasarkan gender
    Order by: Menghitung jumlah pengguna berdasarkan jenis kelamin dan mengurutkan dari yang terbanyak.

# 6. Menghitung Presentase Jumlah Pesanan Dengan Status Complete
SELECT
    COUNT(CASE WHEN status = 'Complete' THEN 1 END) * 100.0 / COUNT(*) AS success_payment_percentage
FROM 
    bigquery-public-data.thelook_ecommerce.orders

    Penjelasan:
    COUNT: Menghitung persentase pesanan dengan status pembayaran Complete terhadap total pesanan.

# 7. Jumlah Pengguna Berdasarkan Negara
SELECT 
    country,
    COUNT(id) AS total_users
FROM 
   bigquery-public-data.thelook_ecommerce.users 
GROUP BY 
    country
ORDER BY 
    total_users DESC

    Penjelasan: 
    COUNT: menghitung jumlah id pada setiap negara
    Group by: Mengurutkan berdasarkan country
    Order by: Menghitung jumlah pengguna berdasarkan negara dan mengurutkan dari yang terbanyak.

# 8. Jumlah Pengguna Berdasarkan Jenis Sumber 
SELECT 
    traffic_source,
    COUNT(id) AS total_users
FROM 
   bigquery-public-data.thelook_ecommerce.users 
GROUP BY 
    traffic_source
ORDER BY 
    total_users DESC

    Penjelasan:
    COUNT: menghitung jumlah id pada setiap sumber
    Group by: Mengurutkan berdasarkan sumber
    Order by: Menghitung jumlah pengguna berdasarkan jenis sumber dan mengurutkan dari yang terbanyak.

# 9. Jumlah Pesanan Status Complete
SELECT 
    COUNT(*) AS successful_orders
FROM 
    bigquery-public-data.thelook_ecommerce.orders
WHERE 
    status = 'Complete'

    Penjelasan:
    COUNT: Menghitung jumlah pesanan dengan status pembayaran "Complete".
    WHERE: Menampilkan rincian pesanan dengan status pembayaran Complete.

# 10. Jumlah Produk Pada Setiap Kategori
SELECT
    category,
    COUNT(*) AS total_products
FROM 
  bigquery-public-data.thelook_ecommerce.products
GROUP BY 
    category
ORDER BY 
    total_products DESC

    Penjelasan: 
    COUNT: Menghitung jumlah produk
    Group by: Mengelompokkan produk berdasarkan kategori dan menghitung jumlah produk dalam setiap kategori.

    

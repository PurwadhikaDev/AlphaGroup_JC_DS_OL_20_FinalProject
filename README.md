# Summary
Proyek ini menganalisis data transaksi dari Olist, sebuah e-commerce asal Brasil, dengan tujuan membangun model prediksi keterlambatan pengiriman pesanan.
Melalui eksplorasi data dan machine learning, proyek ini menghasilkan insight terkait faktor keterlambatan pengiriman, serta model klasifikasi yang dapat membantu tim layanan pelanggan dalam mengantisipasi potensi keterlambatan.

# Bussines Understanding
Olist adalah perusahaan e-commerce asal Brasil yang berfokus pada pemberdayaan usaha kecil dan menengah (UKM) untuk dapat berjualan secara online dengan lebih mudah. Mereka menyediakan platform dan serangkaian solusi teknologi (solusi perangkat lunak untuk bisnis, 
manajemen inventaris, pelacakan pesanan, dan lainnya)  yang memungkinkan para penjual untuk terhubung dengan berbagai marketplace besar.

## Problem Statement
Keterlambatan pengiriman dapat menurunkan kepuasan pelanggan, meningkatkan risiko churn, dan menambah biaya kompensasi. Oleh karena itu, perusahaan memerlukan model prediktif untuk mengidentifikasi pesanan yang berpotensi terlambat.

## Stakeholder
Tim Layanan Pelanggan & Marketing: dapat mengantisipasi keterlambatan dengan proaktif memberikan informasi atau kompensasi.
Manajemen Operasional: dapat mengoptimalkan resource distribusi.

## Tujuan
1, Membangun model prediksi pesanan tepat waktu (1) atau terlambat (0).
2. Memberikan rekomendasi tindak lanjut kepada Tim Layanan Pelanggan dan Marketing atas hasil prediksi model.

# Dataset
Dataset ini merupakan dataset pesanan di market place olist store yang diperoleh dari [kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce?select=olist_customers_dataset.csv). Jumlah data yang tersedia adalah data 100 ribu order dari tahun 2016 sampai tahun 2018. Berikut adalah fitur-fitur yang digunakan project ini.

|Kolom |Deskripsi|
|-----|:-----|
|order_id|pengenal unik pesanan|
|customer_id|key dataset customer. Setiap pesanan punya customer_id yang unik|
|order_status|Status pesanan. (delivered, shipped, etc)|
|order_purchase_timestamp|timestamp pembelian|
|order_approved_at|timestamp approval pembayaran|
|order_delivered_carrier_date|timestamp saat pesanan diserahkan ke partner logistik|
|order_delivered_customer_date|tanggal pesanan sampai ke pelanggan|
|order_delivered_delivery_date|estimasi tanggal pesanan sampai|
|customer_zip_code_prefix|lima digit pertama kode pos pelanggan|
|customer_city|nama kota pelanggan|
|customer_state|negara bagian pelanggan|
|seller_zip_code_prefix|lima digit pertama kode pos penjual|
|seller_city|kota penjual|
|seller_state|negara bagian penjual|
|review_score|skor review|
|product_category_name|nama kategori produk dalam bahasa portugis|
|product_category_name_english|nama kategori produk dalam bahasa inggris|
|price|harga per item|
|freight_value|har pengiriman barang|
|product_weight_g|berat produk dalam gram|
|product_lenght_cm|panjang produk dalam cm|
|product_height_cm|tinggi produk dalam cm|
|product_width_cm|lebar produk dalalm cm|

# Struktur Project
1. Pemahaman Bisinis:  konteks, problem statement, stakeholder.
2. Pra-pemrosesan data: Memuat dataset, membersihkan data, dan mengeksplorasi data 
3. Feature Engineering: Membuat fitur baru seperti waktu pengiriman, service level, total volume, total weight, jarak seller dan pelanggan meningkatkan daya prediksi.
4. Pemodelan: Membangun model machine learning untuk memprediksi apakah suatu order akan terlambat atau tepat waktu. Beberapa model diuji, dan model terbaik dipilih berdasarkan metrik performa terbaik.
5. Evaluasi dan Insight: Mengevaluasi performa model dan memberikan insight yang dapat ditindaklanjuti oleh tim layanan pelanggan dan marketing guna meningkatkan kepuasan customer.

# Exploratory Data Analysis
1. Distribusi Target: On-time vs Late
2. Analisis Missing Value
3. Distribusi Fitur Numerik
4. Analisis Bivariat: Kategori Produk vs Proporsi Keterlambatan
5. Analisis Kohort Pelanggan (Pertumbuhan Pelanggan Baru)
6. Analisis Pertumbuhan Order vs Keterlambatan & Akuisisi Pengguna Baru
7. Analisis Service Level: Korelasi Ketepatan Pengiriman dengan Skor Review
8. Analisis Tingkat Keterlambatan: "Semakin Lama Terlambat, Semakin Buruk Skornya?"
9. Analisis Hubungan Jarak dengan Waktu Pengiriman terhadap Keterlambatan
10. Analisis Volume terhadap Waktu Pengiriman
11. Analisis Berat terhadap Waktu Pengiriman
12. Analisis SLA terhadap Waktu Pengiriman
13. Insight Utama

# Tools dan Library
1. Python: untuk analisis data dan pemodelan
2. Jupyter Notebook: untuk pengembangan kode
3. Pandas, NumPy: untuk manipulasi data dan analisis data
4. Scikit-Learn: untuk pemodelan machine learning
5. Matplotlib, Seaborn: untuk visualisasi data

# Kesimpulan
Berdasarkan hasil dari model yang dibangun (sebelum threshold tuning), model dapat menangkap 67% order yang mungkin terlambat dan 71% order yang mungkin ontime. Dari model ini, perlu diperhatikan adalah tingkat precision pada kelas 0 (terlambat) di 16%, sedangkan kelas 1 (ontime) adalah 96%. Hal tersebut menandakan bahwa model memberikan banyak false alarm dimana ada risiko dari biaya yang akan dikeluarkan perusahaan.

Dengan melihat kondisi pertumbuhan order dari Olist di tahun 2018 yang mengalami penurunan, maka kami merekomendasikan bahwa fokus prioritasnya adalah meningkatkan jumlah order. Dengan simulasi yang ada, diketahui bahwa mendapatkan konsumen baru memerlukan biaya lebih tinggi dibandingkan mempertahankan konsumen yang sudah ada. Dengan begitu, model disarankan agar memberikan nilai recall yang tinggi, walaupun precisionnya akan menurun dan memberikan banyak false alarm.

# Saran dan rekomendasi

Berdasarkan hasil analisis dan model prediksi, rekomendasi untuk Olist adalah:

1. **Optimasi Logistik**  
   - Gunakan model prediksi untuk mengidentifikasi order yang berpotensi terlambat sejak awal.  
   - Berikan prioritas lebih tinggi pada order tersebut dalam distribusi logistik.

2. **Customer Experience Management**  
   - Jika model memprediksi keterlambatan, tim Customer Service bisa proaktif menghubungi pelanggan.  
   - Sediakan kompensasi berupa voucher atau potongan ongkir untuk menjaga kepuasan.

3. **Strategi Marketing**  
   - Data prediksi bisa dipakai untuk segmentasi pelanggan (misalnya pelanggan yang rawan mengalami keterlambatan → diberikan penawaran khusus).  

4. **Feedback Loop**  
   - Review score pelanggan dapat dipantau sebagai indikator keberhasilan implementasi model.  
   - Insight dari review digunakan untuk menyempurnakan model di iterasi berikutnya.

# Tableu
![Tableu](https://github.com/user-attachments/assets/4dd428cf-94d9-483e-ab55-764d3b2bbed7)





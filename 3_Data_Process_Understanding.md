# Data Process Understanding

Proyek ini menerapkan alur kerja *end-to-end data analytics* yang mencakup enam tahapan utama, mulai dari persiapan data hingga validasi hasil dashboard.

## 1. Data Cleaning & Preparation

Dataset awal diperoleh dalam format Excel dan diolah menggunakan Python untuk memastikan kualitas, kelengkapan, dan konsistensi data sebelum disimpan ke dalam database.

Tahapan data cleaning meliputi:

- **Pengecekan Duplikasi:** Mengidentifikasi dan menangani data duplikat pada setiap tabel.
- **Penanganan Missing Values:** Mengidentifikasi nilai yang hilang (*null values*) serta melakukan penanganan atau pengisian nilai sesuai kebutuhan data.

Dokumentasi proses: [Data Cleaning Notebook](./3_Clean_Dataset/2_Data_Cleaning.ipynb)

## 2. Database Storage & Management

Setelah proses data cleaning selesai, data disimpan ke dalam **PostgreSQL** sebagai database utama proyek.

PostgreSQL digunakan untuk:
- Menyimpan data yang telah dibersihkan secara terstruktur dan terpusat.
- Mempermudah pengelolaan serta pengambilan data (*data retrieval*) menggunakan SQL.
- Menyediakan sumber data yang konsisten untuk proses analisis selanjutnya.

Dokumentasi proses: [Load Dataset to Database](./3_Clean_Dataset/4_Load_Dataset_to_DB.sql)

## 3. Data Synchronization

Proses sinkronisasi dilakukan menggunakan SQL untuk memastikan konsistensi antara data listing dan transaksi.

Berdasarkan hasil pemeriksaan, ditemukan beberapa listing yang masih berstatus terbuka meskipun properti terkait telah berhasil terjual melalui listing lain yang dibuat setelahnya.

Untuk menjaga konsistensi data dan akurasi analisis inventory, dilakukan penyesuaian pada kolom `close_date` dan `listing_status` dalam tabel listings berdasarkan informasi transaksi yang berkaitan.

Dokumentasi proses: [Data Synchronization](./5_Data_Synchronization.sql)

## 4. Data Analysis

Analisis data dilakukan menggunakan **Python** dengan mengakses data dari PostgreSQL.

Tahapan analisis meliputi:
- *Exploratory Data Analysis (EDA)* untuk memahami karakteristik dan distribusi data.
- Perhitungan metrik bisnis terkait conversion performance dan inventory absorption.
- Analisis pengaruh relisting terhadap conversion performance
- Analisis karakteristik property serta segmen properti berdasarkan kinerja konversi.
- Analisis kontribusi nilai transaksi dan komisi.

Dokumentasi analisis: [Property and Listing Performance](./Property%20And%20Listing%20Performance.ipynb)

## 5. Dashboard Development

Hasil analisis divisualisasikan menggunakan **Power BI** untuk membangun *Real Estate Inventory Performance Dashboard*.

Tahapan pengembangan dashboard meliputi:
- Data modeling dan pengaturan relasi antar-tabel.
- Pengembangan metrik dan KPI menggunakan **DAX**.
- Pembuatan visualisasi untuk memantau kinerja konversi, penyerapan inventory, serta pendapatan dan komisi.

File dashboard: [Real Estate Inventory Performance Dashboard (.pbix)](./Real%20Estate%20Inventory%20Performance%20Dashboard.pbix)

Dashboard preview: [Real Estate Inventory Performance Dashboard (.pdf)](./Real%20Estate%20Inventory%20Performance%20Dashboard.pdf)

## 6. Data Validation

Untuk memastikan akurasi hasil dashboard, dilakukan proses validasi silang menggunakan **Python**.

Nilai KPI dan hasil perhitungan yang ditampilkan di Power BI dibandingkan dengan hasil perhitungan secara independen menggunakan Python. Proses ini bertujuan untuk memastikan konsistensi angka serta meminimalkan kesalahan dalam perhitungan dan penyajian data.
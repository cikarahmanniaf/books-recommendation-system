# Laporan Proyek Machine Learning - Cika Rahmannia Febrianti

## Project Overview

Sistem rekomendasi telah menjadi komponen penting dalam berbagai platform digital, terutama pada e-commerce dan layanan hiburan seperti Amazon, Netflix, dan Goodreads. Sistem ini berfungsi untuk membantu pengguna menemukan produk atau konten yang sesuai dengan preferensi dan kebutuhan mereka, sehingga tidak hanya meningkatkan pengalaman pengguna, tetapi juga mendorong penjualan dan keterlibatan pengguna terhadap platform.

Masalah utama yang ingin diselesaikan dalam proyek ini adalah bagaimana mempermudah pengguna dalam menemukan buku yang relevan di antara jutaan judul yang tersedia secara daring. Tanpa adanya sistem rekomendasi yang efektif, pengguna seringkali mengalami kesulitan dalam menavigasi banyaknya pilihan yang ada. Hal ini dapat berujung pada pengalaman pengguna yang kurang memuaskan, bahkan penurunan loyalitas pelanggan

Untuk menjawab tantangan tersebut, proyek ini akan menerapkan dua pendekatan utama dalam sistem rekomendasi, yaitu Content-Based Filtering (CBF) dan Collaborative Filtering (CF). Pendekatan ini bertujuan untuk membangun model rekomendasi buku yang mampu mempersonalisasi saran berdasarkan preferensi pengguna dan pola interaksi komunitas pembaca.

Menurut Ricci et al. [3], sistem rekomendasi terbukti mampu meningkatkan kepuasan pengguna serta konversi penjualan dengan mengurangi beban keputusan yang dihadapi konsumen. Studi lain oleh Gómez-Uribe dan Hunt [2] menunjukkan keberhasilan implementasi sistem rekomendasi dalam industri hiburan melalui Netflix Prize, yang menjadi salah satu acuan dalam pengembangan algoritma prediktif berbasis penilaian pengguna.

Dalam era digital yang penuh dengan pilihan, pengguna kerap kali kewalahan ketika harus memilih dari ribuan opsi, yang dapat berujung pada keputusan yang tidak optimal atau bahkan tidak memilih sama sekali [1]. Situasi ini juga terjadi pada platform buku digital dan toko buku daring, di mana katalog besar memungkinkan ditemukannya buku dari berbagai genre dan preferensi, termasuk judul-judul yang hanya diminati oleh segmen tertentu. Di sinilah sistem rekomendasi memegang peran penting dalam membantu pengguna menemukan buku yang relevan dengan cepat dan efisien.

Referensi:
- [1] B. Schwartz, The Paradox of Choice: Why More Is Less. New York, NY, USA: Harper Perennial, 2015.
- [2] C. A. Gómez-Uribe and N. Hunt, “The Netflix Recommender System: Algorithms, Business Value, and Innovation,” ACM Trans. Manag. Inf. Syst., vol. 6, no. 4, pp. 1–19, 2016, doi: 10.1145/2843948.
- [3] F. Ricci, L. Rokach, and B. Shapira, “Introduction to Recommender Systems Handbook,” in Recommender Systems Handbook, Springer, 2011, pp. 1–35, doi: 10.1007/978-0-387-85820-3_1.

## Business Understanding

### Problem Statements

1. Bagaimana membangun sistem rekomendasi yang dapat mempersonalisasi daftar bacaan pengguna berdasarkan preferensi eksplisit (rating) dan implisit (pola interaksi)?
2. Bagaimana memanfaatkan metadata buku (judul, penulis, genre) untuk menghasilkan rekomendasi yang relevan secara konten?
3. Bagaimana mengukur dan membandingkan performa antara model Collaborative Filtering dan Content-Based Filtering dalam sistem rekomendasi buku?

### Goals

1. Mengembangkan sistem rekomendasi buku yang menggabungkan data eksplisit dan implisit untuk personalisasi yang lebih baik.
2. Memanfaatkan metadata buku untuk mendukung rekomendasi berbasis konten yang relevan dengan preferensi pengguna.
3. Melakukan evaluasi komparatif performa model Collaborative Filtering dan Content-Based Filtering menggunakan metrik yang sesuai seperti RMSE, Precision, Recall, dan F1-score.

### Solution Approach

- Collaborative Filtering (CF):
Menerapkan teknik User-Based dan Item-Based Collaborative Filtering, serta matrix factorization untuk memprediksi rating dan memberikan rekomendasi berdasarkan pola interaksi antar pengguna.

- Content-Based Filtering (CBF):
Membangun representasi preferensi pengguna berdasarkan metadata buku seperti genre, penulis, dan sinopsis, guna merekomendasikan buku dengan konten yang serupa dengan minat pengguna.

## Data Understanding
Dataset yang digunakan dalam proyek ini berasal dari [Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset/data) yang tersedia di Kaggle. Dataset ini terdiri dari tiga file utama yang memuat informasi pengguna, buku, dan interaksi rating:

- Books.csv: Metadata buku   
- Ratings.csv: Data rating pengguna terhadap buku  

### Deskripsi Variabel

#### Books.csv

| Variabel           | Deskripsi                          |
|--------------------|----------------------------------|
| `ISBN`             | Kode unik buku                   |
| `Book-Title`       | Judul buku                      |
| `Book-Author`      | Penulis buku                    |
| `Year-Of-Publication` | Tahun terbit buku              |
| `Publisher`        | Penerbit buku                   |
| `Image-URL-S`      | URL gambar sampul ukuran kecil  |
| `Image-URL-M`      | URL gambar sampul ukuran sedang |
| `Image-URL-L`      | URL gambar sampul ukuran besar  |

#### Ratings.csv

| Variabel     | Deskripsi                               |
|--------------|---------------------------------------|
| `User-ID`    | ID pengguna yang memberikan rating     |
| `ISBN`       | Kode unik buku yang diberi rating      |
| `Book-Rating`| Nilai rating yang diberikan (0-10)    |

### Exploratory Data Analysis (EDA)
Sebelum dilakukan preparasi data, dilakukan eksplorasi data terlebih dahulu agar karakteristik dari dataset diketahui. Pada kasus ini, dilakukan tahapan EDA secara univariat untuk masing-masing dataset sebagai berikut.

1. Books Univariate EDA
- Pemeriksaan nama variabel, tipe data, dan missing value. Ada variabel non relevan yang nantinya akan di drop, ada missing value pada 'Book-Author' dan 'Publisher' yang akan diisi dengan string 'Unknown'
- Pemeriksaan duplikasi data keseluruhan dan primary key
- Pemeriksaan nilai unik pada 'Year-of-Publication' karena ada nilai non numerik/year sehingga diasumsikan adanya salah input (data kotor)
- Visualisasi penulis dengan buku terbanyak, penerbit dengan buku terbanyak, dan judul buku paling umum.

<div align="center">
  <img src="https://github.com/user-attachments/assets/1589df60-4dce-4e0e-a630-56dcbd3d7408" alt="Top 10 Penulis dengan Buku Terbanyak" width="600"/>
  <img src="https://github.com/user-attachments/assets/83fd0ab9-2fd9-4aa9-b697-cca4ea509584" alt="Top 10 Penerbit dengan Buku Terbanyak" width="600"/>
  <img src="https://github.com/user-attachments/assets/7088c167-6876-436e-b8d5-924b6abe7402" alt="Judul Buku Paling Umum" width="600"/>
</div>

- Validasi data panjang ISBN

<div align="center">
  <img src="https://github.com/user-attachments/assets/ed907a68-1179-46e1-a601-20868b8f154d" alt="Distribusi Panjang ISBN" width="600"/>
</div>

Dalam grafik tersebut, diketahui bahwa panjang ISBN sudah benar ada di angka '10' untuk keseluruhan.
  
2. Ratings Univariate EDA
- Pemeriksaan nama variabel, tipe data, dan missing value
- Pemeriksaan duplikasi data ditemukan adanya duplikasi User-ID sebanyak '1044497'. User-ID memang muncul berulang kali di dataset rating, karena satu user bisa memberi rating ke banyak buku. Sehingga adanya duplikat itu normal. Namun, untuk data keseluruhan, tidak ditemukan adanya duplikasi.
- Visualisasi Distribusi Nilai Book-Rating
<div align="center">
  <img src="https://github.com/user-attachments/assets/eefed90b-0991-42ba-9c35-e6f43bf35fda" alt="Distribusi Nilai Book-Rating" width="600"/>
</div>
Book Rating bernilai '0' kemungkinan menunjukkan bahwa user tidak memberikan rating eksplisit. Rating ini bisa dianggap sebagai interaksi pasif (misalnya user hanya melihat buku tersebut). Oleh karena itu, nilai rating '0' akan dihilangkan dan hanya rating eksplisit (1–10) yang digunakan untuk algoritma Collaborative Filtering (CF) dan Content-Based Filtering (CBF).
- Visualisasi Distribusi Jumlah Rating per User dan per Buku

<div align="center">
  <img src="https://github.com/user-attachments/assets/8e0172c0-2fd6-47aa-a083-c3637c898bf8" alt="Distribusi Jumlah Rating per User" width="600"/>
</div>

Terdapat banyak user yang hanya memberikan sedikit rating. Untuk meningkatkan kualitas rekomendasi pada CF, user pasif (dengan hanya 1–2 rating) akan dihapus dari dataset karena dapat menyebabkan matriks interaksi menjadi terlalu sparse (jarang terisi), yang berdampak negatif pada output sistem rekomendasi.

<div align="center">
  <img src="https://github.com/user-attachments/assets/75fb2b13-27c6-4ef6-8438-4ee13eb2ba36" alt="Distribusi Jumlah Rating per Buku" width="600"/>
</div>

Begitu pula dengan banyak buku yang hanya mendapatkan sedikit rating. Hal ini menyebabkan informasi yang terbatas untuk mengenali kemiripan item/user dalam CF, sehingga performa rekomendasi bisa menurun.
- Visualisasi Boxplot Distribusi Rating Buku

<div align="center">
  <img src="https://github.com/user-attachments/assets/e0202b93-0da2-4908-805c-ce5a35f31ca0" alt="Boxplot Distribusi Rating Buku" width="600"/>
</div>

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

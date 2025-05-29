# Laporan Proyek Machine Learning - Cika Rahmannia Febrianti

## Project Overview

Sistem rekomendasi telah menjadi komponen penting dalam berbagai platform digital, terutama pada e-commerce dan layanan hiburan seperti Amazon, Netflix, dan Goodreads. Sistem ini berfungsi untuk membantu pengguna menemukan produk atau konten yang sesuai dengan preferensi dan kebutuhan mereka, sehingga tidak hanya meningkatkan pengalaman pengguna, tetapi juga mendorong penjualan dan keterlibatan pengguna terhadap platform.

Masalah utama yang ingin diselesaikan dalam proyek ini adalah bagaimana mempermudah pengguna dalam menemukan buku yang relevan di antara jutaan judul yang tersedia secara daring. Tanpa adanya sistem rekomendasi yang efektif, pengguna seringkali mengalami kesulitan dalam menavigasi banyaknya pilihan yang ada. Hal ini dapat berujung pada pengalaman pengguna yang kurang memuaskan, bahkan penurunan loyalitas pelanggan

Untuk menjawab tantangan tersebut, proyek ini akan menerapkan dua pendekatan utama dalam sistem rekomendasi, yaitu Content-Based Filtering (CBF) dan Collaborative Filtering (CF). Pendekatan ini bertujuan untuk membangun model rekomendasi buku yang mampu mempersonalisasi saran berdasarkan preferensi pengguna dan pola interaksi komunitas pembaca.

Menurut Ricci et al. [3], sistem rekomendasi terbukti mampu meningkatkan kepuasan pengguna serta konversi penjualan dengan mengurangi beban keputusan yang dihadapi konsumen. Studi lain oleh Gómez-Uribe dan Hunt [2] menunjukkan keberhasilan implementasi sistem rekomendasi dalam industri hiburan melalui Netflix Prize, yang menjadi salah satu acuan dalam pengembangan algoritma prediktif berbasis penilaian pengguna.

Dalam era digital yang penuh dengan pilihan, pengguna kerap kali kewalahan ketika harus memilih dari ribuan opsi, yang dapat berujung pada keputusan yang tidak optimal atau bahkan tidak memilih sama sekali [1]. Situasi ini juga terjadi pada platform buku digital dan toko buku daring, di mana katalog besar memungkinkan ditemukannya buku dari berbagai genre dan preferensi, termasuk judul-judul yang hanya diminati oleh segmen tertentu. Di sinilah sistem rekomendasi memegang peran penting dalam membantu pengguna menemukan buku yang relevan dengan cepat dan efisien.

Referensi:
[1] B. Schwartz, The Paradox of Choice: Why More Is Less. New York, NY, USA: Harper Perennial, 2015.
[2] C. A. Gómez-Uribe and N. Hunt, “The Netflix Recommender System: Algorithms, Business Value, and Innovation,” ACM Trans. Manag. Inf. Syst., vol. 6, no. 4, pp. 1–19, 2016, doi: 10.1145/2843948.
[3] F. Ricci, L. Rokach, and B. Shapira, “Introduction to Recommender Systems Handbook,” in Recommender Systems Handbook, Springer, 2011, pp. 1–35, doi: 10.1007/978-0-387-85820-3_1.

## Business Understanding

Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:
- Pernyataan Masalah 1
- Pernyataan Masalah 2
- Pernyataan Masalah n

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Jawaban pernyataan masalah 1
- Jawaban pernyataan masalah 2
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi).

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

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

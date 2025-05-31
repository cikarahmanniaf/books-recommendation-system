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

Tahapan data preparation dilakukan agar data siap digunakan untuk membangun sistem rekomendasi berbasis Collaborative Filtering (CF) dan Content-Based Filtering (CBF). Proses dilakukan secara sistematis sebagai berikut:

1. Menghapus Kolom Tidak Relevan
Beberapa kolom seperti `Image-URL-S`, `Image-URL-M`, `Image-URL-L`, dan `ISBN_Length` tidak relevan untuk kebutuhan sistem rekomendasi, sehingga dihapus dari dataframe `books`.

2. Menangani Missing Values
Nilai kosong pada kolom `Book-Author` dan `Publisher` diisi dengan nilai `'Unknown Author'` dan `'Unknown Publisher'` agar tidak mengganggu proses pengolahan data selanjutnya.

```python
books['Book-Author'].fillna('Unknown Author', inplace=True)
books['Publisher'].fillna('Unknown Publisher', inplace=True)
```
3. Normalisasi Teks
Data teks dibersihkan dari spasi berlebih di awal, akhir, maupun tengah teks agar lebih konsisten.

```python
def clean_text(text):
    if pd.isnull(text):
        return ""

    text = text.strip()                      # hapus spasi di awal/akhir
    text = re.sub(r'\s+', ' ', text)        # hapus spasi berlebih di tengah
    return text

for col in ['Book-Title', 'Book-Author', 'Publisher']:
    books[col] = books[col].apply(clean_text)
```
4. Penanganan Tahun Terbit yang Tidak Valid
Kolom 'Year-Of-Publication' mengandung beberapa entri yang tidak valid seperti nama penerbit dan angka di luar jangkauan. Namun, karena tidak digunakan dalam model CF dan CBF, kolom ini dibiarkan apa adanya.
5. Memfilter User dan Buku
Agar matriks interaksi tidak terlalu sparse, user yang hanya memberikan kurang dari 3 rating serta buku yang mendapatkan kurang dari 3 rating dihapus.

```python
# Filter user aktif
user_counts = ratings['User-ID'].value_counts()
ratings = ratings[ratings['User-ID'].isin(user_counts[user_counts >= 3].index)]

# Filter buku populer
book_counts = ratings['ISBN'].value_counts()
ratings = ratings[ratings['ISBN'].isin(book_counts[book_counts >= 3].index)]
```
6. Menghapus rating tidak eksplisit
Rating dengan nilai 0 dianggap bukan sebagai penilaian eksplisit, sehingga dihapus.

```python
ratings = ratings[ratings['Book-Rating'] > 0]
```
7. Menyiapkan Dataset untuk CF dan CBF
Dataset cf_data digunakan untuk Collaborative Filtering, sementara cbf_data untuk Content-Based Filtering. Proses ini dilakukan dengan merge antara data ratings dan data books.

```
cf_data = ratings.merge(books[['ISBN', 'Book-Title']], on='ISBN', how='left')
cbf_data = ratings.merge(books[['ISBN', 'Book-Title', 'Book-Author']], on='ISBN', how='left')
```
8. Menangani Missing Values Setelah Merge
Setelah proses merge, ditemukan beberapa nilai kosong karena tidak semua ISBN di ratings tersedia di books. Untuk CBF, kolom Book-Title dan Book-Author sangat penting karena digunakan dalam fitur konten. Oleh karena itu, baris yang memiliki nilai kosong dihapus.
```
cbf_data = cbf_data.dropna(subset=['Book-Title', 'Book-Author'])
```
Untuk CF, kolom Book-Title tidak digunakan secara langsung dalam model, sehingga nilai kosong dibiarkan.
9. Dataset siap digunakan dalam modelling.


## Modeling
Sistem rekomendasi dibangun untuk menyelesaikan permasalahan pemilihan buku yang relevan bagi pengguna. Dua pendekatan yang digunakan dalam proyek ini adalah:

1. Content-Based Filtering (CBF): merekomendasikan buku berdasarkan kesamaan konten (judul dan penulis).
2. Collaborative Filtering (CF): merekomendasikan buku berdasarkan pola interaksi antar pengguna.

### Content-Based Filtering (CBF)

CBF bekerja dengan mengukur kemiripan antar item berdasarkan fitur kontennya. Dalam kasus ini, fitur yang digunakan adalah `Book-Title` dan `Book-Author`.

Dataset awal `cbf_data` berisi 253.721 entri yang terdiri dari:
- `User-ID`
- `ISBN`
- `Book-Rating`
- `Book-Title`
- `Book-Author`

Terdapat **banyak duplikasi pada kolom judul buku** yang disebabkan oleh:
- Satu buku dibaca oleh banyak user,
- Perbedaan ISBN pada buku dengan judul sama,
- Variasi penulisan nama penulis atau penerbit.

Untuk mencegah penggunaan memori yang besar di Google Colab, dilakukan sampling terhadap 5.000 judul buku unik pertama yang ditemukan.

#### Proses Pembentukan Model

1. Ekstraksi Fitur Konten
   Fitur konten dibentuk dengan menggabungkan judul dan penulis buku, lalu dinormalisasi dalam format huruf kecil.

2. Representasi Teks dengan TF-IDF
   Fitur konten dikonversi ke dalam representasi numerik menggunakan TF-IDF Vectorizer untuk mengukur pentingnya kata-kata dalam dokumen.

3. Perhitungan Kemiripan (Similarity)
   Kemiripan antar buku dihitung menggunakan cosine similarity, yang menghasilkan matriks kemiripan antar semua buku dalam sampel.

4. Fungsi Rekomendasi
   Dibuat fungsi `recommend_books_cbf(title)` yang menerima input judul buku, lalu mengembalikan daftar top-N buku yang paling mirip.

Contoh Hasil Rekomendasi
```
recommend_books_cbf('See Jane Run')
```

Output rekomendasi:
- The Little Friend  
- Run for Your Life  
- The Girls  
- What the Dead Know  
- The Weight of Water  

> Rekomendasi didasarkan pada kemiripan konten judul dan penulis dengan buku yang dicari.

---

#### Analisis Kelebihan dan Kekurangan Pendekatan CBF

Kelebihan:
- Tidak membutuhkan interaksi pengguna lain yang akan efektif untuk pengguna baru.
- Dapat menjelaskan alasan rekomendasi karena berbasis atribut konten.

Kekurangan:
- Tidak bisa merekomendasikan item yang sangat berbeda dari preferensi sebelumnya.
- Kualitas rekomendasi sangat bergantung pada informasi konten yang tersedia.
- Rentan terhadap cold-start item jika buku baru tidak memiliki data konten lengkap.

---
### Collaborative Filtering (CF)

Pendekatan Collaborative Filtering (CF) memanfaatkan interaksi antar pengguna (user-item interaction) untuk memberikan rekomendasi. Dalam proyek ini digunakan pendekatan model-based CF menggunakan *neural network (deep learning)*, bukan teknik memory-based seperti k-NN.

1. Data awal mencakup `User-ID`, `ISBN`, dan `Book-Rating`.
2. Encoding dilakukan untuk mengubah `User-ID` dan `ISBN` menjadi ID numerik agar kompatibel dengan algoritma machine learning.
3. Rating dinormalisasi ke skala [0, 1] agar stabil saat proses training.
4. Dataset dibagi menjadi data latih (80%) dan data validasi (20%).

Model neural network yang digunakan bernama `RecommenderNet`, terdiri dari:

- Embedding layer untuk merepresentasikan user dan buku dalam bentuk vektor berdimensi tetap (`embedding_size` = 50).
- Dot product antara vektor user dan buku digunakan untuk memodelkan interaksi di antara keduanya.
- Bias term ditambahkan untuk masing-masing user dan buku agar model lebih fleksibel.
- Aktivasi akhir menggunakan fungsi sigmoid agar output berada di rentang [0, 1].

```python
model = RecommenderNet(num_users, num_books, embedding_size=50)
model.compile(
    loss=tf.keras.losses.MeanSquaredError(),
    optimizer=keras.optimizers.Adam(learning_rate=0.001),
    metrics=[tf.keras.metrics.RootMeanSquaredError()]
)
``` 
Untuk mencegah overfitting, digunakan EarlyStopping dengan memonitor val_root_mean_squared_error.

#### Analisis Kelebihan dan Kekurangan Pendekatan CF

Kelebihan:
- Dapat memberikan rekomendasi yang sangat personal karena mempertimbangkan pola preferensi pengguna lain.
- Tidak memerlukan atribut konten buku (judul, penulis, dll), cocok untuk sistem dengan metadata terbatas.

Kekurangan:
- Masalah cold start untuk pengguna atau item baru (tidak ada riwayat interaksi).
- Butuh cukup banyak data interaksi agar model dapat belajar representasi yang baik.
- Lebih kompleks dan memerlukan sumber daya komputasi lebih besar dibanding CBF.

---
### Perbandingan Content-Based Filtering (CBF) dan Collaborative Filtering (CF)

| Aspek              | Content-Based Filtering                      | Collaborative Filtering                           |
|--------------------|----------------------------------------------|---------------------------------------------------|
| Data yang Dibutuhkan | Atribut konten item (judul, penulis)         | Riwayat interaksi user-item                       |
| Cold Start         | Tidak cocok untuk item baru                  | Tidak cocok untuk user/item baru                  |
| Personalization    | Terbatas pada preferensi sebelumnya          | Sangat personal, berdasarkan pengguna serupa      |
| Kompleksitas       | Lebih sederhana dan ringan                   | Kompleks dan memerlukan training model            |

## Evaluation
### Metrik Evaluasi yang Digunakan

Untuk mengevaluasi sistem rekomendasi, digunakan dua metrik evaluasi yang berbeda:

#### 1. Precision@N (untuk Content-Based Filtering)

Precision@N mengukur proporsi item relevan di antara N rekomendasi teratas yang diberikan oleh sistem.

Formula:
Precision@N = (Jumlah item relevan dalam rekomendasi top-N) / N

Precision digunakan karena sesuai dengan kebutuhan sistem rekomendasi untuk memberikan hasil yang relevan (bukan semua hasil, seperti recall). Metrik ini cocok untuk mengevaluasi seberapa baik model memberikan rekomendasi yang sesuai dengan preferensi pengguna.

Hasil Evaluasi:

- Anchor Book: *See Jane Run*
- Buku yang Disukai User:
  - The First Time
  - Run Jane Run
  - Grand Avenue
  - Lauf, Jane, lauf. Roman.
  - Olivia Joules and the Overactive Imagination
- Top-5 Rekomendasi:
  - the first time
  - run jane run
  - grand avenue
  - lauf, jane, lauf. roman.
  - olivia joules and the overactive imagination (fielding, helen)

Precision@5 = 0.80

> Artinya, 4 dari 5 buku yang direkomendasikan termasuk dalam daftar buku yang disukai user.

---

#### 2. Root Mean Squared Error (RMSE) (untuk Collaborative Filtering)

RMSE digunakan untuk mengevaluasi model *Collaborative Filtering* berbasis Neural Network. Metrik ini mengukur rata-rata selisih kuadrat antara nilai prediksi dan nilai aktual rating.

Formula:
RMSE = sqrt(Σ(y_actual - y_predicted)² / n)

RMSE dipilih karena model memprediksi rating dari pasangan user-item, dan metrik ini dapat menunjukkan seberapa dekat prediksi terhadap rating sebenarnya.

Hasil Evaluasi:

- Model berhenti pada **epoch ke-6** karena early stopping.
- RMSE Validasi Terbaik: `0.1833`

Visualisasi RMSE selama proses pelatihan:
![image](https://github.com/user-attachments/assets/177c10a3-8393-4de7-b0fd-2ee2125ada4d)

---

### Contoh Hasil Rekomendasi (Collaborative Filtering)

- User ID: 57095
Buku yang Disukai User:
- The Hitchhiker's Guide to the Galaxy
- Into the Wild
- Disclosure
- Sphere
- Airframe

Top-5 Rekomendasi dari Model:
- Harry Potter and the Chamber of Secrets Postcard Book
- The Return of the King (The Lord of the Rings, Part 3)
- My Sister's Keeper : A Novel (Picoult, Jodi)
- Dilbert: A Book of Postcards
- The Two Towers (The Lord of the Rings, Part 2)

---
## Conclusion & Recommendation
### Conclusion

Berdasarkan eksperimen dan evaluasi yang telah dilakukan, berikut kesimpulan utama dari proyek ini:

1. Personalisasi Rekomendasi
   Sistem rekomendasi berbasis *Collaborative Filtering (CF)* berhasil mempersonalisasi daftar bacaan berdasarkan rating pengguna. Model neural network yang dibangun mampu mempelajari pola interaksi antara pengguna dan buku, menghasilkan rekomendasi yang lebih sesuai dengan preferensi pribadi masing-masing user.

2. Relevansi Berdasarkan Konten
   Dengan memanfaatkan metadata buku seperti judul dan penulis, pendekatan *Content-Based Filtering (CBF)* dapat menghasilkan rekomendasi buku yang mirip secara konten. Hasil evaluasi menggunakan metrik Precision@5 menunjukkan tingkat relevansi yang cukup tinggi (*precision = 0.80*), menandakan bahwa pendekatan ini efektif dalam mengenali kesamaan konten antar buku.

3. Perbandingan Performa Model
   Dari sisi kinerja model:
   - Model CF menghasilkan **RMSE validasi sebesar 0.1833**, menunjukkan prediksi rating yang cukup akurat.
   - Model CBF memiliki **Precision@5 sebesar 0.80**, menunjukkan 80% buku yang direkomendasikan memang sesuai dengan selera user berdasarkan buku yang disukai.

   Setiap pendekatan memiliki kelebihan dan kekurangan:
   - CBF unggul dalam menghadapi masalah *cold start* item, karena hanya butuh metadata buku.
   - CF unggul dalam personalisasi, tetapi membutuhkan cukup banyak data interaksi dan sensitif terhadap user baru (*cold start problem*).

---

### Recommendation

Berdasarkan hasil dan keterbatasan masing-masing metode, pendekatan terbaik untuk sistem rekomendasi buku adalah:

> Menggabungkan Collaborative Filtering dan Content-Based Filtering dalam model Hybrid Recommender System.

Dengan sistem Hybrid, dapat memanfaatkan keunggulan kedua pendekatan:
- Menggabungkan personalisasi dari CF
- Menggabungkan relevansi konten dari CBF
- Mengurangi masalah cold start

Dengan mengimplementasikan model hybrid, sistem rekomendasi akan lebih fleksibel, akurat, dan mampu beradaptasi terhadap berbagai kondisi data dan jenis pengguna.


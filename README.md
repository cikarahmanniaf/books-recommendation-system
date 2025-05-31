# Book Recommendation System

Sistem rekomendasi buku yang dibangun menggunakan dua pendekatan utama: Content-Based Filtering (CBF) dan Collaborative Filtering (CF) berbasis neural network. Proyek ini bertujuan untuk memberikan rekomendasi buku yang relevan dan terpersonalisasi berdasarkan preferensi pengguna.

## Problem Statements

1. Bagaimana membangun sistem rekomendasi yang dapat mempersonalisasi daftar bacaan pengguna berdasarkan preferensi eksplisit (rating) dan implisit (pola interaksi)?
2. Bagaimana memanfaatkan metadata buku (judul, penulis, genre) untuk menghasilkan rekomendasi yang relevan secara konten?
3. Bagaimana mengukur dan membandingkan performa antara model Collaborative Filtering dan Content-Based Filtering dalam sistem rekomendasi buku?

## Dataset

Dataset yang digunakan adalah Book-Crossing Dataset yang terdiri dari:
- Metadata buku: Book-Title, Book-Author, Year-Of-Publication
- Informasi pengguna: User-ID, Location, Age
- Rating buku dari pengguna: Book-Rating

Sumber dataset: https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset/data

## Metode yang Digunakan

### Content-Based Filtering (CBF)
- Menggunakan TF-IDF vectorization dari judul buku
- Menghitung kemiripan antar buku menggunakan cosine similarity
- Rekomendasi berdasarkan buku yang disukai user sebelumnya

### Collaborative Filtering (CF)
- Menggunakan Neural Network dengan Keras
- Menggunakan user-item embedding dan dot product untuk prediksi rating
- Model dilatih untuk meminimalkan Root Mean Squared Error (RMSE)

## Arsitektur Model CF

- Embedding Layer untuk User dan ISBN
- Bias Embedding untuk setiap entitas
- Dot Product antar embedding
- Sigmoid Activation agar output dalam range [0, 1]

## Evaluation Results

### Content-Based Filtering
- Metrik: Precision@5
- Hasil Evaluasi:
  - Anchor Book: See Jane Run
  - Precision@5 = 0.80

### Collaborative Filtering
- Metrik: RMSE
- RMSE Validasi: 0.1833
- Model berhenti di epoch ke-6 karena early stopping

## Perbandingan Metode

| Aspek                  | Content-Based Filtering             | Collaborative Filtering                   |
|------------------------|-------------------------------------|-------------------------------------------|
| Data yang Dibutuhkan   | Metadata item (judul, penulis)      | Riwayat interaksi user-item               |
| Cold Start             | Cocok untuk item baru               | Tidak cocok untuk user/item baru          |
| Personalization        | Terbatas pada konten                | Sangat personal, berdasarkan pengguna serupa |
| Kompleksitas           | Sederhana                           | Kompleks, perlu training model            |

## Conclusion and Recommendation

- Content-Based Filtering cocok untuk situasi minim data user (cold start).
- Collaborative Filtering unggul dalam rekomendasi yang dipersonalisasi.
- Hybrid Recommender System direkomendasikan untuk menggabungkan kekuatan keduanya dan mengurangi kelemahan masing-masing.

## How to Run

1. Clone repo ini
   ```bash
   git clone https://github.com/username/book-recommender.git
   cd book-recommender
   ```
2. Install dependencies
   ```
   pip install -r requirements.txt
   ```
3. jalan notebook di Jupyter Notebook/Google Colab
4. 

   

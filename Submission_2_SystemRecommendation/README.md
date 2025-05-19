# Project Overview
Perkembangan pesat teknologi informasi telah mengubah cara masyarakat dalam mengakses hiburan, termasuk film. Dengan banyaknya layanan streaming seperti Netflix, Disney+, dan Amazon Prime Video, pengguna dihadapkan pada ribuan pilihan judul film yang terus bertambah. Di tengah jumlah pilihan yang melimpah, pengguna sering mengalami kesulitan dalam menentukan film yang sesuai dengan selera mereka. Oleh karena itu, dibutuhkan suatu sistem yang mampu memberikan rekomendasi secara otomatis dan personal. Sistem ini dikenal sebagai sistem rekomendasi film (movie recommendation system). Sistem rekomendasi bertujuan untuk membantu pengguna menemukan item (dalam hal ini film) yang relevan berdasarkan preferensi atau perilaku mereka. Dalam penelitian ini, dua metode utama digunakan sebagai pendekatan dalam membangun sistem rekomendasi, yaitu Content-Based Filtering (CBF) dan Collaborative Filtering (CF).

Metode Content-Based Filtering merekomendasikan film berdasarkan karakteristik yang dimiliki film itu sendiri, seperti genre, sutradara, aktor, atau sinopsis. Sistem ini bekerja dengan menganalisis film yang pernah disukai oleh pengguna, lalu mencari film lain yang memiliki kemiripan dalam konten. Keunggulan dari metode ini adalah kemampuannya untuk memberikan rekomendasi secara personal tanpa membutuhkan data dari pengguna lain. Namun, metode ini memiliki keterbatasan dalam hal keberagaman rekomendasi karena cenderung merekomendasikan item yang serupa. Di sisi lain, Collaborative Filtering memanfaatkan data interaksi antar pengguna, seperti penilaian (rating) atau riwayat tontonan. Metode ini bekerja dengan mencari kesamaan antar pengguna (user-based) atau antar item (item-based), lalu merekomendasikan film yang disukai oleh pengguna lain dengan preferensi serupa. Keunggulan utama dari metode ini adalah kemampuannya menemukan hubungan yang tidak terlihat secara eksplisit dalam konten. Namun, metode ini juga menghadapi tantangan seperti cold start problem dan sparsity, terutama ketika data pengguna terbatas.

Dengan melakukan dua percobaan menggunakan metode Content-Based Filtering dan Collaborative Filtering, penelitian ini bertujuan untuk mengevaluasi keefektifan masing-masing pendekatan dalam memberikan rekomendasi film yang relevan. Hasil dari kedua percobaan ini diharapkan dapat memberikan pemahaman yang lebih baik tentang kelebihan dan kelemahan masing-masing metode, serta membantu menentukan pendekatan yang paling sesuai untuk sistem rekomendasi film berbasis data pengguna.

# Business Understanding
## Problem Statement
Dari latar belakang diatas, adapun rumusan masalah yang dihadapi sebagai berikut :
- Bagaimana mengembangkan sistem rekomendasi film menggunakan metode Content Based Filtering?
- Bagaimana mengembangkan sistem rekomnedasi film menggunakan metode Collaborative Filtering?
## Goals
Berdasarkan rumusan masalah yang telah dipaparkan di atas, maka proyek penelitian ini memiliki tujuan, yaitu:
- Mengembangkan sistem rekomendasi film dengan pendekatan Content-Based Filtering untuk memberikan saran film yang sesuai dengan preferensi pengguna berdasarkan karakteristik konten film.
- Mengembangkan sistem rekomendasi film dengan pendekatan Collaborative Filtering untuk memberikan rekomendasi berdasarkan pola kesamaan perilaku antar pengguna.

## Solustion Statement
Untuk menjawab permasalahan dalam pengembangan sistem rekomendasi film, solusi yang diusulkan adalah membangun dua model rekomendasi menggunakan pendekatan berbeda, yaitu Content-Based Filtering dan Collaborative Filtering:
- **Content-Based Filtering**: Sistem akan menganalisis karakteristik film berdasarkan genre. Berdasarkan preferensi pengguna sistem akan menghitung kemiripan antara film  dengan film lainnya menggunakan teknik seperti TF-IDF dan cosine similarity, sehingga dapat memberikan rekomendasi yang relevan secara personal tanpa bergantung pada data pengguna lain.
- **Collaborative Filtering**: Sistem akan menggunakan data interaksi pengguna seperti rating tiap film, untuk mengidentifikasi pola kesamaan antar pengguna atau antar film. Teknik yang digunakan dalam sistem ini akan memanfaatkan cosine similarity dan item based filtering untuk memprediksi preferensi pengguna terhadap film yang belum ditonton.
- Menampilkan hasil rekomendasi tiap metode yang digunakan
  
# Data Understanding
Dataset yang digunakan menggunakan diambil dari kaggle yang dapat diakses [disini](https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system). Dataset ini memiliki 2 file terpisah yaitu `movies.csv` dan `ratings.csv`. Dataset ini dipublikasikan oleh [Nicoleta Cilibiu](https://www.kaggle.com/nicoletacilibiu) pada tahun 2023. Dataset ini berisi informasi terkait Film seperti tahun release, user rating, dan lain-lain.


| Jenis    | Keterangan                                                |
|----------|-----------------------------------------------------------|
| Title    | Movies & Ratings for Recommendation System                                        |
| Source   |[Kaggle](https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system)                                                  |
| Publisher | [Nicoleta Cilibiu](https://www.kaggle.com/dbdmobile)                                                   |
| License  | CC0: Public Domain      |
| Visibility | Publik                                                  |
| Usability | 9.41                                                     |

## Variable Dataset
1. Pada file `movies.csv` terdapat 9737 rows dan 3 columns
   - `movieId` : memuat nomor ID film
   - `title` : memuat judul film
   - `genres` : memuat genre film
2. Pada file `ratings.csv` terdapat 100836 rows dan 4 columns
   - `userId` : memuat nomor ID users
   - `movieId` : memuat nomor ID film
   - `rating` : memuat rating tiap user dengan peningkatan setengah bintang dalam rentang 0.5 - 5 bintang
   - `timestamp` : memuat waktu user ketika memberi rating

# Data Preparation
# Modeling
# Evaluation

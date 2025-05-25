# Project Overview
Perkembangan pesat teknologi informasi telah mengubah cara masyarakat dalam mengakses hiburan, termasuk film. Dengan banyaknya layanan streaming seperti Netflix, Disney+, dan Amazon Prime Video, pengguna dihadapkan pada ribuan pilihan judul film yang terus bertambah. Di tengah jumlah pilihan yang melimpah, pengguna sering mengalami kesulitan dalam menentukan film yang sesuai dengan selera mereka. Oleh karena itu, dibutuhkan suatu sistem yang mampu memberikan rekomendasi secara otomatis dan personal. Sistem ini dikenal sebagai sistem rekomendasi film (movie recommendation system). Sistem rekomendasi bertujuan untuk membantu pengguna menemukan item (dalam hal ini film) yang relevan berdasarkan preferensi atau perilaku mereka. Dalam penelitian ini, dua metode utama digunakan sebagai pendekatan dalam membangun sistem rekomendasi, yaitu Content-Based Filtering (CBF) dan Collaborative Filtering (CF).

Metode Content-Based Filtering merekomendasikan film berdasarkan karakteristik yang dimiliki film itu sendiri, seperti genre, sutradara, aktor, atau sinopsis. Sistem ini bekerja dengan menganalisis film yang pernah disukai oleh pengguna, lalu mencari film lain yang memiliki kemiripan dalam konten. Keunggulan dari metode ini adalah kemampuannya untuk memberikan rekomendasi secara personal tanpa membutuhkan data dari pengguna lain. Namun, metode ini memiliki keterbatasan dalam hal keberagaman rekomendasi karena cenderung merekomendasikan item yang serupa. Di sisi lain, Collaborative Filtering memanfaatkan data interaksi antar pengguna, seperti penilaian (rating) atau riwayat tontonan. Metode ini bekerja dengan mencari kesamaan antar pengguna (user-based) atau antar item (item-based), lalu merekomendasikan film yang disukai oleh pengguna lain dengan preferensi serupa. Keunggulan utama dari metode ini adalah kemampuannya menemukan hubungan yang tidak terlihat secara eksplisit dalam konten. Namun, metode ini juga menghadapi tantangan seperti cold start problem dan sparsity, terutama ketika data pengguna terbatas.

Dengan melakukan dua percobaan menggunakan metode Content-Based Filtering dan Collaborative Filtering, penelitian ini bertujuan untuk mengevaluasi keefektifan masing-masing pendekatan dalam memberikan rekomendasi film yang relevan. Hasil dari kedua percobaan ini diharapkan dapat memberikan pemahaman yang lebih baik tentang kelebihan dan kelemahan masing-masing metode, serta membantu menentukan pendekatan yang paling sesuai untuk sistem rekomendasi film berbasis data pengguna.

# Business Understanding
## Problem Statement
Dari latar belakang diatas, adapun rumusan masalah yang dihadapi sebagai berikut :
- Bagaimana mengembangkan sistem rekomendasi film menggunakan metode Content Based Filtering?
- Bagaimana mengembangkan sistem rekomnedasi film menggunakan metode Collaborative Filtering?
- Bagaimana hasil dan evaluasi model dalam mengembangkan sistem rekomendasi film yang sesuai dengan metode Content Based Filtering dan Collaborative Filtering?
  
## Goals
Berdasarkan rumusan masalah yang telah dipaparkan di atas, maka proyek penelitian ini memiliki tujuan, yaitu:
- Mengembangkan sistem rekomendasi film dengan pendekatan Content-Based Filtering untuk memberikan saran film yang sesuai dengan preferensi pengguna berdasarkan karakteristik konten film.
- Mengembangkan sistem rekomendasi film dengan pendekatan Collaborative Filtering untuk memberikan rekomendasi berdasarkan pola kesamaan perilaku antar pengguna.
- Menganalisis hasil dan evaluasi model dalam mengembangkan sistem rekomendasi film.
  
## Solustion Statement
Untuk menjawab permasalahan dalam pengembangan sistem rekomendasi film, solusi yang diusulkan adalah membangun dua model rekomendasi menggunakan pendekatan berbeda, yaitu Content-Based Filtering dan Collaborative Filtering:
- **Content-Based Filtering**: Sistem akan menganalisis karakteristik film berdasarkan genre. Berdasarkan preferensi pengguna sistem akan menghitung kemiripan antara film  dengan film lainnya menggunakan teknik seperti TF-IDF dan cosine similarity, sehingga dapat memberikan rekomendasi yang relevan secara personal tanpa bergantung pada data pengguna lain.
- **Collaborative Filtering**: Sistem akan menggunakan data interaksi pengguna seperti rating tiap film, untuk mengidentifikasi pola kesamaan antar pengguna atau antar film. Teknik yang digunakan dalam sistem ini akan memanfaatkan cosine similarity dan item based filtering untuk memprediksi preferensi pengguna terhadap film yang belum ditonton.
  
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
1. Pada file `movies.csv` terdapat 9742 rows dan 3 columns
   - `movieId` : memuat nomor ID film
   - `title` : memuat judul film
   - `genres` : memuat genre film
2. Pada file `ratings.csv` terdapat 100836 rows dan 4 columns
   - `userId` : memuat nomor ID users
   - `movieId` : memuat nomor ID film
   - `rating` : memuat rating tiap user dengan peningkatan setengah bintang dalam rentang 0.5 - 5 bintang
   - `timestamp` : memuat waktu user ketika memberi rating

## Exploratory Data Analysis
Proses EDA dilakukan untuk menganalisis dataset untuk menemukan insight.

### Univariate Analysis

  ![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/EDA.png?raw=true)

Dari hasil analisis, terdapat total 100.836 data rating yang diberikan oleh 610 user terhadap 9.724 film. Setiap user memberikan rata-rata sekitar 165 rating, menunjukkan bahwa user dalam dataset ini tergolong aktif. Namun, setiap film hanya menerima rata-rata sekitar 10 rating, yang mengindikasikan kemungkinan adanya ketimpangan distribusi rating antar film, beberapa film mungkin sangat populer sementara banyak lainnya hanya menerima sedikit rating. Hal ini dapat memengaruhi performa sistem rekomendasi, terutama dalam menghadapi masalah cold start untuk film dengan sedikit rating.
  
# Data Preparation
## Data Cleaning
Pada proses data cleaning, saya melakukan data cleaning pada data movies.csv dan ratings.csv. setelah kedua data tersebut dirasa sudah terlihat cukup baik, saya melakukan merging dataframe pada kedua data tersebut dan menjadikannya sebagai dataframe yang utuh untuk mengembangkan sistem rekomendasi. Berikut langkah-langkahnya:

A. Data Cleaning `movies.csv`

   Pada data `movies.csv` pada variable atau feature `title` terdapat judul film dan tahun release. Hal ini diperlukan
   penanganan khusus untuk memisahkan antara judul film dengan tahun rilis agar tidak terjadi permasalahan yang tidak
   diinginkan pada proses training model. dimana, tahun rilis dari setiap film akan dipisahkan ke dalam kolom tersendiri.
   
B. Data Cleaning `ratings.csv`

   Pada data `ratings.csv` terdapat feature yang tidak digunakan dalam tahap modeling sistem rekomendasi menggunakan metode
   Content Based Filtering maupun Collaborative Filtering, feature tersebut adalah `timestamp` yang mana `timestamp` hanya
   menampilkan kapan user memberikan rating, sehingga saya mendrop/menghapus feature tersebut.
   
C. Data Merge `movies_df` dengan `ratings_df`

   Penggabungan dilakukan dengan melakukan merge pada kedua dataframe antara movies dengan ratings menjadi satu dataframe
   yang utuh dan mengassignnya kedalam variabel `films`.

D. Data Cleaning `films`
   
1. Handling Missing Value
  
  Setelah data digabung, terdapat beberapa feature yang memiliki null values atai nilai NaN, karena hanya 18 rows yang
  terdeteksi nilai NaN sehingga saya mengahpusnya. Saat saya mengecek pada kolom `genres` terdapat beberapa film yang
  tidak memiliki genre `(no genres listed)`, karena nanti akan digunakan untuk modeling metode `Content Based Filtering`
  film-film yang tidak memiliki genre akan dihapus agar model bisa memberikan rekomendasi yang lebih relevan.
  
2. Memisahkan Dataframe menjadi 2 variable yang berbeda
  
  Karena tujuan awal adalah membuat modeling dengan 2 metode yang berbeda, sehingga dataframe dibedakan agar memudahkan
  pada proses modeling, karena tiap metode memiliki treatment yang berbeda. Dataframe 1 untuk metode `Content Based
  Filtering` menggunakan nama `content_df` sedangkan untuk `Collaborative Filtering` dengan nama `collab_df`
  
3. Data Cleaning
  - Dataframe `Content Based Filtering` / `content_df`
    - Menghapus Data Duplikat
      
      Pada dataframe untuk model `Content Based Filtering` judul film yang duplikat harus dihapus, karena pada model
      `Content Based Filtering` tidak membutuhkan rating tiap usernya.
      
    - Menghapus Whitespace pada Kolom `title` dan `genres`
      
      Pada dataframe `content_df` terdapat spasi tambahan atau *whitespace* pada kolom `title` dan `genres`, karena ini akan
      mengganggu dalam proses modeling, sehingga spasi tambahan ini dihapus dengan `.str.strip()`
      
    - TF-IDF Vektorisasi
      
      Proses term frequency-inverse document frequency (TF-IDF) diperlukan untuk menemukan representasi kata yang penting
      dalam kolom genre. Pada metode `Content Based Filtering`, proses vectorizer dilakukan dengan memanfaatkan function
      `tfidfvectorizer()` yang telah tersedia pada library scikit-learn.

  - Dataframe `Collaborative Filtering` / `collab_df`
    - Menghapus Whitespace pada Kolom `title`

      Sedikit berbeda penanganan untuk Whitespace pada metode `Collaborative Filtering`, karena pada metode ini tidak
      membutuhkan feature `genres` jadi yang perlu dihapus hanya feature `title` dengan `.str.strip()`.
      
    - Membuat Pivot Table
    - 
      Untuk membangun model `Collaborative Filtering`, saya hanya menggunakan tiga fitur utama, yaitu `userId`, `title`, dan
      `rating`. Oleh karena itu, saya membuat sebuah pivot table dari ketiga fitur tersebut dengan kode berikut:
      
      ```Ruby
      collab_df = collab_df.pivot_table(index="userId", columns="title", values="rating")
      collab_df
      ```
      Setelah dilakukan pivot table terdapat banyak nilai NaN pada rating tiap filmnya, dimana maksud NaN adalah user
      tersebut belum merating film tersebut, sehingga kita isi dengan nilai 0 untuk merepresentasikan film tersebut belum
      dirating oleh user tersebut. Serta jika dilihat dari Exploratory Data sebelumnya, setiap film hanya menerima rata-rata
      sekitar 10 rating dari user, jadi kita asumsikan banyak film yang hanya di rating 1-5 oleh user yang membuat rata-rata
      rating cukup rendah, sehingga kita abaikan saja film-film yang dirating <5 user. Berikut adalah code untuk inputing
      nilai NaN dan menghapus film yang dirating 1-5:
      
      ```Ruby
      collab_df = collab_df.dropna(thresh=5, axis=1).fillna(0)
      collab_df
      ```

# Modeling
Pada proyek ini, pendekatan yang dipakai untuk mengembangkan model dalam sistem rekomendasi adalah` Content-Based Filtering` dan `Collaborative Filtering`.

A. Content-Based Filtering 

Konsep dasar dari content-based filtering adalah memberikan rekomendasi item dengan memperhatikan kemiripan dari item yang disukai oleh pengguna berdasarkan aktivitas pengguna tersebut di masa lalu. Pada proyek kali ini, saya akan menerapkan pendekatan `content-based filtering` untuk mengembangkan model sistem rekomendasi film sesuai dengan goals dari proyek ini. Ada beberapa tahapan yang saya lakukan, diantaranya sebagai berikut:

1. Cosine Similarity

   Cosine similarity digunakan untuk mengukur tingkat kemiripan antar film. Dalam proyek ini, perhitungan kesamaan tersebut
   dilakukan dengan memanfaatkan fungsi `cosine_similarity()` dari pustaka scikit-learn. Tahapan ini menjadi bagian krusial
   dalam metode `content-based filtering`, karena metode ini bekerja berdasarkan prinsip kemiripan antar item untuk
   memberikanrekomendasi yang relevan. Hasil dari perhitungan cosine similarity akan berupa sebuah matriks kesamaan, yang
   kemudiandapat dikonversi menjadi bentuk dataframe untuk dianalisis lebih lanjut.

   ![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/cosine_CBF.png?raw=true)

2. Membuat Custom Functions

   Tahap akhir dalam proses ini adalah membangun custom functions untuk menghasilkan rekomendasi berdasarkan data input yang
   diberikan. Fungsi ini bekerja dengan mengambil nilai kemiripan dari film yang dicari, lalu menyimpan film-film yang
   paling mirip ke dalam variabel closest. Parameter K ditentukan untuk menampilkan top-K recommendation berdasarkan tingkat
   kemiripan tertinggi. Film yang menjadi acuan pencarian akan dihapus dari daftar agar tidak direkomendasikan kepada
   dirinya sendiri. Pada langkah terakhir, fungsi akan mengembalikan hasil dalam bentuk dataframe, di mana isi dari
   dataframe tersebut merupakan daftar rekomendasi film berdasarkan tingkat kesamaan tertinggi.

   ```Ruby
       # function recommendations
    def film_recommendations(title, similarity_data=cosine_sim_df, items=data[['title', 'genres']], k=5):
        # get data index
        index = similarity_data.loc[:,title].to_numpy().argpartition(
            range(-1, -k, -1))
    
        # retrieve data from an existing index
        closest = similarity_data.columns[index[-1:-(k+2):-1]]
    
        # drop title you want to search
        closest = closest.drop(title, errors='ignore')
    
        return pd.DataFrame(closest).merge(items).head(k)
   ```

3. Get Recommendation

   ![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/get_recomen_CBF.png?raw=true)
   
  Dari film `Saving Christmas` dengan genre `children` `comedy`, sistem akan merekomendasikan film yang sesuai dengan 
  genre yang paling mirip, diantaranya 5 film rekomendasi seperti berikut

  ![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/get_recomen_CBF2.png?raw=true)


B. Collaborative Filtering

Collaborative filtering merupakan metode sistem rekomendasi yang memberikan saran berdasarkan aktivitas dan preferensi pengguna lain yang memiliki kemiripan perilaku atau selera dengan pengguna target. Konsep dasarnya adalah: jika dua pengguna memiliki preferensi yang mirip di masa lalu, maka kemungkinan besar mereka juga akan menyukai hal yang sama di masa depan. Pada proyek ini collaborative filtering yang digunakan menggunakan `item-based filtering` Ada beberapa tahapan yang saya lakukan, diantaranya sebagai berikut

1. Cosine Similarity
   
   Pada tahap ini, dilakukan proses standarisasi terhadap data rating menggunakan fungsi `standardize()`, yaitu dengan
   mengurangi nilai rata-rata pada setiap baris dan membaginya dengan selisih antara nilai maksimum dan minimum, agar skala
   data menjadi seragam. Data yang telah distandarisasi (data_std) kemudian digunakan untuk menghitung item-item similarity
   menggunakan fungsi `cosine_similarity()`. Hasil perhitungan tersebut dikonversi menjadi DataFrame dengan indeks dan kolom
   yang sesuai dengan nama item (misalnya judul film), sehingga menghasilkan matriks kesamaan antar item yang siap digunakan
   untuk proses rekomendasi.

   ```Ruby
   def standardize(row):
       return (row - row.mean()) / (row.max() - row.min())
    
   data_std = collab_df.apply(standardize)
   item_similarity = cosine_similarity(data_std.T)
   item_similarity = pd.DataFrame(item_similarity, index=collab_df.columns, columns=collab_df.columns)
   item_similarity
   ```
   
2. Membuat Custom Function
   
   Pada tahap ini, dibuat fungsi `get_similar_movies()` yang bertujuan untuk menghitung skor kemiripan film berdasarkan satu
   film yang diberikan oleh pengguna beserta rating-nya. Fungsi akan mengecek apakah nama film ada dalam matriks kesamaan
   `item_similarity`. Jika ada, maka skor kemiripan film dikalikan dengan `(user_rating - 2.5)` untuk menyesuaikan pengaruh
   rating terhadap hasil rekomendasi (misalnya, rating di atas 2.5 memberi pengaruh positif, sedangkan di bawah 2.5 memberi
   pengaruh negatif). Hasilnya kemudian dikonversi menjadi array satu dimensi yang merepresentasikan skor kemiripan yang
   sudah disesuaikan terhadap semua film.

   ```Ruby
   def get_similar_movies(movie_name, user_rating):
       if movie_name not in item_similarity:
           print(f"Not Found: {movie_name}")
           return
       similar_score = item_similarity[movie_name] * (user_rating-2.5)  # manipulate the similar score using given rating by
       user
       similar_score = pd.DataFrame(similar_score).T
       return np.array(similar_score).reshape(-1)
    
    print(get_similar_movies("Zodiac", 3.5))
   ```

3. Membuat User Profile
   
   Sebelum mendemokan sistem rekomendasi, saya akan membuat user profile terlebih dahulu.
   ```Ruby
    usamah_profile = [
        ("Zodiac", 3.5),
        ("Muse, The", 2.0),
        ("Rambo: First Blood Part II", 2.5),
        ("Doc Hollywood", 4.5),
        ("Erin Brockovich", 5.0),
        ("Fantasia", 3.0),
        ("Fun with Dick and Jane", 4.5),
        ("Brothers", 5.0),
        ("Indecent Proposal", 4.0)
    ]
   ```

4. Mendapatkan Rekomendasi Berdasarkan User Profile

   Setelah user profil telah dibuat, selanjutnya mendapatkan rekomendasi berdasarkan profilenya

   ```Ruby
   similar_movies = pd.DataFrame(columns=collab_df.columns)

   for i, (movie, rating) in enumerate(usamah_profile):
       sim_scores = get_similar_movies(movie, rating)
       similar_movies.loc[i] = sim_scores
    
   # Profil user (film yang sudah ditonton)
   watched_movies = [movie for movie, rating in usamah_profile]
   recommendation_scores = similar_movies.sum().sort_values(ascending=False)
   recommendation_scores = recommendation_scores.drop(labels=watched_movies, errors='ignore')
    
   print(recommendation_scores[:10])
   ```

   Dari kode diatas akan menampilkan rekomendasinya seperti digambar dibawah ini.

   ![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/hasil_rekomendasi_CF.png?raw=true)

   Hasil menampilkan top 10 rekomendasi yang mungkin juga akan disukai oleh Usamah (user profile)


C. Perbandingan Kekurangan dan Kelebihan Metode `Content-Based Filtering` dengan `Collaborative Filtering`

1. `Content-Based Filtering`

| Aspek | Kelebihan | Kekurangan |
|-------|-----------|------------|                                        
| Personalisasi | Memberikan rekomendasi yang spesifik dan relevan sesuai preferensi pengguna | Terlalu bergantung pada data historis pengguna, sehingga bisa kurang bervariasi |
| Cold Start (Item Baru) | Dapat merekomendasikan item baru selama memiliki fitur yang jelas | Sulit menangani pengguna baru yang belum memiliki histori interaksi |
| Independensi Data | Tidak memerlukan data dari pengguna lain | Tidak bisa memanfaatkan pola umum dari pengguna lain |

2. `Collaborative Filtering`

| Aspek | Kelebihan | Kekurangan |
|-------|-----------|------------|                                        
| Personalisasi | Memberikan rekomendasi berdasarkan kesamaan antar pengguna atau item | Kurang akurat jika pengguna atau item memiliki data interaksi yang sedikit |
| Explorasi | Dapat merekomendasikan item yang belum pernah dilihat pengguna (lebih variatif) | Rawan memberikan saran yang tidak relevan jika datanya noisy atau tidak akurat |
| Kebutuhan Data | Tidak perlu tahu detail fitur item (hanya butuh interaksi pengguna) | Membutuhkan banyak data interaksi untuk menghasilkan rekomendasi yang baik |


# Evaluation

Evaluasi dilakukan untuk mengukur sejauh mana performance atau kinerja dari model sistem rekomendasi. Pada proyek ini, evaluasi diukur menggunakan metriks evaluasi sesuai dengan pendekatan yang dipakai dalam pengembangan sistem rekomendasi.

A. `Content-Based Filtering`

Pada pendekatan Content-Based Filtering, performance model diukur menggunakan Metode `Evaluasi Genre-Based Similarity Score`. metode ini merupakan ukuran yang mengkuantifikasi kesamaan antara dua atau lebih vektor.

![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/rumus_evaluasi_CBF.png?raw=true)

Contoh perhitungan :
Misalnya
- input film : `Saving Christmas`
- genre : `children` `comedy`
- total genre : 2

Maka :

![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/hasil_rumus_evaliasi.png?raw=true)

Hasil Rekomendasi :

![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/hasil_evaluasi_CBF.png?raw=true)

Dari hasil rekomendasi dapat diketahui bahwa, 5 film yang direkomendasikan mendapatkan similarity 1 karena genre dari 5 film tersebut sama dengan film `Saving Christmas` yaitu `children` `comedy`.

B. `Collaborative Filtering` 

Pada pendekatan `Collaborative Filtering` peforma model diukur dengan metode `Manual Relevance Evaluation using Pearson Correlation`. Metode ini akan mengukur tingkat kesesuaian antara skor prediksi sistem rekomendasi dan penilaian manual dari pengguna terhadap hasil rekomendasi. Penilaian manual dilakukan secara subjektif oleh pengguna berdasarkan relevansi film yang disarankan terhadap preferensi pribadinya. Berikut adalah beberapa tahapan evaluasinya:

1. Menentukan Hasil Rekomendas

Setelah sistem collaborative filtering dibangun dan menghasilkan rekomendasi, diambil beberapa film teratas untuk dinilai:

```Ruby
top_recommendations = recommendation_scores[:10].index.tolist()
```

2. Menyusun Manual Relevance (Penilaian Manual)

Pengguna memberikan penilaian terhadap film yang direkomendasikan, berdasarkan tingkat relevansinya dengan selera pribadi, menggunakan skala 1–5:

```Ruby
# Buat penilaian manual untuk evaluasi (1 = tidak relevan, 5 = sangat relevan)
manual_relevance = {
    "Frequency": 5,
    "Meatballs": 4,
    "Unstoppable": 4,
    "Night on Earth": 2,
    "Dragonslayer": 5,
    "Fly, The": 3,
    "Walk the Line": 2,
    "Chasing Liberty": 5,
    "Pee-wee's Big Adventure": 4,
    "Shrek 2": 3,
}
```

3. Menyusun Data Evaluasi

Menggabungkan skor hasil prediksi sistem dan skor manual dari pengguna ke dalam sebuah DataFrame:

```Ruby
evaluation_df = pd.DataFrame({
    'Predicted Score': recommendation_scores[manual_relevance.keys()],
    'Manual Relevance': pd.Series(manual_relevance)
})
```

4. Normalisasi Skor Prediksi

Agar dapat dibandingkan dengan skor manual, skor prediksi dari sistem dinormalisasi:

![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/normalisasi_CF.png?raw=true)

5. Menghitung Korelasi Pearson

Untuk mengukur hubungan antara skor prediksi sistem dan relevansi manual, digunakan korelasi Pearson (Pearson Correlation Coefficient).

![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/Korelasi_paerson_CF.png?raw=true)

6. Hasil Evaluasi

Berikut adalah hasil evaluasi `Collaborative Filtering` :

![img alt](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_2_SystemRecommendation/img/Hasil_evaluasi_CF.png?raw=true)

Dari hasil evaluasi korelasi hanya 0.17 menunjukkan bahwa sistem hanya memiliki hubungan lemah dengan preferensi pengguna. Ini berarti bahwa rekomendasi yang dihasilkan belum terlalu sesuai, dan perlu dilakukan perbaikan, misalnya:
- Menambah jumlah film yang telah dirating oleh pengguna
- Menggabungkan metode content-based dan collaborative filtering
- Menambahkan fitur genre, tahun, dan sinopsis dalam rekomendasi


## Kesimpulan Evaluasi

Dari hasil evaluasi dari metode `Content-Based Filtering` dan `Collaborative Filering`, hasil terbaik menunjukkan pada metode `Content-Based Filtering`, dimana sistem dapat menemukan genre yang sesuai dengan film yang telah di inputkan, sedangkan untuk `Collaborative Filtering` belum akurat dalam memberikan rekomendasi.

# Referensi
[1] Bobadilla, J., Ortega, F., Hernando, A., & Gutiérrez, A. (2013). Recommender systems survey. Knowledge-Based Systems, 46, 109–132. https://doi.org/10.1016/j.knosys.2013.03.012

[2] Ricci, F., Rokach, L., & Shapira, B. (2015). Recommender Systems Handbook (2nd ed.). Springer. https://doi.org/10.1007/978-1-4899-7637-6

[3] Aggarwal, C. C. (2016). Recommender Systems: The Textbook. Springer. https://doi.org/10.1007/978-3-319-29659-3

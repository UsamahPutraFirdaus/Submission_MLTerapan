# **Laporan Proyek Machine Learning - Usamah Putra Firdaus**

## **Domain Proyek**

Diabetes merupakan salah satu penyakit kronis yang paling banyak diderita di seluruh dunia. Berdasarkan data dari World Health Organization (WHO), jumlah penderita diabetes terus meningkat setiap tahunnya, baik di negara maju maupun berkembang. Penyakit ini seringkali tidak menunjukkan gejala pada tahap awal, sehingga banyak penderita yang tidak menyadari bahwa mereka mengidap diabetes hingga komplikasi muncul. Kondisi ini menyebabkan keterlambatan dalam penanganan yang dapat memperburuk kesehatan pasien.

Dalam era digital saat ini, kemajuan teknologi di bidang data science dan machine learning membuka peluang besar untuk mendukung deteksi dini penyakit, termasuk diabetes. Dengan memanfaatkan data kesehatan seperti kadar glukosa darah, tekanan darah, indeks massa tubuh (BMI), dan faktor risiko lainnya, kita dapat membangun sistem prediksi yang membantu tenaga medis maupun individu dalam mengidentifikasi risiko diabetes secara lebih cepat dan akurat.

Proyek ini bertujuan untuk membangun model predictive analytics yang mampu mendeteksi kemungkinan seseorang menderita diabetes berdasarkan [data kesehatan](https://www.kaggle.com/datasets/nanditapore/healthcare-diabetes). Dengan pendekatan ini, diharapkan dapat mendukung pengambilan keputusan yang lebih tepat dalam pencegahan maupun penanganan awal diabetes, sehingga menekan angka penderita dan meningkatkan kualitas hidup masyarakat.

## Business Understanding
### Problem Statements
Dari latar belakang diatas, maka rumusan masalah yang akan dibahas pada proyek ini sebagai berikut:
- Apakah dengan banyaknya jumlah kehamilan berpengaruh terhadap risiko menderita diabetes?
- Model machine learning apa yang memiliki akurasi tertinggi dan tingkat kesalahan prediksi paling rendah dalam mendeteksi penderita diabetes?

### Goals
Berdasarkan Problem Statement yang telah disebutkan, berikut adalah tujuan/goals dari proyek ini sebagai berikut:
- Menganalisis apakah terdapat pengaruh antara jumlah kehamilan seseorang terhadap kemungkinan menderita diabetes.
- Membandingkan performa beberapa model *machine learning* untuk menemukan model dengan akurasi terbaik dan kesalahan prediksi paling minim.

### Solution Statements
- Melakukan Exploratory Data Analysis (EDA) untuk memvisualisasikan jumlah kehamilan berdasarkan kelompok umur, dan penderita diabetes berdasarkan umur
- Membandingkan 3 performa model *Machine Learning* yaitu Logistic Regression, Decision Tree, dan Random Forest
- Melakukan Evaluasi model menggunakan Confusion Matrix untuk melihat mana model yang paling sedikit melakukan kesalahan prediksi

## **Data Understanding**
Dataset yang digunakan untuk memprediksi seseorang yang beresiko mengalami diabetes. Dataset diambil dari kaggle yang dapat diakses [disini](https://www.kaggle.com/datasets/nanditapore/healthcare-diabetes), dataset ini dipubilkasi oleh [Nandita Pore](https://www.kaggle.com/nanditapore) pada tahun 2023. Dataset ini berisi berbagai atribut yang berkaitan dengan kesehatan, yang dikumpulkan secara cermat untuk mendukung pengembangan model prediktif dalam mengidentifikasi individu yang berisiko menderita diabetes.

### Variable Description
- Id: Identitas unik untuk setiap entri data.
- Pregnancies: Jumlah kehamilan yang pernah dialami.
- Glucose: Konsentrasi glukosa plasma selama 2 jam dalam tes toleransi glukosa oral.
- BloodPressure: Tekanan darah diastolik (mm Hg).
- SkinThickness: Ketebalan lipatan kulit trisep (mm).
- Insulin: Kadar insulin serum selama 2 jam (mu U/ml).
- BMI: Indeks massa tubuh (berat dalam kg / tinggi dalam m²).
- DiabetesPedigreeFunction: Skor genetik risiko diabetes berdasarkan silsilah keluarga.
- Age: Usia dalam tahun.
- Outcome: Klasifikasi biner yang menunjukkan adanya (1) atau tidak adanya (0) diabetes.

### Exploratory Data Analysis (EDA)
**A. EDA - Univariete Analysis**
1. Distribusi Usia

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/distribusi%20usia.png?raw=true)
   
   **Interpretasi Visualisasi Distribusi Usia**
   
   - Dataset ini didominasi oleh orang-orang berusia muda, terutama awal 20-an.
   - cukup sedikit orang yang berusia di atas 60 tahun.

3. Distribusi Jumlah Orang perKelompok Usia

      ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/distribusi%20jumlah%20orang%20per%20kelompok.png?raw=true)

   >```Ruby
   ># Buat kategori umur
   >bins = [20, 30, 40, 50, 60, 70, 80]
   >labels = ['20-30', '31-40', '41-50', '51-60', '61-70', '71-85']
   >df['AgeGroup'] = pd.cut(df['Age'], bins=bins, labels=labels, right=True)
   >```
   Kode diatas digunakan untuk membuat kelompok umur
   
   **Interpretasi Visualisasi Distribusi Jumlah Orang perKelompok Usia**
   
   - Kelompok usia muda (20–30) adalah mayoritas populasi.
   - Populasi mengecil seiring bertambahnya usia, terutama di atas 50 tahun.
     
4. Perbandingan Jumlah Penderita Diabetes

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/perbandingan%20penderita%20diabetes.png?raw=true)

   **Interpretasi Visualisasi Perbandingan Jumlah Penderita Diabetes**
   
   - Mayoritas orang dalam dataset **tidak** menderita diabetes.
   - Namun, sekitar 1 dari 3 orang ternyata menderita diabetes, yang masih cukup signifikan secara proporsi.
   
6. Perbandingan Jumlah Kehamilan paling banyak dengan Paling Sedikit

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/distribusi%20kehamilan%20berdasarkan%20kelompok%20usia.png?raw=true)

   **Interpretasi Visualisasi Perbandingan Jumlah Kehamilan Paling Banyak dengan Paling Sedikit**
   
   - Distribusi jumlah kehamilan condong ke angka kecil: Mayoritas orang memiliki kehamilan 0–4 kali.
   - Jumlah kehamilan lebih dari 10 berpotensi sebagai outlier
   
**B. EDA - Multivariete Analysis**
1. Rata-rata Kehamilan Berdasarkan perKelompok Usia

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/rata%20rata%20kehamilan%20per%20kelompok%20usia.png?raw=true)

   **Interpretasi Visualisasi Rata-rata Kehamilan Berdasarkan perKelompok Usia**
   
   - Puncak rata-rata kehamilan terjadi pada usia 41–50 tahun, dan menurun setelahnya.
   - Data ini menunjukkan bahwa sebagian besar perempuan mengalami jumlah kehamilan tertinggi di usia pertengahan hingga awal lanjut usia.

3. Jumlah Penderita Diabetes berdasarkan perKelompok Usia

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/jumlah%20penderita%20diabetes%20perkelompok%20usia.png?raw=true)

   **Interpretasi Visualisasi Jumlah Penderita Diabetes berdasarkan perKelompok Usia**

   - Jika dilihat langsung dari visualisasi diatas, usia 20 hingga 30 memiliki penderita diabetes yang sangat banyak. Namun jika melihat dari visualisasi Distribusi Jumlah Orang perKelompok Usia, kelompok usia 20 - 30 memiliki jumlah yang sangat banyak dibandingkan dengan kelompok usia lainnya. Kelompok usia 20-30 hanya sekitar -+ 17% penderita diabetes. Dibandingkan dengan kelompok usia 41-50, tingkat penderita diabetes mencapai hampir 55%

4. Matriks Korelasi antar Kolom

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/matriks%20korelasi.png?raw=true)
   
   **Interpretasi Visualisasi Jumlah Penderita Diabetes berdasarkan perKelompok Usia**
   - Glucose adalah fitur paling signifikan dalam menentukan kemungkinan diabetes.
   - BMI, Age, dan jumlah kehamilan (Pregnancies) juga berkontribusi tetapi tidak sekuat Glucose.

**C. Handling Outliers**
Untuk mengatasi outlier, salah satu metode yang umum digunakan adalah metode IQR (Interquartile Range) dengan visualisasi menggunakan boxplot. Berikut penjelasan mengenai metode IQR dan visualisasi boxplot:

1. Apa itu IQR?
Interquartile Range (IQR) adalah selisih antara kuartil ketiga (Q3) dan kuartil pertama (Q1) dari suatu data. Q1 adalah nilai yang membagi 25% data pertama (bagian bawah), sedangkan Q3 adalah nilai yang membagi 75% data (bagian atas). IQR digunakan untuk menggambarkan sebaran nilai yang berada di tengah 50% data.

2. Langkah-langkah Deteksi Outlier dengan IQR:
- Hitung Q1 dan Q3
   - Q1 adalah nilai pada persentil ke-25 dari data.
   - Q3 adalah nilai pada persentil ke-75 dari data.
- Hitung IQR
   - IQR = Q3 − Q1
- Tentukan Batas Deteksi Outlier
   - Batas Bawah (Lower Bound) = Q1 − 1.5 × IQR
   - Batas Atas (Upper Bound) = Q3 + 1.5 × IQR
- Identifikasi Outlier
   - Nilai yang lebih kecil dari batas bawah atau lebih besar dari batas atas dikategorikan sebagai outlier, yaitu data yang menyimpang jauh dari nilai mayoritas.

3. Visualisasi Boxplot
- Sebelum Outliers Dihapus

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/outliers%20sebelum%20dihapus.png?raw=true)

   Pada kolom `Pregnancies`, `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`, dan `DiabetesPedigreeFunction` terdeteksi cukup banyak outlier. Sementara itu, kolom `Age` juga menunjukkan indikasi adanya outlier. Namun, setelah ditinjau lebih lanjut, nilai-nilai pada kolom Age masih berada dalam rentang yang wajar sehingga tidak dihapus dari data.
     
- Setelah Outliers Dihapus

   ![alt text]([https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/outliers%20sebelum%20dihapus.png](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/outliers%20setelah%20dihapus.png)?raw=true)

   Visualiasi diatas nemapilkan hasil outliers setelah dihapus

## **Data Preparation**
Pada tahap ini, dilakukan proses transformasi data agar sesuai dan siap digunakan dalam proses pemodelan, salah satunya dengan membagi dataset (split dataset).

### Melakukan Split Dataset
Karena fokus prediksi terletak pada variabel Outcome sebagai target untuk menentukan tingkat akurasi dalam mengklasifikasikan apakah seseorang mengalami menderita diabetes atau tidak, maka kolom tersebut dipisahkan dari dataset utama dan disimpan dalam variabel terpisah. Dataset kemudian dibagi menjadi dua bagian: data training yang digunakan untuk melatih model, dan data testing yang digunakan untuk menguji performa model terhadap data yang belum pernah dilihat sebelumnya. Pembagian ini dilakukan dengan rasio 75% untuk training dan 25% untuk testing, menggunakan fungsi train_test_split dari pustaka sklearn.

```Ruby
x = df.drop(["Outcome"],axis=1)
y = df["Outcome"]
x_train , x_test , y_train , y_test = train_test_split(x,y,test_size=0.25,random_state=42,stratify = y)
```

## Modeling
Setelah melakukan data preparation data yang sudah siap akan digunakan untuk membuat model, kali ini akan dibuat 3 model sebagai perbandingan

### A. Model Logistic Regression
1. Inisialisasi Model Logistic Regression
```Ruby
lr_model = LogisticRegression(max_iter=500)
```
- Baris ini membuat objek `lr_model` dari kelas `LogisticRegression` yang berasal dari library `sklearn.linear_model`.
- Parameter `max_iter=500` berarti model diizinkan melakukan maksimal 500 iterasi dalam proses training untuk mencapai konvergensi. Jika data cukup kompleks atau butuh waktu untuk konvergen, nilai ini bisa ditingkatkan dari default-nya (100).

2. Melatih Model dengan Data Training
```Ruby
lr_model.fit(x_train, y_train)
```
- Fungsi `.fit()` digunakan untuk melatih model menggunakan data training.
   - `x_train` berisi fitur-fitur (variabel independen) untuk pelatihan.
   - `y_train` berisi label atau target variabel (dalam hal ini kemungkinan Outcome).
- Model mempelajari hubungan antara fitur dan target dari data ini agar bisa melakukan prediksi pada data baru.
  
3. Evaluasi Akurasi pada Data Training
```Ruby
train_acc = lr_model.score(x_train, y_train)
```
- Fungsi `.score()` akan menghitung akurasi prediksi model pada data training.
- Akurasi di sini adalah proporsi prediksi yang benar dibandingkan total data training.
- Nilai `train_acc` akan disimpan sebagai metrik performa untuk melihat seberapa baik model mengenali pola pada data yang sudah dipelajarinya.

4. Evaluasi Akurasi pada Data Testing
```Ruby
test_acc = lr_model.score(x_test, y_test)
```
- Serupa dengan sebelumnya, tetapi dilakukan pada data testing (`x_test`, `y_test`).
- Ini menunjukkan seberapa baik model dapat menggeneralisasi ke data baru yang belum pernah dilihat sebelumnya.

5. Menampilkan Hasil Akurasi
```Ruby
print("Akurasi Training:", train_acc)
print("Akurasi Testing :", test_acc)
```
- Menampilkan hasil akurasi pada data training dan testing.
- Penting untuk membandingkan kedua nilai ini:
   - Jika training tinggi tapi testing rendah, kemungkinan model overfitting.
   - Jika kedua nilai serupa dan tinggi, model dianggap baik dan stabil.

### B. Model Decision Tree
1. Inisialisasi Model Decision Tree
```Ruby
dt_model = DecisionTreeClassifier(random_state=42)
```
- Membuat objek model `dt_model` dari kelas `DecisionTreeClassifier`, yang merupakan algoritma pohon keputusan dari library `sklearn.tree`.
- Parameter `random_state=42` digunakan untuk memastikan hasil model konsisten setiap kali dijalankan (mengontrol faktor acak, seperti pemilihan fitur saat pemecahan cabang).

2. Melatih Model
```Ruby
dt_model.fit(x_train, y_train)
```
- Model dilatih menggunakan data fitur (`x_train`) dan label (`y_train`).
- Selama proses ini, Decision Tree akan membagi data ke dalam node berdasarkan fitur yang paling baik memisahkan kelas target (menggunakan kriteria seperti Gini Impurity atau Entropy).

3. Melakukan Prediksi
```Ruby
y_pred_dt = dt_model.predict(x_test)
```
- Menggunakan model yang telah dilatih untuk memprediksi label pada data testing (`x_test`).
- Hasil prediksi disimpan dalam `y_pred_dt`, yang bisa digunakan untuk evaluasi lanjutan seperti confusion matrix atau metrik klasifikasi lainnya.
  
4. Evaluasi Akurasi Model
```Ruby
print("Akurasi Training:", dt_model.score(x_train, y_train))
print("Akurasi Testing :", dt_model.score(x_test, y_test))
```
- `dt_model.score()` menghitung akurasi, yaitu proporsi prediksi yang benar.
   - Akurasi training: seberapa baik model mengenali pola dari data latih.
   - Akurasi testing: seberapa baik model mampu menggeneralisasi ke data baru.
- Jika akurasi training sangat tinggi tapi akurasi testing jauh lebih rendah, kemungkinan besar model mengalami overfitting, yang umum terjadi pada decision tree tanpa pengaturan kedalaman (max_depth).

### C. Model Random Forest
1.  Inisialisasi Model Random Forest
```Ruby
rf_model = RandomForestClassifier(random_state=42)
```
- Baris ini membuat objek `rf_model` dari kelas `RandomForestClassifier`, yang merupakan bagian dari library `sklearn.ensemble`.
- Random Forest adalah algoritma ensemble learning yang menggabungkan banyak Decision Tree untuk meningkatkan akurasi dan stabilitas model.
- `random_state=42` digunakan untuk memastikan hasil yang reproducible (tidak berubah-ubah setiap kali dijalankan).

2. Melatih Model
```Ruby
rf_model.fit(x_train, y_train)
```
- Model dilatih dengan data fitur (`x_train`) dan target (`y_train`).

3. Prediksi pada Data Testing
```Ruby
y_pred_rf = rf_model.predict(x_test)
```
- Model digunakan untuk memprediksi label pada data uji (`x_test`).
- Hasil prediksi disimpan di `y_pred_rf`, yang bisa digunakan untuk evaluasi lanjutan seperti confusion matrix, precision, recall, dll.

4.  Evaluasi Akurasi Model
```Ruby
print("Akurasi Training:", rf_model.score(x_train, y_train))
print("Akurasi Testing :", rf_model.score(x_test, y_test))
```
- `.score()` digunakan untuk menghitung akurasi:
   - Akurasi training: seberapa akurat model terhadap data yang digunakan untuk melatihnya.
   - Akurasi testing: seberapa baik model memprediksi data baru yang belum pernah dilihat sebelumnya.
 
## Evaluation
Metrik evaluasi yang digunakan dalam proyek ini ialah sebagai berikut:

### Classification Report

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/tp_tn_fp_fn.png?raw=true)

Terdapat 4 label pada matriks confusion seperti yang terlihat di gambar, yaitu TP, TN, FP, dan FN. a. True Positive (TP) merupakan jumlah data pada positif yang ditebak dengan benar. b. True Negative (TN) merupakan jumlah data pada negatif yang ditebak dengan benar. c. False Positive (FP) merupakan jumlah data yang ditebak dengan salah karena diprediksi positif, sedangkan aslinya adalah negatif. d. False Negative (FN) merupakan jumlah data yang ditebak dengan salah karena diprediksi negatif, sedangkan aslinya adalah positif.

1. Precision

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/precision.png?raw=true)

   Dari seluruh prediksi positif, berapa yang benar-benar positif.

2. Recall
   
   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/recal.png?raw=true)

   Dari semua kasus positif aktual, berapa banyak yang berhasil diprediksi dengan benar.

3. F1-Score

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/f1.png?raw=true)

   Harmoni antara precision dan recall. Semakin tinggi, semakin baik keseimbangan keduanya.

4. Average (Macro vs Weighted)

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/avg.png?raw=true)

   - Macro Average : Menghitung metrik (precision, recall, f1) secara rata-rata antar kelas, tanpa memperhatikan jumlah sampel (support) pada tiap kelas.
   - Weighted Average : Sama seperti macro, tetapi diberi bobot sesuai jumlah sampel (support) di tiap kelas.

### Confusion Matrix

   ![alt text](https://github.com/UsamahPutraFirdaus/Submission_MLTerapan/blob/main/Submission_1_PredictiveAnalytics/img/confusion%20matrix.png?raw=true)

Berdasarkan hasil Confusion Matrix dari ketiga model yang diuji, model Decision Tree menunjukkan performa terbaik, dengan hanya 2 kesalahan prediksi pada kelas positif (1), dan tidak ada kesalahan pada kelas negatif (0). Sebaliknya, model Logistic Regression memberikan hasil terburuk, dengan 40 kesalahan prediksi pada kelas negatif (0) dan 88 kesalahan pada kelas positif (1). Hal ini menunjukkan bahwa Logistic Regression kurang efektif dalam mendeteksi kasus positif, yang penting dalam konteks deteksi diabetes.

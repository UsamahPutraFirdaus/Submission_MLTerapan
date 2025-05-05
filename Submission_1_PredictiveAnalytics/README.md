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
2. Jumlah Penderita Diabetes berdasarkan perKelompok Usia
3. Matriks Korelasi antar Kolom

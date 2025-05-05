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


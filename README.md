# Laporan-Proyek-Pertama

### Domain Proyek

Domain yang saya pilih adalah datasets yang paling populer di Kaggel, yang berjudul Top 1000 Kaggle Datasets

#### Latar Belakang

Kaggle merupakan anak perusahaan Google LLC. Kaggle memungkinkan pengguna untuk menemukan dan menerbitkan kumpulan data, menjelajahi dan membangun model dalam lingkungan ilmu data berbasis web, bekerja dengan ilmuwan data dan insinyur pembelajaran mesin lainnya, dan mengikuti kompetisi untuk memecahkan tantangan ilmu data.

Kaggle dimulai pada tahun 2010 dengan menawarkan kompetisi pembelajaran mesin dan sekarang juga menawarkan platform data publik, berbasis cloud untuk ilmu data, dan pendidikan Kecerdasan Buatan. Personil utamanya adalah Anthony Goldbloom dan Jeremy Howard. Nicholas Gruen adalah ketua pendiri digantikan oleh Max Levchin. Ekuitas dinaikkan pada tahun 2011 dengan nilai perusahaan sebesar $25 juta. Pada 8 Maret 2017, Google mengumumkan bahwa mereka mengakuisisi Kaggle.

Untuk itulah saya tertarik mengambil topik ini dalam submission saya. 

### Business Understanding

#### Problem Statement

berdasarkan hal tersebut, adapun permasalahan yang diangkat adalah:

* Bagaimana menganalisa poin kegunaan rata-rata dari dataset?
  
  
* Bagaimana memprediksi banyaknya badges yang paling banyak didapatkan?

#### Goals

Adapun tujuan dari dibentuk nya Proyek ini, adalah:

* mengetahui banyaknya badges yang paling banyak didapatkan
* mampu memprediksi poin kegunaan dari datasets

### Data Understanding

Dataset yang digunakan pada proyek ini diambil dari website kaggle dengan judul Top 1000 Kaggle Datasets

[https://www.kaggle.com/datasets/notkrishna/top-1000-kaggle-datasets]

Dataset ini memiliki total 999 baris dan 9 kolom, dan memiliki 1 _missing value_. Adapun penjelasan dari masing-masing kolom tersebut

* list : Identifier
* title : Judul datasets
* uploaded_by : Nama yang mengupload dataset
* last_updated : Terakhir kali dataset diubah
* usability : Skor kegunaan
* files : Jumlah file yang terdapat dalam dataset
* size : Ukuran dataset
* upvotes : Suara positif yang diterima dalam dataset
* badge : Perolehan peringkat

### Data Preparation

Adapun tahap - tahap yang saya gunakan pada Data Preparation ini, adalah: 

#### melakukan split pada dataset

hal pertama adalah membagi dataset menjadi train data dan test data. dengan menggunakan library train_test_split, saya membagi variabel X dan variabel Y. X adalah data bertipe numerik tanpa adanya kolom 'list' (hanya 'usability' dan	'upvotes'). Variabel Y adalah data bertipe numerik yang isinya 'list'. lalu saya bagi dengan ration 80:20. lalu didapatkan x_train yaitu 693, x_test = 174 dari total 867.

#### Standarisasi 

Standarisasi ini adalah teknik machine learning yang digunakan agar model dapat dengan mudah dilatih. disini saya menggunakan StandardScaler agar nilai nya berada diantara -1 dan 1

#### Univariate Analysis

Mari kita berfokus ke variabel 'upvotes'. Dari hasil tersebut, didapatkan analisa bahwa grafik 'upvotes' akan semakin turun seiring dengan banyak nya jumlah sample.

#### Multivariate Analysis

Kita akan berfokus ke variabel 'list'. Dalam hal tersebut, artinya kita akan berfokus ke baris pertama dari atas. Dimana sumbu y nya adalah 'list'. lalu kita lihat korelasi fitur 'list' tersebut dengan fitur numerik lainnya. Pada pola tersebut, terlihat fitur 'usability' memiliki korelasi negatif dengan 'list'. 

#### Correlation Matrix

Disini kita akan berfokus ke korelasi fitur 'list' dengan fitur numerik lainnya. Adapun koefisien korelasi berkisar antara -1 dan +1. dari gambar tersebut, dapat dianalisa bahwa fitur 'usability' memiliki kolerasi yang lebih kecil. 

### Modeling

Model yang akan digunakan adalah KNN, RandomForest, dan Boosting

#### K-Nearest Neighboor (KNN)

Algoritma KNN menggunakan ‘kesamaan fitur’ untuk memprediksi nilai dari setiap data yang baru. Dengan kata lain, setiap data baru diberi nilai berdasarkan seberapa mirip titik tersebut dalam set pelatihan.
* n_neighbors = membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah  tetangga terdekat. pada laporan ini saya menggunakan n_neighbors = 3

#### Random Forest

Random Forest ini adalah kombinasi dari masing-masing tree (pohon) kemudian disatukan dalam satu model. Random Forest ini adalah salah satu metode dalam Decission Tree

* n_estimator: jumlah trees di forest. pada laporan ini saya menggunakan n_estimator = 10
* max_depth: kedalaman atau panjang pohon. pada laporan ini saya menggunakan max_depth = 5
* random_state: digunakan untuk mengontrol random number generator yang digunakan. pada laporan ini saya menggunakan random_state = 5
* n_jobs: jumlah job (pekerjaan) yang digunakan secara paralel. Ia merupakan komponen untuk mengontrol thread atau proses yang berjalan secara paralel. pada laporan ini saya menggunakan n_jobs = -1

#### Boosting

Boosting ini bertujuan untuk meningkatkan performa atau akurasi prediksi. Algoritma yang menggunakan teknik boosting bekerja dengan membangun model dari data latih, kemudian ia membuat model kedua yang bertugas memperbaiki kesalahan dari model pertama. 

* Learning_rate : bobot yang diterapkan pada setiap regressor di masing-masing proses iterasi boosting. pada laporan ini saya menggunakan Learning_rate = 0.01
* random_state: digunakan untuk mengontrol random number generator yang digunakan. pada laporan ini saya menggunakan random_state = 5

### Evaluation

Untuk evaluasi ini saya menggunakan metrik MSE (Mean Squad Error) yang menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. MSE didefinisikan dengan persamaan berikut:

dengan nilai N = jumlah dataset, yi = nilai sebenarnya, dan y_pred = nilai prediksi.

Dari Model Evaluation tersebut, didapatkan bahwa model dengan Boosting memiliki performa paling besar

Selain itu saya dapat menentukan poin kegunaan rata-rata dari yang terbesar hingga terkecil, dan saya menentukan banyaknya badges yang paling banyak didapatkan yaitu ada Silver dengan jumlah lebih dari 400 pengguna.



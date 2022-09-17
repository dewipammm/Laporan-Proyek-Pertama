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

* Bagaimana menganalisa datasets dengan poin yang paling banyak?
* Bagaimana memprediksi banyaknya badges yang paling sering didapatkan?

#### Goals

Adapun tujuan dari dibentuk nya Proyek ini, adalah:

* mampu menganalisa datasets dengan poin yang paling banyak
* mampu memprediksi banyaknya badges yang paling sering didapatkan

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

Mari kita lihat terlebih dahulu grafik yang saya dapatkan:

<img width="513" alt="paint 33" src="https://user-images.githubusercontent.com/93527916/190047190-292c84fa-133e-48c1-a5b5-c9f3b7969741.png">

Mari kita berfokus ke variabel 'upvotes' yang merupakan target utama kita. dari hasil tersebut, didapatkan analisa bahwa grafik 'upvotes' akan semakin turun seiring dengan banyak nya jumlah sample.

#### Multivariate Analysis

Mari kita lihat terlebih dahulu grafik yang saya dapatkan:

![image](https://user-images.githubusercontent.com/110523200/190850190-67d9f4c5-3e96-4ea6-9962-6c53dd0103f2.png)

Sama seperti sebelumnya, kita akan berfokus ke variabel 'upvotes'. Dalam hal tersebut, artinya kita akan berfokus ke baris ke 3 dari atas. dimana sumbu y nya adalah 'upvotes'. lalu kita lihat korelasi fitur 'upvotes' tersebut dengan fitur numerik lainnya. pada pola tersebut, terlihat fitur 'list' memiliki korelasi negatif dengan 'upvotes'. Ditandai dengan menurunnya variabel y saat terjadi kenaikan pada variabel x, namun untuk korelasi nya masih lemah karena sebarannya tidak membentuk pola sempurna. Sedangkan fitur 'usability' memiliki korelasi acak dengan fitur 'upvotes'. Hal tersebut karena sebarannya tidak membentuk pola dan naik turun variabel y saat terjadi kenaikan pada variabel x.

#### Correlation Matrix

mari kita lihat terlebih dahulu korelasi yang saya dapatkan:

![image](https://user-images.githubusercontent.com/110523200/190850321-ffef1c57-3862-4712-a93f-6dead6cc7fc9.png)

disini kita akan berfokus ke korelasi fitur 'upvotes' dengan fitur numerik lainnya. Adapun koefisien korelasi berkisar antara -1 dan +1. dari gambar tersebut, dapat dianalisa bahwa fitur 'usability' memiliki kolerasi yang lebih kecil. Korelasi 'upvotes' dengan 'usability' bernilai 0.06, dan nilai tersebut hampir mendekati nilai 0. 

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

untuk evaluasi ini saya menggunakan metrik MSE (Mean Squad Error) yang menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. MSE didefinisikan dengan persamaan berikut:

dengan nilai N = jumlah dataset, yi = nilai sebenarnya, dan y_pred = nilai prediksi.

adapun grafik yang saya dapatkan setelah menggunakan metrik ini, yaitu:

![image](https://user-images.githubusercontent.com/110523200/190850533-8cbef5de-0493-41b7-a555-4ae17ec27798.png)

Dari Model Evaluation tersebut, didapatkan bahwa model dengan Boosting memiliki performa paling baik

#### Kesimpulan

Dari hasil model yang telah saya buat, tentu saja hasilnya belum memuaskan. Saya harus melakukan improvisasi lagi terkait model tersebut. Melakukan data cleaning mungkin pilihan terbaik agar model dapat berjalan secara maksimal.



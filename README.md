# Laporan Proyek Machine Learning - Deaka Ahmad Naufal
## Project Overview
Buku merupakan jendela dunia sekaligus sumber pengetahuan dan informasi yang dapat mengembangkan pemahaman pembacanya tentang berbagai topik. Melalui buku, pembaca dapat mengeksplorasi ide-ide baru, memperluas wawasan, hingga mengasah keterampilan kritis. Di era digital, akses terhadap buku semakin mudah dengan hadirnya platform e-book, perpustakaan digital, dan toko buku daring. Namun, jumlah buku yang terus bertambah justru menimbulkan tantangan baru. Pembaca kerap kesulitan memilih buku yang sesuai dengan minat, kebutuhan, atau tingkat pemahamannya. Faktor seperti genre, penulis, rekomendasi komunitas, dan rating menjadi pertimbangan yang kompleks. Di sisi lain, penerbit dan platform buku juga membutuhkan cara untuk meningkatkan keterlibatan pengguna dengan menawarkan rekomendasi yang personal dan relevan.

Sistem rekomendasi buku berfungsi sebagai jembatan antara keinginan pembaca dan penyedia materi. Dengan menggunakan metode machine learning seperti kolaboratif filtering, penyaringan berbasis konten, atau kombinasi dua pendekatan, sistem ini mampu mengevaluasi selera pengguna, rekam jejak membaca, dan penilaian untuk menyajikan rekomendasi yang disesuaikan. Pelaksanaan sistem ini tidak hanya membuatnya lebih sederhana bagi pengguna untuk menemukan buku yang sesuai, tetapi juga dapat meningkatkan minat membaca di masyarakat dan mendukung perkembangan industri literasi secara berkelanjutan.
- Referensi terkait riset sebelumnya
  
   R. Ardiansyah, M. Ari Bianto, dan B. D. Saputra, “Sistem Rekomendasi Buku Perpustakaan Sekolah menggunakan Metode Content-Based Filtering,” CoSciTech, vol. 4, no. 2, hlm. 510–518, Okt 2023, doi: 10.37859/coscitech.v4i2.5131.[1]
  
   D. Sarma, T. Mittra, dan M. Shahadat, “Personalized Book Recommendation System using Machine Learning Algorithm,” IJACSA, vol. 12, no. 1, 2021, doi: 10.14569/IJACSA.2021.0120126.[2]

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah disampaikan sebelumnya, pernytaan masalah yang akan diselesaikan pada proyek ini adalah:
-  Jumlah buku yang sangat banyak, membuat pengguna kesulitan menemukan buku yang relevan dengan minat, kebutuhan, atau tingkat pemahaman mereka.

### Goals

Berdasarkan Problem Statement tersebut tujuan yang harus dicapai adalah:
-  Memberikan rekomendasi buku berdasarkan fitur yang serupa dengan buku yang diinput pengguna.
-  Membangun sistem rekomendasi yang merekomendasikan buku populer atau berkualitas tinggi (berdasarkan ulasan/rating pengguna) yang belum pernah dibaca oleh pengguna, tetapi diminati oleh pengguna lain dengan preferensi serupa.


### Solution statements
1. Mengimplementasikan Content-Based Filtering

	Menggunakan teknik cosine similarity untuk menghitung kemiripan antar buku berdasarkan fitur seperti genre.
2. Mengimplementasikan Collaborative Filtering
   
	Membangun model yang mempelajari pola preferensi pengguna dari riwayat baca atau rating yang diberikan, untuk memprediksi buku yang mungkin disukai pengguna berdasarkan kesamaan preferensi dengan pengguna lain.




## Data Understanding
Dataset yang digunakan berasal dari kaggle yang dapat diakses pada [Kaggle](https://www.kaggle.com/datasets/ruchi798/bookcrossing-dataset?select=Books+Data+with+Category+Language+and+Summary). Berisi 1031175 baris dan 19 kolom.
### Variabel-variabel pada Student Habits vs Performance dataset

| Kolom                           | Deskripsi                            |
| ------------------------------- | ------------------------------------ |
| `unamed0:0`                     | kolom index dari data  |
| `user_id`                    	  | ID dari pengguna |
| `location`                           | alamat dari pengguna             |
| `age`                        | Umur pengguna                    |
| `isbn`           | International Standart Book Number kode unik dari buku        |
| `rating`            | Rating yang diberikan oleh pengguna pada buku    |
| `book_title`                 | Judul buku               |
| `book_author`                 | Penulis / pengarang buku                               |
| `year_of_publication`         | Tahun buku diterbitkan  |
| `publisher`                   | Penerbit           |
| `image_s`                  | Gambar sampul buku ukuran small                      |
| `image_m`            | Gambar sampul buku ukuran medium  |
| `image_l`      | Gambar sampul buku ukuran Large|
| `Summary`              | Ringkasan tentang buku         |
| `Language`          | Kode bahasa buku                      |
| `Category` | Kategori buku                             |
| `city`                    | Kota tempat asal pengguna            |
| `state`                    | Provinsi atau negara bagian tempat asal pengguna            |
| `country`                    | Negara asal pengguna            |


**EDA**:
1. Mengecek informasi pada dataset menggunakan `.info()`
	  
  	![Screenshot 2025-04-30 124929](https://github.com/user-attachments/assets/9bf85da7-80a4-41c0-ae84-dd1b07d6c018)

2. Mengecek missing value dan duplicate value
	
 	![Screenshot 2025-04-30 125204](https://github.com/user-attachments/assets/ec4b047f-aedc-4af4-addc-fb6cfc67eb8b)

 	Dalam dataset ini terdapat missing value pada kolom `city`,`statre`,dan`country` . Sedangkan untuk duplicated data tidak ada .
3. Mengecek deskripsi statistik menggunakan`.describe()`
	
 	![Screenshot 2025-04-30 125129](https://github.com/user-attachments/assets/16fa4851-5f75-4ac8-a9b2-df7c64d98f2c)

	Terlihat tidak ada nilai outlier atau nilai yang tidak seharusnya
4. Univariate EDA
	
 	![Screenshot 2025-04-30 133109](https://github.com/user-attachments/assets/96e874e9-c364-4663-8806-428285efc961)

   	Didapat jumlah judul buku, jumlah user, rating dimana da  rating 0 yang artinya user tidak memberikan rating, jumlah kategori pada buku, jumlah bahasa dan terdapat bahasa apa saja, dimana kita nanti akan mengambil buku dengan bahasa inggris saja

6. Cek duplikat kolom isbn
   
   	Didapat Jumlah duplikat sebanyak isbn: 761005.
   
## Data Preparation
- Ambil hanya baris dengan kode en pada kolom language.
  	Untuk memudahkan saat memberi rekomendasi jadi hanya yang berbahasa inggris saja
- Delete duplicated isbn
  	karena isbn merupakan kode unik tiap buku maka jika ada isbn yang sama maka itu adalah buku yang sama
- Handle Missing Value
  	 Missing value pada kolom setiap kolom kita drop
- Ambil sample data
	Data hanya diambil sebanyak 30000 baris untuk memudahkan dan mempercepat komputasi karena sumber daya komputasi yang tidak mencukupi.
 
- Membuat variabel preperation 
	Berisi dataframe dengan kolom untuk membangun model sistem rekomendasi

## Modeling

### **Content Based Filtering**

Content Based Filtering merekomendasikan konten bedasarkan karakteristik konten itu. Jika dianalisis dari atribut setiap konten, seperti genre, penulis, atau topik, konten jenis ini merekomendasikan konten bedasarkan penggunanya.[3] 

**Kelebihan**:
	
 - Tidak bergantung pada data user lain

 - Dapat dijelaskan untuk hasil yang direkomendasikan Karena algoritme pemfilteran berbasis konten sepenuhnya didasarkan pada riwayat perilaku pengguna yang ada untuk menjalankan push. Oleh karena itu, objek yang direkomendasikan kepada pengguna oleh algoritme seharusnya menjadi sesuatu yang sudah diketahui pengguna, bukan sesuatu yang sama sekali baru yang dapat menyebabkan pengguna tidak menyukainya.

 - Memperhitungkan preferensi pengguna yang spesifik dan tidak terpengaruh oleh tren atau preferensi umum.
 
 **Kekurangan**:
	
 - Kebaruan rendah dan kisaran rekomendasi sempit
	
 -  Tidak dapat memperoleh konten inti objek
	    
**Tahapan yang dilakukan**
	
 - Vektorisasi Tfidf. Term Frequency-Inverse Document Frequency. Ia bertujuan untuk mengukur seberapa penting suatu kata terhadap kata-kata lain dalam dokumen. Kategori buku diubah menjadi vektor.

 - Hitung cosine similiarity. menghitung derajat kesamaan(similiarity degree) antara kategori

**Hasil Top 10 Recomendation** 

Buku yang dijadikan acuan adalah 'Accidental City: The Transformation of Toronto' dengan kategori architecture


 ![Screenshot 2025-04-30 141311](https://github.com/user-attachments/assets/70071ed8-0690-4468-94b8-5b6ac4b982d1)

Model memprediksi buku dengan kategori yang sama

### **Collaborative Filtering**
Ide inti dari algoritma rekomendasi collaborative filtering adalah bahwa "pelanggan dengan preferensi yang sama mungkin memiliki minat serupa lainnya"
	
 **Kelebihan**:
 
- Kemudahanan extraksi fitur. tidak perlu mengekstrak dan meringkas informasi secara manual.
- Novelty pada hasil rekomendasi    
- Tidak bergantung pada fitur buku
	
 **Kekurangan**:
 
- Cold start problem. tidak memungkinkan memberi rekomendasi untuk user saat pertama kali
- Maintanability danextensibility. Seiring dengan meningkatnya jumlah pengguna dan meluasnya bidang minat, jumlah item dalam database juga meningkat.

**TOP 10 Rekomendasi**

![Screenshot 2025-04-30 142846](https://github.com/user-attachments/assets/7085595d-56b7-483e-995d-841e84735bde)

Model merekomendasikan buku berdasarkan buku yang telah dibaca dan diberi rating tinggi oleh user
	
## Evaluation


### Content Based Filtering
   Me
**_Precision_** mengukur seberapa baik model menghindari positif palsu (false positives, FP) [4]. Pada model sistem rekomendasi **Contentbased filtering** evaluasi yang digunakan adalah precission dengan formula
  Precision = $\displaystyle \frac{\text{jumlah rekomendasi buku yang relevan}}{\text{jumlah item yang direkomendasikan}}$
  Pada Hasil rekomendasi model contentbased filtering didapat
	Precision = $\\frac{10}{10} = 1$

 Dalam 10 rekomendasi yang diberikan model memberikan 10 kategori yang sesuai
 
### Colaborative Filtering
**Root mean squared error**
RMSE adalah akar kuadrat dari MSE atau akar kuadrat dari nilai rata-rata dari kuadrat kesalahan antara nilai sebenarnya dan nilai prediksi. Ini mengembalikan kesalahan ke dalam satuan yang sama dengan data sehingga lebih mudah diinterpretasikan.
RMSE = $\displaystyle \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^{2}}$

Hasil evaluasi

![Screenshot 2025-04-30 150224](https://github.com/user-attachments/assets/2978e549-adca-4d40-8708-dfc7704b3cbb)


Nilai RMSE kovergen pada epoch ke 50 dengan nilai error 0.1585 dan untuk nilai error validasinya sebesar 0.2918



## REFERENSI
[1]R. Ardiansyah, M. Ari Bianto, dan B. D. Saputra, “Sistem Rekomendasi Buku Perpustakaan Sekolah menggunakan Metode Content-Based Filtering,” CoSciTech, vol. 4, no. 2, hlm. 510–518, Okt 2023, doi: 10.37859/coscitech.v4i2.5131.  
   
[2]D. Sarma, T. Mittra, dan M. Shahadat, “Personalized Book Recommendation System using Machine Learning Algorithm,” IJACSA, vol. 12, no. 1, 2021, doi: 10.14569/IJACSA.2021.0120126.

[3] X. Wu, “Comparison Between Collaborative Filtering and Content-Based Filtering,” HSET, vol. 16, hlm. 480–489, Nov 2022, doi: 10.54097/hset.v16i.2627.

[4] Dicoding. Diakses pada 23 April 2025 dari https://www.dicoding.com/academies/184/tutorials/38763

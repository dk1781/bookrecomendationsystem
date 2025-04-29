# Laporan Proyek Machine Learning - Deaka Ahmad Naufal
## Project Overview
Buku merupakan jendela dunia sekaligus sumber pengetahuan dan informasi yang dapat mengembangkan pemahaman pembacanya tentang berbagai topik. Melalui buku, pembaca dapat mengeksplorasi ide-ide baru, memperluas wawasan, hingga mengasah keterampilan kritis. Di era digital, akses terhadap buku semakin mudah dengan hadirnya platform e-book, perpustakaan digital, dan toko buku daring. Namun, jumlah buku yang terus bertambah justru menimbulkan tantangan baru. Pembaca kerap kesulitan memilih buku yang sesuai dengan minat, kebutuhan, atau tingkat pemahamannya. Faktor seperti genre, penulis, rekomendasi komunitas, dan rating menjadi pertimbangan yang kompleks. Di sisi lain, penerbit dan platform buku juga membutuhkan cara untuk meningkatkan keterlibatan pengguna dengan menawarkan rekomendasi yang personal dan relevan.

Sistem rekomendasi buku berfungsi sebagai jembatan antara keinginan pembaca dan penyedia materi. Dengan menggunakan metode machine learning seperti kolaboratif filtering, penyaringan berbasis konten, atau kombinasi dua pendekatan, sistem ini mampu mengevaluasi selera pengguna, rekam jejak membaca, dan penilaian untuk menyajikan rekomendasi yang disesuaikan. Pelaksanaan sistem ini tidak hanya membuatnya lebih sederhana bagi pengguna untuk menemukan buku yang sesuai, tetapi juga dapat meningkatkan minat membaca di masyarakat dan mendukung perkembangan industri literasi secara berkelanjutan.
- Referensi terkait riset sebelumnya
  
   R. Ardiansyah, M. Ari Bianto, dan B. D. Saputra, “Sistem Rekomendasi Buku Perpustakaan Sekolah menggunakan Metode Content-Based Filtering,” CoSciTech, vol. 4, no. 2, hlm. 510–518, Okt 2023, doi: 10.37859/coscitech.v4i2.5131.
  
   D. Sarma, T. Mittra, dan M. Shahadat, “Personalized Book Recommendation System using Machine Learning Algorithm,” IJACSA, vol. 12, no. 1, 2021, doi: 10.14569/IJACSA.2021.0120126.

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
Dataset yang digunakan berasal dari kaggle yang dapat diakses pada [Kaggle](https://www.kaggle.com/datasets/jayaantanaath/student-habits-vs-academic-performance/data). Dengan 1.000 catatan siswa sintetis dan 16 fitur termasuk jam belajar, pola tidur, penggunaan media sosial, kualitas diet, kesehatan mental, dan nilai ujian akhir. 1000 baris dan 16 kolom.

### Variabel-variabel pada Student Habits vs Performance dataset


| Kolom                           | Deskripsi                            |
| ------------------------------- | ------------------------------------ |
| `student_id`                    | ID unik siswa (tidak untuk analisis) |
| `age`                           | Usia siswa (17-24 tahun)             |
| `gender`                        | Jenis kelamin siswa Male/Female/Other                    |
| `study_hours_per_day`           | Rata-rata lama waktu jam belajar harian siswa        |
| `social_media_hours`            | Rata-rata lama waktu siswa di sosial media    |
| `netflix_hours`                 | Rata-rata lama waktu siswa menonton Netflix               |
| `part_time_job`                 | status part time siswa Yes/No                               |
| `attendance_percentage`         | Persentase kehadiran dikelas (0-100%)  |
| `sleep_hours`                   | Rata-rata jam tidur harian           |
| `diet_quality`                  | Kualitas diet siswa (Poor/Fair/Good )                      |
| `exercise_frequency`            | Frekuensi olahraga per minggu (0-7)  |
| `parental_education_level`      | jejang edukasi orang tua             |
| `internet_quality`              | Kualitas internet yang dimiliki Poor/Average/Good/Excellent          |
| `mental_health_rating`          | Status kesehatan mental dalam Skala 1-10                           |
| `extracurricular_participation` | Status mengikuti kegiatan extrakulikulerYes/No                               |
| `exam_score`                    | Nilai ujian akhir (0-100)            |


**EDA**:
1. Mengecek informasi pada dataset menggunakan `.info()`
	
 	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424195500.png">
	
 	Dari gambar diatas dapat kita lihat ada missing value pada kolom `parental_education_level`
2. Mengecek missing value dan duplicate value
	Dalam dataset ini terdapat missing value pada kolom `parental_education_level` sebanyak 91. Sedangkan untuk duplicated data tidak ada .
3. Mengecek deskripsi statistik menggunakan`.describe()`
 	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424200512.png">
Saat kita lihat statistik tidak terdapat nilai berupa outlier atau nilai yang salah
4. Boxplot dan distribusi setiap variabel numerik
	- Age
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424200916.png">
 
	- study hours perday
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424200944.png">
 
	- attendance percentage
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424201004.png">
 
	- sleephours
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424201052.png">
 
	- exercise frequency
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424201112.png">
 

	- mental health rating
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424201131.png">

	- exam score
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424201144.png">

	- screen time(Jumlah social media hours dan netflix hours)
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424201200.png">
 

	Seluruh variabel memiliki nilai yang cukup normal walaupun beberapa terdapat outlier akan tetapi nilai tersebut masih berada didalam rentang yang seharusnya
5. Categorical Feature 
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424201503.png">
 
## Data Preparation
- Handle Missing Value
  
  	 Missing value pada kolom `parental_education_level` kita isi dengan nilai modusnya( Nilai yang paling sering muncul).
  
- Drop kolom student_id
	Kolom dihapus karena tidak akan digunakan dan malah akan menganggu proses klasifikasi
 
- Membuat kolom screen time 
	yaitu jumlah dari waktu yang digunakan untuk social media dan netflix lalu mendrop kolom netflix_hours dan social_media_hours 
- Map Exam Score
  
	Memetakan kolom Exam Score ke kolom exam resul menjadi "Pass" dan "Faill" untuk  dijadikan targer klasifikasi dimana exam_score >= 70 adalah "Pass". lalu drop kolom exam scorenya
- Encoding Feature Kategorikal
  
	fitur kategori yang bertipe object di rubah menjadi numerik agar model mengenali data kategorikal
- Feature Selection
  
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424231629.png">
 
	Kolom study_hours_per_day,mental_health_rating, screen_time dipilih karena memiliki nilai korelasi yang paling tinggi baik itu positif atau negatif. itu artinya Fitur inilah yang paling berpengaruh pada kelulusan
- Split dataset
  
	Membagi dataset menjadi train dan test dengan rasio 80 : 20 dilakukan guna melakukan tahap training pada model menggunakan data train, lalu melakukan tahap evaluasi menggunakan data test
- Standarisasi
  
	Melakukan Standarisasi menggunakan standar scaller agar algoritma tidak terpengaruh oleh perbedaan skala antar fitur

## Modeling

1. logistic Regression
	Algoritma yang bertujuan untuk memprediksi probabilitas bahwa suatu instance termasuk dalam kelas tertentu atau tidakdengan cara menganalisis hubungan antara dua faktor data.

Parameter:
   
- penalty='l2', #Parameter penalty yang akan diterapkan untuk mencegah overfitting.
- C=0.5,#inverse dari kekuatan regularisasi. Ini adalah parameter positif yang mengontrol seberapa kuat penalti regularisasi diterapkan
- solver='liblinear',#lgoritma optimasi yang akan digunakan untuk menemukan nilai koefisien yang optimal. 
- max_iter=2000,#jumlah maksimum iterasi yang akan dilakukan oleh algoritma solver untuk mencapai konvergensi.

    random_state=42 # Reproduksibilitas struktur mengontrol keacakan dalam algoritma.
   
**Kelebihan**:
   
- Efisien untuk dataset kecil (sederhana dan mudah dilatih
-  Interpretasi koefisien mudah untuk analisis pengaruh fitur

**Kekurangan**:

- Hanya menangkap hubungan linear
-  Sensitif terhadap outlier
    




2. **Decision Tree **
	Algoritma berbasis pohon keputusan dengan pembagian rekursif.digunakan untuk memprediksi nilai kontinu dari variabel dependen berdasarkan variabel independen.
	
 Parameter:
 
- max_depth=7,          # Batasi kedalaman maksimum pohon
- min_samples_split=15, # Minimal 15 sampel untuk split node
- random_state=42       # Reproduksibilitas struktur mengontrol keacakan dalam algoritma.
	
 **Kelebihan**:
 
-  Menangkap hubungan non-linear
-  Tidak membutuhkan feature scaling
-  Visualisasi intuitif
	
 **Kekurangan**:
- Rentan overfitting jika depth tidak diatur
-  Sensitif terhadap perubahan kecil data
	    


 
3. **Random Forest**
Metode ensemble berbasis pohon keputusan yang menggabungkan banyak pohon untuk meningkatkan akurasi dan mengurangi overfitting
	
Parameter:

- n_estimators=200,     # Jumlah pohon besar untuk stabilitas
- max_depth=12,         # Kedalaman fleksibel dengan kontrol
- min_samples_leaf=5,   # Minimal 5 sampel di leaf node
- random_state=42       
	
 **Kelebihan**:
 
- Robust terhadap noise dan outlier
- Fitur importance otomatis    
-  Reduksi varians dibanding single tree
	
 **Kekurangan**:
 
- Waktu training lebih lama
-  Kompleksitas interpretasi manual
	 	
4. **XGBoost**
	Algoritma gradient boosting yang optimalkan model bertahap.algoritma boosting yang sangat kuat untuk tugas klasifikasi dan regresi. XGBoost dirancang untuk efisiensi, fleksibilitas, dan performa tinggi.
	
 Parameter:
 
- learning_rate=0.05,   # Langkah pembelajaran presisi tinggi
- max_depth=4,          # Kedalaman terkontrol
-  n_estimators=300,     # Kompensasi learning rate kecil
- random_state=42       
	
 **Kelebihan**:
 
-  Akurasi tinggi untuk data kompleks
- Regularisasi bawaan (max_depth)
-  Handle missing value otomatis
	
 **Kekurangan**:
 
-  Waktu training panjang
-  Sensitif terhadap hyperparameter

  
**Pemilihan model terbaik**
Berdasarkan Hasil Evaluasi pada data test Model terbaik adalah Logistic Regression
	
## Evaluation

1. Confussion Matrix
	**_Confusion matrix_** adalah alat untuk mengevaluasi kinerja model klasifikasi dengan menunjukkan jumlah prediksi yang benar dan salah dalam format tabel. Ini memberikan pandangan yang lebih rinci tentang cara model berperforma di berbagai kelas.
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230256.png">
 
2. Akurasi
	**Akurasi** adalah metrik yang paling sederhana dan sering digunakan untuk mengukur kinerja model klasifikasi. Akurasi dihitung sebagai proporsi dari prediksi benar (baik positif maupun negatif) terhadap seluruh prediksi yang dilakukan oleh model.
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230111.png">
 
3. F1 Score
	**F1-Score** adalah metrik yang menggabungkan presisi dan recall menjadi satu nilai tunggal yang mempertimbangkan keduanya. F1-Score adalah rata-rata harmonis dari presisi dan recall, memberikan gambaran yang lebih baik ketika ada _trade-off_ antara keduanya.
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230454.png">
 
4. Precission
	**_Precision_** mengukur seberapa baik model menghindari positif palsu (false positives, FP). Ini adalah rasio prediksi positif yang benar terhadap semua prediksi positif yang dibuat oleh model
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230429.png">
 
5. Recall
	**_Recall_** atau **sensitivitas** adalah metrik yang mengukur seberapa baik model dapat menangkap semua contoh positif. Ini adalah rasio prediksi positif yang benar terhadap semua kasus positif yang sebenarnya ada dalam data.
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230144.png">
 
6. Cross-Validation
	Teknik ini membagi data menjadi beberapa subset yang dikenal sebagai **_fold_**. Model dilatih dalam beberapa subset serta diuji pada subset yang tersisa dan proses ini diulang beberapa kali. Jika performa model sangat bervariasi antara **_fold_**, ini menunjukkan bahwa model mengalami overfitting pada subset data tertentu dan tidak dapat menggeneralisasi dengan baik. _Cross-validation_ membantu memastikan bahwa model dinilai secara lebih konsisten di seluruh data.
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230539.png">
 

### Hasil Evaluasi

<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424231028.png">

- Logistic Regression
  
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230654.png">

- Decission Tree
  
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230818.png">
 
- Random Forest
  
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230835.png">
 
- XGBoost
  
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424230842.png">
 

- Perbandingan Akurasi serta crosvall setiap Model
	
	<img src="https://raw.githubusercontent.com/dk1781/PredictiveAnalysis_StudentHabitsvsPerformance/refs/heads/main/images/Pasted%20image%2020250424231128.png">
- Berdasarkan gambar diatas model Logistic regression dan random forest mendapatkan nilai akurasi yang paling tinggi yaitu 83% akan tetapi untuk Cross validationnya model Logistic Regression mengungguli model Random Forest yaitu 83% dibandingkan 78%. Maka didapat model Logistic Regression model terbaik untuk klasifikasi student habits vs performance ini.

### Kesimpulan
- Kebiasaan siswa yang paling berpengaruh terhadap kelulusan adalah study_hours_per_day (rata rata lama belajar siswa perhari ,mental_health_rating (kesehatan mental siswa), screen_time("rata rata lama siswa membuka social media ataupun menonton netflix perhari)
- Model terbaik yang mampu meprediksi kelulusan siswa berdasarrkan kebiasaanya adalah Model Logistic Regression



## REFERENSI
[1]Ashfaq, U., M, B. P., & Mafas, R. (2020). Managing Student Performance: A Predictive Analytics using Imbalanced Data. _International Journal of Recent Technology and Engineering (IJRTE)_, _8_(6), 2277–2283. https://doi.org/10.35940/ijrte.e7008.038620

[2]A. Rahman, “Klasifikasi Performa Akademik Siswa Menggunakan Metode Decision Tree dan Naive Bayes,” _saintekom_, vol. 13, no. 1, hlm. 22–31, Mar 2023, doi: [10.33020/saintekom.v13i1.349](https://doi.org/10.33020/saintekom.v13i1.349).

[3]Dicoding. Diakses pada 23 April 2025 dari https://www.dicoding.com/academies/184/tutorials/38763

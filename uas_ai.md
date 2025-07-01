# Laporan Proyek Machine Learning - Segmentasi Lagu Populer Spotify 2019

## Domain Proyek

Musik telah menjadi bagian integral dari kehidupan manusia dan terus berkembang dengan bantuan teknologi digital. Platform seperti Spotify memungkinkan pengguna untuk menikmati jutaan lagu dengan berbagai genre dan gaya. Dengan banyaknya data lagu yang tersedia, penting untuk melakukan analisis untuk memahami pola atau karakteristik yang tersembunyi dalam data audio tersebut.

Salah satu pendekatan yang efektif dalam mengelompokkan lagu berdasarkan kesamaan fitur adalah teknik clustering, khususnya K-Means Clustering. Algoritma ini mampu membagi kumpulan lagu menjadi beberapa grup yang serupa secara otomatis berdasarkan fitur seperti tempo, energi, danceability, dan lainnya. Segmentasi ini dapat digunakan oleh perusahaan musik, pengembang aplikasi rekomendasi, dan pengguna umum untuk mengatur playlist atau memahami selera musik berdasarkan data.

## Referensi
- Schedl, M., Zamani, H., Chen, C.-W., Deldjoo, Y., & Elahi, M. (2018). Current Challenges and Visions in Music Recommender Systems Research. International Journal of Multimedia Information Retrieval, 7, 95–116. https://doi.org/10.1007/s13735-018-0154-2

- Wang, Y., & Zhang, D. (2020). Music Recommendation System Based on Clustering and Deep Learning. International Conference on Artificial Intelligence and Big Data. https://doi.org/10.1109/ICAIBD49188.2020.9137379

- Tzanetakis, G., & Cook, P. (2002). Musical genre classification of audio signals. IEEE Transactions on Speech and Audio Processing, 10(5), 293–302. https://doi.org/10.1109/TSA.2002.800560

- Lee, J.-H., & Cunningham, S. J. (2013). The Impact (or Non-Impact) of User Studies in Music Information Retrieval. Journal of the American Society for Information Science and Technology, 64(3), 409–425. https://doi.org/10.1002/asi.22745

- Celma, Ò. (2010). Music Recommendation and Discovery: The Long Tail, Long Fail, and Long Play in the Digital Music Space. Springer.

## Business Understanding
## Problem Statements
1. **Bagaimana mengelompokkan lagu-lagu populer di Spotify berdasarkan kesamaan fitur audio?**
   Lagu populer dapat berbeda secara genre, tempo, dan intensitas. Segmentasi akan membantu memahami grup lagu yang serupa dengan menggunakan algoritma K-Means berdasarkan fitur numerik seperti energy, danceability, loudness, dsb.

2.  **Fitur audio apa saja yang paling memengaruhi pengelompokan lagu-lagu tersebut?**
   Dengan mengamati hasil klastering dan distribusi fitur per klaster, dapat dievaluasi fitur dominan yang menjadi pembeda antar klaster seperti energy, loudness, acousticness, atau valence.

3. **Bagaimana visualisasi dan interpretasi dari hasil segmentasi dapat digunakan untuk analisis bisnis atau rekomendasi musik?**
   Visualisasi seperti scatter plot (PCA), bar chart, dan heatmap membantu pemahaman klaster. Informasi ini dapat digunakan untuk membuat playlist otomatis, meningkatkan sistem rekomendasi lagu, atau analisis pasar berdasarkan gaya lagu yang disukai audiens.

## Goals
1. Mengelompokkan 50 lagu populer Spotify tahun 2019 berdasarkan fitur audio menggunakan K-Means Clustering.
2. Menyediakan visualisasi dari hasil klastering untuk interpretasi yang mudah.
3. Mengidentifikasi karakteristik unik dari tiap klaster.

## Solution Statement
Untuk mencapai tujuan, langkah-langkah sebagai berikut dilakukan:
1. Exploratory Data Analysis (EDA)
   Menyajikan statistik deskriptif dan visualisasi fitur lagu.
2. Preprocessing
   Seleksi dan normalisasi fitur numerik.
3. K-Means Clustering:
   Menentukan jumlah klaster optimal dan melakukan segmentasi lagu.
4. Evaluasi & Visualisasi
   Menggunakan Elbow Method, PCA, dan scatter plot untuk visualisasi hasil klaster.

### Problem Statements

1. **Bagaimana mengelompokkan lagu-lagu populer di Spotify berdasarkan kesamaan fitur audio?**
   Lagu populer dapat berbeda secara genre, tempo, dan intensitas. Segmentasi akan membantu memahami grup lagu yang serupa.

2. **Fitur audio apa saja yang paling memengaruhi pengelompokan lagu-lagu tersebut?**
   Dengan mengamati hasil klastering, dapat dievaluasi fitur dominan yang menjadi pembeda antar klaster.

3. **Bagaimana visualisasi dan interpretasi dari hasil segmentasi dapat digunakan untuk analisis bisnis atau rekomendasi musik?**

### Goals

* Mengelompokkan 50 lagu populer Spotify tahun 2019 berdasarkan fitur audio menggunakan K-Means Clustering.
* Menyediakan visualisasi dari hasil klastering untuk interpretasi yang mudah.
* Mengidentifikasi karakteristik unik dari tiap klaster.

### Solution Statement

Untuk mencapai tujuan, langkah-langkah sebagai berikut dilakukan:

1. **Exploratory Data Analysis (EDA)**: Menyajikan statistik deskriptif dan visualisasi fitur lagu.
2. **Preprocessing**: Seleksi dan normalisasi fitur numerik.
3. **K-Means Clustering**: Menentukan jumlah klaster optimal dan melakukan segmentasi lagu.
4. **Evaluasi & Visualisasi**: Menggunakan Elbow Method, PCA, dan scatter plot untuk visualisasi hasil klaster.

## Data Understanding

### Dataset

Dataset digunakan dari Kaggle: [Top 50 Spotify Songs - 2019](https://www.kaggle.com/datasets/leonardopena/top50spotify2019)

* Jumlah data: 50 lagu
* Fitur utama: `Beats.Per.Minute`, `Energy`, `Danceability`, `Loudness..dB..`, `Liveness`, `Valence.`, `Length.`, `Acousticness..`, `Speechiness.`, `Popularity`

### Informasi Dataset
Informasi dataset diberikan menggunakan fungsi `data.info()`. Berikut adalah hasilnya:

 #   Column            Non-Null Count  Dtype  
---  ------            --------------  -----  
 0   Unnamed: 0        50 non-null     int64  
 1   Track.Name        50 non-null     object 
 2   Artist.Name       50 non-null     object 
 3   Genre             50 non-null     object 
 4   Beats.Per.Minute  50 non-null     int64  
 5   Energy            50 non-null     int64  
 6   Danceability      50 non-null     int64  
 7   Loudness..dB..    50 non-null     int64  
 8   Liveness          50 non-null     int64  
 9   Valence.          50 non-null     int64  
 10  Length.           50 non-null     int64  
 11  Acousticness..    50 non-null     int64  
 12  Speechiness.      50 non-null     int64  
 13  Popularity        50 non-null     int64  
 14  Cluster           50 non-null     int32  
 15  PCA1              50 non-null     float64
 16  PCA2              50 non-null     float64

### Statistik Deskriptif

* Fitur `Energy` berkisar dari 33 hingga 98.
* Fitur `Danceability` menunjukkan variasi tinggi antara lagu.
* Tidak ditemukan nilai null, dan semua fitur yang digunakan bertipe numerik.

## Data Preparation

1. **Seleksi Fitur Numerik**
   Dipilih fitur yang relevan untuk clustering, yaitu:

   * `Beats.Per.Minute`
   * `Energy`
   * `Danceability`
   * `Loudness..dB..`
   * `Liveness`
   * `Valence.`
   * `Length.`
   * `Acousticness..`
   * `Speechiness.`

2. **Normalisasi Data**
   Dilakukan Min-Max Scaling agar semua fitur berada pada skala yang sama (0 - 1) agar tidak bias dalam perhitungan jarak (Euclidean Distance).

## Modeling

### Menentukan Jumlah Klaster Optimal

* Digunakan **Metode Elbow** dengan variabel WCSS (Within-Cluster-Sum-of-Squares).
* Dari grafik elbow, terlihat titik tekuk optimal berada pada **k=4**.

### Penerapan K-Means Clustering

* Model: `KMeans(n_clusters=4, random_state=42)`
* Hasil clustering memberikan label 0 sampai 3 untuk tiap lagu.

### Visualisasi

* Digunakan **PCA (Principal Component Analysis)** untuk mereduksi dimensi menjadi 2D.
* Visualisasi scatter plot menunjukkan 4 kelompok lagu yang terpisah jelas.

## Evaluation

### Interpretasi Tiap Klaster

Dengan menganalisis nilai rata-rata tiap fitur pada setiap klaster, dapat diambil kesimpulan berikut:

* **Klaster 0**: Lagu dengan energi tinggi, danceability tinggi, dan loudness keras. Cocok untuk suasana pesta/klub.
* **Klaster 1**: Lagu slow, akustik tinggi, speechiness rendah. Cocok untuk relaksasi.
* **Klaster 2**: Lagu dengan karakteristik seimbang, cocok untuk easy listening.
* **Klaster 3**: Lagu dengan speechiness tinggi dan liveness tinggi. Mungkin berisi lagu live performance atau hip-hop.

### Manfaat Hasil Segmentasi

* Playlist Generator: Spotify dapat mengelompokkan lagu secara otomatis berdasarkan segmentasi ini.
* Rekomendasi Musik: Jika pengguna menyukai lagu dari klaster tertentu, sistem bisa merekomendasikan lagu dari klaster yang sama.
* Analisis Pasar: Label rekaman dapat mengetahui tren audio seperti apa yang paling populer.

## Kesimpulan

Proyek ini berhasil melakukan segmentasi terhadap lagu-lagu populer Spotify 2019 menggunakan algoritma K-Means Clustering. Dengan 4 klaster utama, kita dapat memahami perbedaan karakteristik antar grup lagu berdasarkan fitur audio. Visualisasi dan interpretasi hasil memberikan wawasan baru bagi pengembangan sistem rekomendasi musik dan strategi pemasaran konten musik digital.

## Referensi

* Jha, A., & Singh, Y. (2020). Music Genre Classification with Machine Learning Algorithms. *International Journal of Computer Applications*, 175(30), 17-21.
* Tiwari, P. (2018). Analysis and Classification of Spotify Songs using Machine Learning. *International Journal of Scientific Research in Computer Science, Engineering and Information Technology*, 3(6), 2456-3307.
* Schedl, M., Gómez, E., & Urbano, J. (2014). Music Information Retrieval: Recent Developments and Applications. *Foundations and Trends in Information Retrieval*, 8(2-3), 127-261.


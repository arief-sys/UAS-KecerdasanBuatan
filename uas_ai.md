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

## Data Understanding

### Deskripsi Dataset
Dataset digunakan dari Kaggle: [Top 50 Spotify Songs - 2019](https://www.kaggle.com/datasets/leonardopena/top50spotify2019)
* Jumlah data: 50 lagu
* Fitur utama: `Beats.Per.Minute`, `Energy`, `Danceability`, `Loudness..dB..`, `Liveness`, `Valence.`, `Length.`, `Acousticness..`, `Speechiness.`, `Popularity`
### Informasi Dataset
Informasi dataset diberikan menggunakan fungsi `data.info()`. Berikut adalah hasilnya:

no  | Column           | Non-Null Count | Dtype  
--- | ------           | -------------- | -----  
 0  | Unnamed: 0       | 50 non-null    | int64  
 1  | Track.Name       | 50 non-null    | object 
 2  | Artist.Name      | 50 non-null    | object 
 3  | Genre            | 50 non-null    | object 
 4  | Beats.Per.Minute | 50 non-null    | int64  
 5  | Energy           | 50 non-null    | int64  
 6  | Danceability     | 50 non-null    | int64  
 7  | Loudness..dB..   | 50 non-null    | int64  
 8  | Liveness         | 50 non-null    | int64  
 9  | Valence.         | 50 non-null    | int64  
 10 | Length.          | 50 non-null    | int64  
 11 | Acousticness..   | 50 non-null    | int64  
 12 | Speechiness.     | 50 non-null    | int64  
 13 | Popularity       | 50 non-null    | int64  
 14 | Cluster          | 50 non-null    | int32  
 15 | PCA1             | 50 non-null    | float64
 16 | PCA2             | 50 non-null    | float64

### Statistik Deskriptif
Berikut adalah statistik deskriptif untuk fitur numerik dalam dataset:
![image](https://github.com/user-attachments/assets/244551a2-7a04-4eec-a90e-75c838b58737)

## Exploratory Data Analysis (EDA)

1. Distribusi Beats Per Minute (BPM)
   Tempo lagu (BPM) dalam dataset bervariasi dari 85 hingga 190 BPM, dengan rata-rata sekitar 120 BPM. Ini menunjukkan campuran lagu lambat hingga cepat.
2. Distribusi Energy dan Loudness
   Nilai energy dan loudness menunjukkan seberapa "kuat" atau intens lagu tersebut. Lagu dengan nilai energy tinggi cenderung juga memiliki loudness yang lebih tinggi (lebih keras).Beberapa lagu memiliki energy rendah dengan loudness rendah, menandakan lagu slow.
3. Danceability vs Acousticness
   Danceability dan acousticness memiliki hubungan terbalik. Lagu dengan nilai danceability tinggi cenderung memiliki nilai acousticness rendah, yang umum ditemukan pada lagu pop, EDM, dan dance.
4. PCA1 vs PCA2 (Visualisasi Klaster)
   Hasil reduksi dimensi menggunakan PCA menunjukkan visualisasi klaster yang cukup terpisah antar segmen. Hal ini menunjukkan bahwa fitur numerik mampu menangkap karakteristik unik tiap kelompok lagu.
5. Distribusi Popularity dan Speechiness
   Lagu-lagu dengan popularitas tinggi tidak selalu memiliki nilai speechiness tinggi. Ini menunjukkan bahwa kandungan lirik atau rap bukan satu-satunya indikator popularitas.

### Kesimpulan Data Understanding
- Dataset sudah bersih, tidak memiliki missing value.
- Fitur numerik memiliki sebaran yang bervariasi dan mencerminkan keberagaman genre/popularitas.
- Terdapat korelasi visual antara beberapa fitur (contoh: energy vs loudness, danceability vs acousticness).
- Visualisasi PCA memperkuat pemisahan antar klaster, yang mendukung proses clustering menggunakan K-Means.

## Data Preparation
1. Seleksi Fitur Numerik
   Dipilih fitur yang relevan untuk clustering, yaitu:
   - Beats.Per.Minute
   - Energy
   - Danceability
   - Loudness..dB..
   - Liveness
   - Valence.
   - Length.
   - Acousticness..
   - Speechiness.
2. Normalisasi Data
   Dilakukan Min-Max Scaling agar semua fitur berada pada skala yang sama (0 - 1) agar tidak bias dalam perhitungan jarak (Euclidean Distance).

3. Pemisahan Fitur dan Label
   Karena ini adalah unsupervised learning, tidak ada label target. Namun data dipecah menjadi:
   - X: Fitur numerik terpilih.
4. Reduksi Dimensi (PCA)
   Dilakukan Principal Component Analysis untuk mengurangi dimensi menjadi 2 komponen utama (PCA1 & PCA2) untuk keperluan visualisasi klaster.
Dataset yang telah diproses ini siap digunakan untuk pelatihan model clustering menggunakan K-Means.

## Modeling
# K-Means Clustering
K-Means Clustering merupakan algoritma unsupervised learning yang bertujuan membagi data ke dalam k klaster berdasarkan kemiripan antar fitur.
1. Pemilihan Jumlah Klaster (k)
   Elbow Method digunakan untuk menentukan nilai optimal k. Hasil grafik menunjukkan bahwa k = 3 memberikan titik siku (elbow) terbaik, sehingga digunakan untuk klastering.
2. Inisialisasi Model
   Model KMeans diinisialisasi dengan:
   - n_clusters=3
   - random_state=42
3. Pelatihan Model
   Model dilatih menggunakan data numerik hasil normalisasi.Output berupa label klaster yang ditambahkan ke dalam dataframe.
4. Reduksi Dimensi untuk Visualisasi
   Principal Component Analysis (PCA) digunakan untuk mereduksi dimensi ke 2D (PCA1 dan PCA2), sehingga visualisasi klaster menjadi lebih mudah.
5. Visualisasi Klaster
   Hasil visualisasi menggunakan scatter plot menunjukkan bahwa lagu-lagu terbagi ke dalam 3 klaster yang cukup terpisah berdasarkan kombinasi fitur.
6. Interpretasi Klaster
   - Klaster 0: Lagu dengan energy dan BPM sedang, danceability tinggi.
   - Klaster 1: Lagu akustik atau ballad dengan loudness rendah dan acousticness tinggi.
   - Klaster 2: Lagu dengan energy tinggi dan loudness keras, cenderung genre EDM/pop uptempo.
Model K-Means ini berhasil mengelompokkan lagu berdasarkan karakteristik audio yang relevan, dan dapat digunakan untuk sistem rekomendasi otomatis, segmentasi pasar musik, atau pembuatan playlist otomatis.

## Evaluation
Pada tahap ini, dilakukan evaluasi terhadap performa model berdasarkan hasil segmentasi.
### Metrik Evaluasi untuk K-Means
Berbeda dengan klasifikasi, model clustering seperti K-Means dievaluasi menggunakan metrik unsupervised:
   - Inertia: Jumlah kuadrat jarak tiap titik ke pusat klasternya. Semakin kecil, semakin baik.
   - Silhouette Score: Metrik konsistensi antar data dalam klaster. Nilai berkisar dari -1 hingga 1. Semakin tinggi, semakin baik pemisahan antar klaster.
### Hasil Evaluasi Model K-Means:
- Inertia: 8500.3
- Silhouette Score: 0.46 (cukup baik untuk clustering dengan 3 klaster dan hanya 50 data)
### Analisis Klaster
Distribusi lagu dalam masing-masing klaster:
![image](https://github.com/user-attachments/assets/66883b44-2b45-40c3-ad2f-b4980d4e7b44)
Setiap klaster menunjukkan karakteristik unik dalam hal fitur:
- Klaster 0: Lagu dance-pop dengan tingkat energy dan valence sedang.
- Klaster 1: Lagu akustik, tempo lambat, dan lebih emotional.
- Klaster 2: Lagu dengan energy tinggi dan loudness keras.
### Visualisasi Evaluasi
Visualisasi PCA menunjukkan bahwa ketiga klaster cukup terpisah dalam ruang 2 dimensi:
![image](https://github.com/user-attachments/assets/2274d914-d71e-43d7-a6e4-d93c3c76bfb1)
Secara keseluruhan, model K-Means dengan 3 klaster memberikan segmentasi yang bermakna terhadap lagu-lagu populer Spotify 2019.

## Kesimpulan
Proyek ini berhasil mengimplementasikan algoritma K-Means Clustering untuk melakukan segmentasi terhadap 50 lagu populer Spotify 2019 berdasarkan fitur-fitur audio numerik. Hasil utama yang diperoleh adalah sebagai berikut:
- Tiga klaster utama berhasil diidentifikasi dari lagu-lagu populer. Masing-masing klaster memiliki ciri khas:
   - Klaster 0: Lagu dance-pop yang ritmis dan menyenangkan.
   - Klaster 1: Lagu akustik atau ballad dengan tempo pelan dan emosi tinggi.
   - Klaster 2: Lagu dengan intensitas tinggi, tipikal genre EDM atau party.
- Evaluasi menggunakan Silhouette Score sebesar 0.46 menunjukkan bahwa pemisahan antar klaster cukup baik dan wajar, mengingat data hanya terdiri dari 50 lagu.
- Visualisasi PCA mempermudah interpretasi hasil klastering dan memperlihatkan distribusi lagu-lagu secara visual yang dapat dimanfaatkan untuk analisis bisnis.
- Segmentasi lagu ini memiliki potensi nyata untuk implementasi bisnis, seperti:
   - Pembuatan playlist otomatis berdasarkan klaster.
   - Rekomendasi musik berdasarkan selera pengguna.
   - Analisis pasar dan tren musik populer.
Dengan demikian, proyek ini memberikan pendekatan yang efektif dan aplikatif untuk analisis musik menggunakan machine learning, khususnya K-Means Clustering, yang dapat ditingkatkan dengan data lebih besar dan fitur tambahan untuk aplikasi industri musik modern.


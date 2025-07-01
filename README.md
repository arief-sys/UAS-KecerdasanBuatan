# 🎵 Segmentasi Lagu Populer Spotify 2019 Berdasarkan Fitur Audio dengan K-Means Clustering

Proyek ini bertujuan untuk mengelompokkan 50 lagu terpopuler Spotify tahun 2019 berdasarkan fitur audio numerik seperti tempo, danceability, energy, dan loudness menggunakan algoritma **K-Means Clustering**. Segmentasi ini dapat digunakan untuk:

- Rekomendasi lagu otomatis  
- Pembuatan playlist berdasarkan tipe lagu  
- Analisis pasar musik berdasarkan karakteristik audio  

---

## ✅ Tujuan Proyek

Mengelompokkan lagu-lagu populer berdasarkan karakteristik numerik seperti:

- **Tempo**
- **Danceability**
- **Energy**
- **Loudness**

Dengan hasil segmentasi yang mendukung:

- **Rekomendasi lagu berdasarkan kesamaan klaster**
- **Pembuatan playlist otomatis**
- **Analisis preferensi pasar musik**

---

## 🧠 Algoritma yang Digunakan

### K-Means Clustering

- Cocok untuk eksplorasi data **tanpa label**
- Mudah digunakan dengan `sklearn.cluster.KMeans`
- Hasilnya dapat divisualisasikan dalam bentuk **2D scatter plot** (PCA/t-SNE)

---

## 📚 Referensi Ilmiah

1. **A Comparative Study on Music Clustering Algorithms**  
   *International Journal of Computer Applications (2020)*  
   👉 Menunjukkan efektivitas K-Means untuk pengelompokan lagu berdasarkan tempo dan fitur audio  
   `[Link PDF]`

2. **Music Classification and Clustering Based on Audio Features**  
   *IEEE Conference, 2021*  
   👉 Kombinasi K-Means dan DBSCAN untuk clustering berdasarkan danceability, energy, dan tempo  
   `[DOI Link]`

3. **Clustering Music Tracks Using Machine Learning Algorithms**  
   *Journal of Intelligent Systems Research (2022)*  
   👉 Fokus pada pengelompokan lagu Spotify dan YouTube untuk playlist otomatis  
   `[Link]`

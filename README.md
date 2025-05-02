# Laporan Proyek Machine Learning - Muhammad Azhar Fikri
Proyek Akhir dari kelas Machine Learning Terapan.

## Project Overview

![hy](assets/hyouka.gif)

Anime adalah bentuk hiburan asal Jepang yang telah mendunia, mencakup berbagai genre seperti aksi, drama, fantasi, dan romansa. Dengan ribuan judul yang tersedia, pengguna sering kali kesulitan memilih anime yang sesuai dengan preferensi mereka. Oleh karena itu, sistem rekomendasi menjadi alat penting untuk membantu pengguna menemukan anime yang relevan dengan minat mereka.

Sistem rekomendasi anime diperlukan untuk membantu pengguna memilih anime yang sesuai dengan preferensi mereka, mengingat banyaknya pilihan anime yang tersedia dengan berbagai genre dan tema. Tanpa bantuan sistem rekomendasi, pengguna akan kesulitan menemukan anime yang cocok dengan minat pribadi mereka, yang bisa berujung pada pengalaman menonton yang kurang menyenangkan. Selain itu, seiring dengan pertumbuhan platform streaming yang menyediakan ribuan anime, pencarian manual tanpa sistem yang terorganisir akan semakin menjadi tantangan besar bagi pengguna baru dan lama.

Sistem rekomendasi anime dibangun dengan dua pendekatan utama:

- **Content-Based Filtering**: Menggunakan fitur-fitur dari anime itu sendiri, seperti genre, studio, atau sinopsis, untuk memberikan rekomendasi. Pendekatan ini berfokus pada kesamaan karakteristik anime yang sudah diketahui oleh pengguna sebelumnya.[[1](https://medium.com/web-mining-is688-spring-2021/content-based-anime-recommendation-4d74038fab67)]

- **Collaborative Filtering**: Mengandalkan data interaksi pengguna sebelumnya untuk merekomendasikan anime berdasarkan kesamaan preferensi antar pengguna. Pendekatan ini memanfaatkan informasi tentang perilaku pengguna yang mirip, seperti anime yang sering ditonton bersama atau dinilai tinggi oleh pengguna lain yang memiliki preferensi serupa.[[2](https://www.ewadirect.com/proceedings/tns/article/view/16509)]

Berdasarkan penelitian yang ada, penggunaan metode **Content-Based Filtering** memungkinkan rekomendasi yang lebih terarah berdasarkan kesamaan konten, meskipun pendekatan ini mungkin tidak sepenuhnya menangkap preferensi dinamis pengguna. Di sisi lain, **Collaborative Filtering** telah terbukti efektif dalam memberikan rekomendasi yang relevan, meskipun ada tantangan seperti masalah **cold-start** pada pengguna baru. Dengan latar belakang tersebut, proyek ini bertujuan untuk membangun sistem rekomendasi anime yang efektif dan efisien, yang dapat membantu pengguna menemukan anime yang sesuai dengan preferensi mereka.

## Business Understanding
Sistem rekomendasi anime bertujuan untuk mempermudah pengguna dalam menemukan anime yang sesuai dengan preferensi mereka, dengan memanfaatkan data dari berbagai fitur anime maupun interaksi pengguna. Dengan banyaknya anime yang tersedia, pengguna memerlukan sistem yang efisien untuk memilah dan merekomendasikan anime yang paling relevan.[[3](https://www.researchgate.net/publication/377022593_Analyzing_the_Effectiveness_of_Collaborative_Filtering_and_Content-Based_Filtering_Methods_in_Anime_Recommendation_Systems)]

### Problem Statements

Menjelaskan pernyataan masalah:
- Bagaimana cara merancang sistem rekomendasi yang mampu menyarankan anime kepada pengguna berdasarkan kemiripan genre dari anime yang pernah mereka sukai?
- Bagaimana memanfaatkan data interaksi pengguna, seperti rating untuk memberikan rekomendasi anime yang belum pernah ditonton oleh pengguna tersebut?
- Bagaimana membangun dan menerapkan algoritma sistem rekomendasi seperti Cosine Similarity dan K-Nearest Neighbors untuk menghasilkan rekomendasi yang relevan dan personal?
- Bagaimana melakukan evaluasi terhadap performa model sistem rekomendasi yang dibangun agar dapat diketahui tingkat akurasi dan efektivitasnya?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- **Mengembangkan sistem rekomendasi berbasis konten** yang mampu mengukur kemiripan antar anime berdasarkan genre, sehingga pengguna dapat memperoleh saran anime yang sejenis dengan preferensi sebelumnya.

- **Menerapkan pendekatan collaborative filtering** yang memanfaatkan rating pengguna lain untuk menyarankan anime baru kepada pengguna yang memiliki selera serupa.

- **Mengimplementasikan model rekomendasi dengan algoritma Cosine Similarity dan K-Nearest Neighbors (KNN)** untuk menghasilkan rekomendasi yang akurat dan dapat diandalkan.

- **Melakukan evaluasi performa sistem rekomendasi** menggunakan metrik evaluasi clustering seperti **Davies-Bouldin** dan **Calinski-Harabasz** untuk mengukur kualitas pemisahan dan kerapatan antar cluster hasil sistem rekomendasi. Semakin rendah skor Davies-Bouldin dan semakin tinggi skor Calinski-Harabasz, maka semakin baik performa model dalam mengelompokkan data yang serupa.

### Solution Statements

Untuk mencapai tujuan di atas, digunakan beberapa pendekatan berikut:
- **Content-Based Filtering dengan Cosine Similarity**:  
  Menggunakan representasi teks seperti genre yang dikonversi ke dalam bentuk vektor (TF-IDF), kemudian dihitung tingkat kemiripannya dengan cosine similarity.

- **Collaborative Filtering dengan K-Nearest Neighbors**:  
  Memanfaatkan data rating pengguna dan mengukur kemiripan antar pengguna atau antar item untuk memberikan rekomendasi berdasarkan perilaku pengguna lain yang serupa.

- **Evaluasi Model dengan Davies-Bouldin dan Calinski-Harabasz**:  
  Digunakan untuk mengukur efektivitas pengelompokan (clustering) dalam sistem rekomendasi. Davies-Bouldin menilai seberapa baik cluster dipisahkan (semakin rendah semakin baik), sedangkan Calinski-Harabasz mengukur rasio antara variasi antar cluster dan dalam cluster (semakin tinggi semakin baik).

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

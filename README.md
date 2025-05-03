# Laporan Proyek Machine Learning - Muhammad Azhar Fikri
Proyek Akhir dari kelas Machine Learning Terapan.

## Project Overview

![hyouka](assets/hyouka.gif)

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

Dataset yang digunakan dalam proyek ini diperoleh dari platform [Kaggle](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database), yang berjudul **Anime Recommendations Database**. Dataset ini berisi informasi preferensi anime berdasarkan data 76,000 users pada [MAL](https://myanimelist.net) 8 tahun yang lalu.

Dataset terdiri dari **12.294 entri** yang mencakup berbagai atribut penting yang berhubungan dengan karakteristik dan popularitas anime. Informasi ini sangat berguna untuk membangun sistem rekomendasi berbasis konten maupun kolaboratif.

### Sumber Dataset
Kaggle: [Anime Recommendations Database](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database)

### Variabel-variabel pada Dataset Anime

Berikut adalah deskripsi dari setiap fitur yang terdapat dalam dataset utama `anime.csv`:

- **anime_id**: ID unik untuk masing-masing anime. Digunakan sebagai identifikasi primer.
- **name**: Nama dari anime.
- **genre**: Genre atau kategori dari anime. Beberapa anime memiliki lebih dari satu genre, dipisahkan oleh koma.
- **type**: Jenis anime (misalnya: TV, Movie, OVA, Special, dll).
- **episodes**: Jumlah episode dari anime. Nilai ini dapat berupa angka atau string `'Unknown'` jika data tidak tersedia.
- **rating**: Rata-rata rating yang diberikan oleh pengguna terhadap anime tersebut (skala 1–10).
- **members**: Jumlah anggota yang telah memberikan rating atau yang menambahkan anime tersebut ke daftar tontonan mereka.

### Exploratory Data Analysis (EDA)

Beberapa langkah yang telah dilakukan untuk memahami data lebih dalam:

1. **Missing Value**  
   - Beberapa nilai yang kosong pada kolom **genre** (62 nilai kosong), **type** (25 nilai kosong), dan **rating** (230 nilai kosong).
   - Diperlukan penanganan nilai-nilai yang hilang atau tidak valid sebelum melakukan pemodelan.

2. **Layanan Penayangan Anime**  
   - Platform yang paling umum menayangkan anime adalah "TV", disusul oleh "OVA", "Movie", dan "Special".

![type](assets/type.png)

3. **Genre Anime Terpopuler**  
   - Genre paling populer adalah "Comedy", "Action", "Advnture".
   - Mayoritas anime memiliki lebih dari satu genre, menunjukkan keragaman tema dalam satu judul.

![genre](assets/genre.png)

4. **Anime dengan Fandom/Komunitas Terbesar**  
   - Anime seperti **Death Note**, **Shingeki no Kyojin**, dan **Sword Art Online** memiliki jumlah anggota komunitas terbanyak, menandakan popularitas tinggi.
   - Sebagian besar anime ini berasal dari genre action/supernatural yang memang populer di kalangan penonton.

![fandom](assets/fandom.png)

| No. | Judul Anime                               | Jumlah Anggota |
|-----|--------------------------------------------|----------------|
| 1   | Death Note                                 | 1,013,917      |
| 2   | Shingeki no Kyojin                         | 896,229        |
| 3   | Sword Art Online                           | 893,100        |
| 4   | Fullmetal Alchemist: Brotherhood           | 793,665        |
| 5   | Angel Beats!                               | 717,796        |
| 6   | Code Geass: Hangyaku no Lelouch            | 715,151        |
| 7   | Naruto                                     | 683,297        |
| 8   | Steins Gate                                | 673,572        |
| 9   | Mirai Nikki                                | 657,190        |
| 10  | Toradora!                                  | 633,817        |

5. **Anime dengan Rating Tertinggi**  
   - Beberapa anime dengan rating tertinggi seperti **Taka no Tsume 8** dan **Spoon-hime no Swing Kitchen** memiliki episode tunggal, biasanya dalam bentuk film pendek atau special.
   - Judul terkenal seperti **Fullmetal Alchemist: Brotherhood** dan **Kimi no Na wa** juga termasuk dalam daftar teratas, menunjukkan kombinasi kualitas produksi dan cerita yang kuat.

![rating](assets/rating.png)

| No. | Judul Anime                                               | Rating |
|-----|------------------------------------------------------------|--------|
| 1   | Taka no Tsume 8: Yoshida-kun no X-Files                   | 10.00  |
| 2   | Spoon-hime no Swing Kitchen                               | 9.60   |
| 3   | Mogura no Motoro                                          | 9.50   |
| 4   | Kimi no Na wa                                             | 9.37   |
| 5   | Kahei no Umi                                              | 9.33   |
| 6   | Fullmetal Alchemist: Brotherhood                          | 9.26   |
| 7   | Yakusoku: Africa Mizu to Midori                           | 9.25   |
| 8   | Gintama 0                                                 | 9.25   |
| 9   | Steins Gate                                               | 9.17   |
| 10  | Gintama 1                                                 | 9.16   |

## Modeling
Dalam proyek ini, dua algoritma utama digunakan untuk membangun sistem rekomendasi, yaitu **Cosine Similarity** untuk pendekatan *Content-Based Filtering* dan **K-Nearest Neighbors (KNN)** untuk pendekatan *Collaborative Filtering*.

### 1. Content-Based Filtering dengan Cosine Similarity

Content-Based Filtering memberikan rekomendasi berdasarkan kemiripan antara item (dalam hal ini anime) yang dihitung dari fitur-fitur kontennya, seperti genre, type, dan rating. Salah satu teknik yang umum digunakan untuk mengukur kemiripan antar item adalah **Cosine Similarity**.

**Cosine Similarity** mengukur sudut kosinus antara dua vektor dalam ruang vektor. Nilai cosine similarity berada pada rentang 0 hingga 1. Nilai 1 menunjukkan bahwa kedua vektor sangat mirip (arahnya sama), sedangkan nilai 0 menunjukkan bahwa kedua vektor benar-benar berbeda (arahnya tegak lurus).

**Rumus Cosine Similarity:**

$$
\text{Cosine Similarity} = \frac{A \cdot B}{\|A\| \times \|B\|}
$$

di mana:
- \( A \) dan \( B \) adalah vektor fitur dari dua anime.
- \( A \cdot B \) adalah dot product antara dua vektor.
- \( \|A\| \) dan \( \|B\| \) adalah norma (panjang) masing-masing vektor.

Anime yang memiliki nilai cosine similarity tertinggi dengan anime yang disukai pengguna akan direkomendasikan.

#### Kelebihan:
- Tidak bergantung pada interaksi pengguna lain, sehingga dapat direkomendasikan meskipun pengguna baru.
- Dapat memberikan rekomendasi yang sangat relevan dengan preferensi pengguna.
- Mudah diimplementasikan dan diinterpretasikan.

#### Kekurangan:
- Tidak menangkap tren umum atau kolektif dari komunitas pengguna.
- Terbatas pada konten yang diketahui; sulit merekomendasikan sesuatu di luar preferensi sebelumnya.
- Membutuhkan representasi fitur konten yang baik dan konsisten.

### 2. Collaborative Filtering dengan K-Nearest Neighbors (KNN)

Collaborative Filtering memberikan rekomendasi berdasarkan interaksi antar pengguna, seperti rating. Pendekatan **User-Based KNN** mencari pengguna yang mirip (nearest neighbors) berdasarkan pola rating, lalu merekomendasikan anime yang disukai oleh tetangga terdekat tersebut.

**Langkah-langkah utama:**
1. Menghitung kemiripan antar pengguna atau item (misalnya dengan cosine similarity).
2. Menentukan K tetangga terdekat (nearest neighbors) dari pengguna target.
3. Mengambil item yang disukai oleh tetangga tersebut dan belum pernah ditonton oleh pengguna target.
4. Mengurutkan item berdasarkan skor gabungan dan merekomendasikan top-N item.

#### Kelebihan:
- Menangkap pola kolektif atau tren dalam komunitas pengguna.
- Dapat memberikan rekomendasi yang bersifat "surprising" atau tidak terduga, karena berasal dari preferensi pengguna lain.
- Tidak membutuhkan deskripsi konten dari item (tidak perlu metadata).

#### Kekurangan:
- Rentan terhadap masalah cold-start (untuk pengguna/item baru tanpa cukup interaksi).
- Performa menurun pada dataset yang sangat besar tanpa optimasi.
- Bisa menghasilkan rekomendasi bias jika mayoritas pengguna memberikan rating serupa.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

# System-recomandation-content-Based-Filtering
## Project Overview
Dalam era digital yang terus berkembang, industri film telah menghasilkan ribuan judul dengan berbagai genre, tema, dan cerita. Platform penyedia konten film seperti Netflix, Disney+, dan HBO Max menawarkan banyak pilihan, namun hal ini justru dapat membuat pengguna kesulitan menemukan film yang sesuai dengan preferensi mereka. Kebiasaan masyarakat yang semakin mengandalkan transaksi secara online menunjukkan bahwa pengguna membutuhkan sistem yang efisien untuk menemukan produk yang diinginkan, termasuk film.

Penelitian oleh [(Azizah and Rozi 2024)](https://doi.org/10.47233/jteksis.v6i3.1411) mengembangkan sistem rekomendasi berbasis Content-Based Filtering dan algoritma cosine similarity untuk membantu konsumen memilih produk skincare. Hasilnya menunjukkan bahwa sistem ini mampu meningkatkan kepuasan konsumen, dengan nilai cosine similarity tertinggi mencapai 0,722. Inovasi ini menunjukkan potensi besar bagi penerapan sistem rekomendasi dalam berbagai bidang, termasuk industri kuliner.

Di sisi lain, penelitian oleh [(Azri Saputra, Huizen, and Arianto 2024)](https://doi.org/10.26623/transformatika.v22i1.7041) menyoroti pentingnya sistem rekomendasi dalam industri film streaming. Penelitian ini mengembangkan sistem rekomendasi film menggunakan metode Content-Based Filtering dan algoritma TF-IDF serta Cosine Similarity. Hasilnya menunjukkan bahwa sistem ini mampu memberikan rekomendasi yang relevan, dengan nilai akurasi hingga 0,7973 untuk tipe show dan 0,7022 untuk tipe movie.

Perkembangan sistem rekomendasi berbasis Content-Based Filtering dan Cosine Similarity terbukti efektif dalam memberikan rekomendasi yang personal dan relevan, sekaligus mengatasi masalah cold-start pada pengguna baru. Tingginya nilai akurasi dalam penelitian menunjukkan bahwa sistem ini mampu menjadi solusi atas kebingungan pengguna dalam memilih film di tengah banyaknya opsi di platform streaming. Dengan demikian, penerapan sistem rekomendasi yang tepat tidak hanya memenuhi kebutuhan masyarakat di era digital, tetapi juga meningkatkan kepuasan pengguna secara signifikan.

## Business Understanding
### Problem Statements
- Pernyataan Masalah 1
Banyaknya pilihan film di platform streaming membuat pengguna kesulitan menemukan konten yang sesuai dengan preferensi mereka.
- Pernyataan Masalah 2
Sistem rekomendasi yang ada sering memberikan saran terlalu umum tanpa mempertimbangkan preferensi genre spesifik pengguna.
- Pernyataan Masalah 3
Pengguna baru sering kali tidak mendapatkan rekomendasi yang akurat karena sistem belum memiliki data preferensi mereka.

### Goals
- Jawaban pernyataan masalah 1
Membangun sistem yang membantu pengguna menemukan film sesuai minat mereka secara efisien.
- Jawaban pernyataan masalah 2
Memberikan rekomendasi film yang benar-benar sesuai dengan genre khusus yang diinginkan.
- Jawaban pernyataan masalah 3
Memastikan pengguna baru langsung mendapatkan rekomendasi relevan hanya berdasarkan pilihan genre awal.

### Solution statements
- Menerapkan TF-IDF untuk mengubah data genre tekstual menjadi representasi numerik yang bermakna. Pendekatan ini memberikan bobot cerdas pada setiap genre dengan mempertimbangkan frekuensi kemunculannya di setiap film dan kelangkaannya di seluruh katalog, sehingga kombinasi genre yang unik mendapatkan penekanan yang tepat.
- Menerapkan cosine similarity, yang mana sistem akan melakukan perbandingan sistematis terhadap vektor genre untuk mengidentifikasi film-film dengan kesamaan tematik tertinggi. Pendekatan ini bekerja dengan mengukur sudut antara vektor-vektor genre dalam ruang multidimensi, dimana nilai 1 menunjukkan kesamaan genre sempurna dan nilai 0 mengindikasikan ketidakmiripan sama sekali.

## Data Understanding
Dataset tersebut adalah data yang berisi informasi tentang judul movie dan genre movie, yang mana memiliki jumlah data 9742 baris dan 3 kolom.  Untuk Dataset dapat diunduh di website grouplens dengan dataset [MovieLens](https://grouplens.org/datasets/movielens/)

### Variabel-variabel pada Dataset ini adalah sebagai berikut:
* movieId : Mempresentasikan Id untuk setiap movie.
* title : Mempresentasikan judul movie, yang mana diimpor dari <https://www.themoviedb.org/>, dan menyertakan tahun rilis dalam tanda kurung
* genres : Mempresentasikan Genre yang terdapat untuk setiap movies

### Exploratory Data Analysis
- Memeriksa pada dataset apakah memiliki nilai nan/kosong dan memeriksa apakah memiliki data yang duplikat, yang mana diketahui  bahwa tidak ada data kosong dan duplicate pada dataset.
![alt text](https://github.com/Donsss/IMAGE/blob/main/MLT%202/Screenshot%202025-05-29%20141532.png?raw=true)
- Mencari daftar unik pada kolom genre, yang mana diketahui bahwa terdapat data yang berisi '(no', 'genres', 'listed)'. Setelah melakukan pengecekan, diketahui bahwa jumlah data dengan genre (no genres listed) berjumlah 34.
![alt text](https://github.com/Donsss/IMAGE/blob/main/MLT%202/genre.png?raw=true)

- Melakukan pengecekan untuk stiap genre, untuk mengetahui genre apa yang paling banyak. Yang mana adalah genre drama memiliki jumlah movie terbanyak dengan total jumlah film 4000 lebih. 
![alt text](https://github.com/Donsss/IMAGE/blob/main/MLT%202/jumlah%20genre.png?raw=true)

- Menganalisis tahun film dirilis dengan membuat kolom baru year untuk melakukan analisis. Yang diketahui ada 13 judul yang tidak memiliki tahun dan rentang tahun movie dari tahun 1902 sampai 2018 yang ada pada dataset.

- Kemudian, Melakukan binning dengan 6 kelompok binning yang mana dengan rentang 21 tahun untuk setiap kelompoknya. yang mana, diketahui rentang tahun 1990-2011  memiliki jumlah judul movie terbanyak yaitu 5562 judul movis dan rentang tahun 1902-1923 memiliki judul movie paling sedikit yaitu hanya 14 judul movies.
![alt text](https://github.com/Donsss/IMAGE/blob/main/MLT%202/distribusi%20film.png?raw=true)

## Data Preparation
Pada tahap ini, data akan dipersiapkan untuk analisis lebih lanjut. Proses ini mencakup pembersihan data dan penghapusan informasi yang tidak relevan guna memastikan bahwa dataset yang digunakan tetap konsisten.
- Hal yang pertama dilakukan adalah membuat  membuat kolom baru bernama genre yang berisi data hasil split dari kolom genres, yang mana data nya akan menjadi list. Kemudian, menggunakan apply untuk untuk mengubahnya elemen list mejadi satu string.
```sh
data['genre'] = data['genres'].str.split('|')
data['genre'] = data['genre'].apply(' '.join)
```
- Membuat kolom year untuk memeriksa apakah ada semua judul film memiliki tahun. Yang mana menggunakan metode str.extract() untuk mencari pola dalam string. untuk mencari angka 4 digit yang diapit oleh tanda kurung dan Jika ada nilai yang tidak terisi (NaN)  nilai tersebut akan diganti dengan 0 serta mengubah tipe datanya menjadi int.
```sh
data['year'] = data['title'].str.extract(r'\((\d{4})\)')
data['year'] = data['year'].fillna(0).astype(int)
```
- Pada tahap ini membuat varibel baru untuk menyimpan hasil processing. Menghapus data (no genres listed) pada kolom genre, karena model rekomendasi ini memnggunakan genre untuk rekomendasinya, pada data tersebut hanya memiliki 34 data yang mana dapat mengganggu. Kemudian, menghapus data yang nama movies nya tidak memiliki tahun yang berjumlah 13 data, menghapus data tersebut karena agar format judul sama untuk semua dataset.
```sh
movies = data[(data['genre'] != '(no genres listed)') & (data['year'] != 0)]
movies.info()
```

- Menghapus kolom yang sudah tidak digunakan, yang mana kolom tersebut digunakan hanya untuk melakukan analsis. penghapusan kolom dilakukan agar membantu menyederhanakan dataset dan Menghemat Ruang Penyimpanan.
```sh
movies = movies.drop(['movieId', 'genres', 'year'], axis=1)
movies.head()
```
- Model ini menggunakan TF-IDF Vectorizer untuk mengubah data genre film menjadi representasi numerik. Proses ini dimulai dengan membangun vocabulary dari seluruh genre yang ada dalam dataset (tf.fit(movies['genre'])), kemudian menghasilkan daftar kata unik yang digunakan (tf.get_feature_names_out()). Selanjutnya, data genre diubah menjadi matriks TF-IDF (tfidf_matrix), di mana setiap baris merepresentasikan sebuah film dan setiap kolom mewakili term dari genre. 


## Modeling
Model bekerja dengan memanfaatkan matriks TF-IDF hasil pra-pemrosesan untuk menghitung kemiripan antar film melalui cosine similarity. Metrik ini membandingkan arah vektor genre setiap pasangan film dalam ruang multidimensi, di mana nilai mendekati 1 menunjukkan kesamaan tinggi. Matriks kemiripan yang dihasilkan menjadi basis rekomendasi dengan mengidentifikasi film-film terdekat secara relevan.

Fungsi rekomendasi (movies_recommendations) bekerja dengan mengambil indeks film-film terdekat berdasarkan nilai kemiripan tertinggi menggunakan argpartition untuk efisiensi komputasi. Sistem kemudian menyaring judul yang sama dan mengembalikan 10 rekomendasi teratas yang diurutkan dari nilai tertinggi. Pendekatan ini memastikan rekomendasi bersifat personal dengan kompleksitas algoritma yang optimal.
```sh
def movies_recommendations(title, similarity_data=cosine_sim_df, items=movies[['title', 'genre']], k=10):
    index = similarity_data.loc[:,title].to_numpy().argpartition
    (range(-1, -k, -1))
    closest = similarity_data.columns[index[-1:-(k+2):-1]]
    closest = closest.drop(title, errors='ignore')
    return pd.DataFrame(closest).merge(items).head(k)
```

Untuk hasil nya menggunkanan judul film Grumpier Old Men (1995), yang mana akan merekomendasikan top-10 judul film dengan genre yang mirip atau sama.
![alt text](https://github.com/Donsss/IMAGE/blob/main/MLT%202/top.png?raw=true)

### Kelebihan
- Pendekatan berbasis TF-IDF dan cosine similarity relatif mudah dipahami dan diterapkan, bahkan untuk pemula dalam machine learning. Teknik ini tidak memerlukan arsitektur model yang kompleks sehingga cocok untuk sistem rekomendasi dasar.
- Berbeda dengan collaborative filtering, metode ini hanya memerlukan informasi genre, sehingga tetap bisa bekerja meskipun tidak ada data preferensi pengguna.
- Untuk dataset yang tidak terlalu besar, perhitungan cosine similarity dapat dilakukan dengan cepat, membuatnya efisien untuk kasus penggunaan sederhana.

### Kekurangan
- Karena hanya menggunakan data genre, model ini tidak mempertimbangkan faktor lain seperti rating, popularitas, atau preferensi spesifik pengguna, sehingga rekomendasinya mungkin kurang relevan.
- Rekomendasi yang dihasilkan sama untuk semua pengguna yang mencari film tertentu, tanpa mempertimbangkan selera individu.


## Evaluation
Pada tahap evaluasi model, penting untuk menggunakan metrik yang tepat untuk menilai performa algoritma yang telah diterapkan. Berikut adalah 2 metrik evaluasi yang digunakan precision@k dan Average Precision@k.
1. **precision@k** 
Precision@k adalah metrik yang digunakan untuk mengevaluasi efektivitas sistem rekomendasi atau pencarian informasi. Metrik ini mengukur seberapa banyak item relevan yang ditemukan dalam k item teratas yang direkomendasikan
Formula :
![Akurasi](https://cdn.prod.website-files.com/660ef16a9e0687d9cc27474a/662c4327f27ee08d3e4d4b34_65777ee1fd55288155f28d37_precision_recall_k2.png)
Cara kerja:
Prosesnya dimulai dengan sistem memberikan k rekomendasi kepada pengguna. Dari daftar tersebut, evaluasi dilakukan untuk menentukan jumlah item yang memang relevan. Kemudian, precision dihitung dengan membagi jumlah item relevan dengan k, memberikan nilai yang mencerminkan seberapa baik sistem dalam menyajikan konten yang sesuai dengan kebutuhan pengguna.

2. **Average Precision@k (AP@k)**
Average Precision@k (AP@k) adalah metrik yang mengukur kualitas hasil yang diperoleh dari sistem rekomendasi atau pencarian dengan mempertimbangkan urutan relevansi item. Metrik ini memberikan gambaran yang lebih komprehensif dibandingkan Precision@k dengan menghitung rata-rata precision pada setiap posisi relevan dalam k item teratas.
![precision](https://cdn.prod.website-files.com/660ef16a9e0687d9cc27474a/662c432c08687cce06cf3df9_657785177018267e55a25642_mean_average_precision4.png)
Cara kerjanya: 
 Prosesnya dimulai dengan sistem memberikan k rekomendasi, di mana kemudian item relevan diidentifikasi. Selanjutnya, precision dihitung untuk setiap posisi di mana item relevan muncul, dengan cara membagi jumlah item relevan hingga posisi tersebut dengan total item yang diperiksa.

Pada tahap ini melakukan evaluasi menggunakana 10 judul film, yang mana untuk mengukur P@K dan AP@K dengan nilai K=10, untuk hasil evaluasinya sebagai berikut:

| Judul Film                         | P@k | AP@k |
|------------------------------------|-----|------|
| Grumpier Old Men (1995)            | 1.00 | 1.00 |
| Jumanji (1995)                     | 1.00 | 1.00 |
| Father of the Bride Part II (1995) | 1.00 | 1.00 |
| Dracula: Dead and Loving It (1995) | 1.00 | 1.00 |
| Mars Needs Moms (2011)             | 0.00 | 0.00 |
| Toy Story (1995)                   | 0.80 | 0.80 |
| Limitless (2011)                   | 1.00 | 1.00 |
| Host, The (2013)                   | 0.40 | 0.80 |
| In the Heart of the Sea (2015)     | 1.00 | 1.00 |
| Justice League (2017)              | 1.00 | 1.00 |

Hasil evaluasi model untuk rekomendasi menunjukkan kinerja yang bervariasi di antara film yang diuji. Seperti, Film seperti Grumpier Old Men (1995) dan Jumanji (1995) mencapai Precision@K dan Average Precision@K sebesar 1.00, menandakan semua rekomendasi relevan. Sebaliknya, Mars Needs Moms (2011) mendapatkan skor 0 di kedua metrik, menunjukkan bahwa tidak ada rekomendasi relevan yang diberikan, yang bisa mengindikasikan masalah pada data atau fitur yang digunakan. Variasi juga terlihat pada film lain, seperti Toy Story (1995) (Precision 0.80, AP 0.80) dan Host, The (2013) (Precision 0.40, AP 0.80), yang menunjukkan bahwa ada beberapa rekomendasi yang cukup relevan sedikit relevan.

# Daftar Pustaka
Nailatul Azizah and Anief Fauzan Rozi, “Sistem Rekomendasi Produk Somethinc Menggunakan Metode Content-based Filtering,” Jurnal Teknologi Dan Sistem Informasi Bisnis, vol. 6, no. 3, pp. 461–468, Jul. 2024, doi: https://doi.org/10.47233/jteksis.v6i3.1411.

Jeremia Maheswara Azri Saputra, L. M. Huizen, and D. B. Arianto, “Sistem Rekomendasi Film pada Platform Streaming Menggunakan Metode Content-Based Filtering,” Jurnal Transformatika, vol. 22, no. 1, pp. 10–10, Aug. 2024, doi: https://doi.org/10.26623/transformatika.v22i1.7041.



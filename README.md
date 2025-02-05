# Laporan Proyek Machine Learning - Caraka Rahman

## Project Overview

Industri perfilm-an menjadi salah satu industri yang paling berkembang di dunia, ini ditandai dengan berkembangnya teknologi yang digunakan dalam tahapan produksi film. Sebagai contoh film pada rumah produksi MCU(_Marvel Cinematic Universe_), Teknologi berbasis AI(Artificial Intelligence) diimplementasi pada 2 tahap pembuatan film, diantaranya proses pembuatan **Storyline** dan juga **Visual Effects**[[1]](https://medium.com/@jeyadev_needhi/the-marvel-ous-world-of-ai-how-artificial-intelligence-powers-the-marvel-cinematic-universe-part-1d92127ec96a).

![MCU](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/MCU-Logo.png "MCU")

Selain itu, Teknik Pemasaran film pun merupakan faktor lain yang menyebabkan industri ini sangat berkembang. Jika _flashback_ ke masa lalu, film hanya ditayangkan melalui bioskop, CD, DVD, dll. Tetapi di zaman sekarang, sangat banyak _platform_ penyedia streaming film, sebagai contoh Netflix, Vidio, Disney Hotstars, dll.

Masing-masing dari _platform_ tersebut dibekali dengan teknologi canggih berbasis AI, salah satunya adalah Sistem Rekomendasi(RecSys). Yang mana sistem ini bertugas untuk memberikan rekomendasi film kepada setiap users dari aplikasi tersebut. Walaupun terlihat sudah bekerja dengan sangat baik, tetapi Sistem Rekomendasi ini masih menjadi sistem yang terus dikembangkan hingga saat ini demi mencapai performa yang sangat optimal. Dikarenakan terkadang pada beberapa platform, film yang di rekomendasikan dirasa kurang relevant.

Dari permasalahan yang telah dijelaskan di atas, maka project ini bertujuan untuk membuat 2 ML Model Sistem Rekomendasi dengan menggunakan 2 metode berbeda, yaitu **content-based filtering** dan **collaborative filtering**.

## Business Understanding

### Problem Statements
Berdasarkan kondisi yang telah diuraikan sebelumnya, maka ML Model Sistem Rekomendasi ini dibuat untuk menjawab beberapa permasalahan berikut:
1. Bagaimana cara memproses data film, pengguna, dan rating agar informasinya dapat digunakan untuk membuat ML Model Sistem Rekomendasi?
2. Manakah Metode yang paling optimal dalam hal memberikan rekomendasi film?

### Goals

Berdasarkan problem statement yang telah diuraikan di atas, maka berikut goals atau tujuan dari dibangunnya model Sistem Rekomendasi ini:
1. Melakukan tahapan pemrosesan data dari mulai Data Collecting hingga Data Preprocessing sehingga data siap untuk digunakan pada model sistem rekomendasi.
2. Membangun ML Model yang dapat memberikan rekomendasi film seakurat mungkin berdasarkan data film, pengguna, dan rating yang sudah di proses sebelumnya.

### Solution statements
Untuk mencapai/meraih goals di atas, berikut merupakan tahapan-tahapan yang akan dilakukan:
1. Melakukan proses Data Preprocessing sebaik mungkin, guna menghasilkan data akhir yang berkualitas untuk keperluan sistem rekomendasi. Karena jika tidak dilakukan Data Preprocessing dengan baik, maka akan berpengaruh pada hasil akhir dari model yang dibangun.
2. Melakukan eksperimen menggunakan dua Metode berbeda untuk memperoleh model yang paling optimal. Metode yang akan digunakan diantaranya **Content-Based Filtering** dan **Collaborative Filtering**.

## Data Understanding
Datasets yang digunakan pada project ini di download dari website **GroupLens Research Project**. Ketika di download di dalam file **.zip** terdapat 7 files, yang diantaranya 6 files **.csv** yang merupakan file Datasets dan file **README** yang merupakan file berisi documentation. Berdasarkan file **README**, Datasets ini dibuat pada 21 November 2019 oleh 162.541 pengguna yang dikumpulkan pada rentang waktu 09 January 1995 hingga 21 November 2019.

![DatasetsImg](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/movielens25m.png "DatasetsImg")

Berikut merupakan informasi tambahan dari Datasets yang digunakan:

|            | Keterangan                                                                       |
|----------  | -----------------------------------------------------------------------          |
| Sumber     | [GroupLens Research Project](https://grouplens.org/datasets/movielens/)          |
| Extension  | .zip                                                                             |
| files .csv | genome-scores.csv, genome-tags.csv, links.csv, movies.csv, ratings.csv, tags.csv |
| Total Data | 25.000.095                                                                       |
| Size       | 249 MB                                                                           |
| Released   | 12/2019                                                                          |

### Penjelasan Masing - Masing Datasets:
1. **genome-scores.csv**
    
    Berikut merupakan informasi detail mengenai DataFrame nya:

    ![genome_scores](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/genome_scores%20info.png "genome_scores")

    - movieId: merepresentasikan ID film
    - tagId: merepresentasikan ID tag
    - relevance: merepresentasikan Score Relevansi

    | Jumlah Data  | Jumlah Kolom  | Missing Value | Duplicate |
    | :----------: | :----------:  | :----------:  | :-------: |
    |   15584448   |    3          | 0             | 0         |

2. **genome-tags.csv**

    Berikut merupakan informasi detail mengenai DataFrame nya:

    ![genome_tags](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/genome_tags%20info.png "genome_tags")

    - tagId: merepresentasikan ID tag
    - tag: merepresentasikan deskripsi tag

    | Jumlah Data | Jumlah Kolom  | Missing Value | Duplicate |
    | :---------: | :----------:  | :----------:  | :-------: |
    |     1128    |       2       | 0             | 0         |
    
3. **links.csv**

    Berikut merupakan informasi detail mengenai DataFrame nya:

    ![links](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/Links%20info.png "links")

    - movieId: merepresentasikan ID film yang merujuk pada website MovieLens
    - imdbId: merepresentasikan ID film yang merujuk pada website IMDB
    - tmdbId: merepresentasikan ID film yang merujuk pada website TMDB

    | Jumlah Data | Jumlah Kolom  | Missing Value | Duplicate |
    | :----------:| :----------:  | :----------:  | :-------: |
    |   62423     |     3         | 107             | 0         |

4. **movies.csv**

    Berikut merupakan informasi detail mengenai DataFrame nya:

    ![movies](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/Movies%20info.png "movies")

    - movieId: merepresentasikan ID film
    - title: merepresentasikan judul film
    - genres: merepresentasikan genre film

    | Jumlah Data | Jumlah Kolom  | Missing Value | Duplicate |
    | :----------:| :----------:  | :----------:  | :-------: |
    |   62423     | 3             | 0             | 0         |

5. **ratings.csv**

    Berikut merupakan informasi detail mengenai DataFrame nya:

    ![ratings](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/Ratings%20info.png "ratings")

    - userId: merepresentasikan ID user
    - movieId: merepresentasikan ID film
    - rating: merepresentasikan rating dari suatu film yang diberikan oleh user dalam rentang 0.5 - 5
    - timestamp: merepresentasikan kode timestamp

    | Jumlah Data | Jumlah Kolom  | Missing Value | Duplicate |
    | :----------:| :----------:  | :----------:  | :-------: |
    |   25000095  | 4             | 0             | 0         |

6. **tags.csv**

    Berikut merupakan informasi detail mengenai DataFrame nya:

    ![tags](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/Tags%20info.png "tags")

    - userId: merepresentasikan ID user
    - movieId: merepresentasikan ID film
    - tag: merepresentasikan tag dari suatu film
    - timestamp: merepresentasikan kode timestamp

    | Jumlah Data | Jumlah Kolom  | Missing Value | Duplicate |
    | :----------:| :----------:  | :----------:  | :-------: |
    |  1093360    | 4             | 16            | 0         |

### Exploratory Data Analysis(EDA)

Proses EDA ini dilakukan untuk menganalisis data pada Datasets guna mendapatkan pemahaman yang mendalam mengenai kondisi dari data, agar dapat mengetahui jika terdapat masalah, seperti missing values, duplicate data, dll.

#### Univariate Analysis

Untuk mempermudah proses Analysis, seluruh file Datasets akan dibagi menjadi 3 data secara umum berdasarkan **kategori** ID nya menjadi movies, users, dan genome. Kemudian akan dilihat jumlah data di masing-masing kategorinya.

- Genome Tags

![all_genome_tags](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/all_genome_tags.png "all_genome_tags")

- Movies

![all_movies](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/all_movies.png "all_movies")

- Users

![all_users](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/all_users.png "all_users")

Dari informasi di atas, dapat diketahui bahwa jumlah data pada relevancy score(**genome_scores**) sangatlah sedikit yaitu hanya berjumlah 1.128 data. Sedangkan jumlah data pada **movies** dan **users** masing-masing berjumlah 62.423 dan 162.541. Dikarenakan perbedaan jumlah data yang cukup significant ini, maka data yang akan digunakan pada project ini adalah **movies** dan **users**.

## Data Preparation
Berikut merupakan proses Data Preprocessing dan Data Preparation yang dilakukan pada project ini:

1. **Data Cleaning movies**

    Pada bagian **Data Understanding**, dapat dilihat bahwa pada DataFrame **movies** seluruh values pada feature **title** mengandung tahun terbit film. Sebagai contoh **"Toy Story (1995)"**, dimana ada dan tidak adanya keterangan tahun tidak akan berpengaruh terhadap genre dan juga rating dari film tersebut. Sehingga pada feature **title** ini akan dipisahkan antara judul dan tahunnya, kemudian akan dibuat satu feature baru bernama **year** untuk menyimpan informasi dari tahun tersebut. Berikut merupakan hasilnya.

    ![SeperateYears](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/SeperateYears.png "SeperateYears")

2. **Data Cleaning ratings**

    Berdasarkan bagian **Data Understanding**, values dari feature rating pada DataFrame **ratings** dimulai dari 0.5 - 5. Dari kondisi ini, selanjutnya seluruh value akan dilakukan **pembulatan**, sebagai contoh 3.5 menjadi 4, 4.5 menjadi 5 dan seterusnya. Sehingga setelah dilakukan pembulatan ini rentang value menjadi 1 - 5.

    Setelah dilakukan pembulatan terhadap feature **rating**, jika dilihat value pada feature **timestamp** sulit dipahami. Sehingga akan dilakukan convertion dari bentuk timestamp ke bentuk datetime. Berikut hasilnya.

    ![datetime](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/datetime.png "datetime")

3. **Data Merging**

    Setelah selesai dilakukan proses Data Cleaning pada DataFrame **movies** dan **ratings**, langkah selanjutnya adalah menyatukan kedua DataFrame tersebut menjadi DataFrame baru bernama **movies_rating**. Berikut hasilnya.

    ![DataMerging](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/DataMerging.png "DataMerging")

4. **Data Reduction #1**

    Dikarenakan keterbatasan sumber daya komputasi, maka jumlah Data yang akan digunakan pada project ini akan **dikurangi**. Data yang awalnya berjumlah 25.003.471, akan dikurangi menjadi 1.000.000.

5. **Data Reduction #2**
    
    Berdasarkan Analysis yang dilakukan, ditemukan bahwa terdapat suatu title movie yang hanya mendapatkan **14** reviews, dan ada juga title movie yang sampai mendapatkan **59.184** reviews. Berdasarkan fakta ini, demi memiliki data yang berkualitas, untuk selanjutnya film yang memiliki jumlah pemberi rating < 100 akan di drop dari DataFrame.

    Setelah dilakukan penghapusan, DataFrame yang awalnya berjumlah **1.000.000** data, sekarang total datanya menjadi **999.243** data.</p>

6. **Replace Values**

    Dari hasil Data Analysis yang dilakukan terhadap DataFrame **movies_rating**, pada feature **genres** terdapat genre berjenis **Sci-Fi**, **Sci-Fi** merupakan akronim dari kata Science Fiction yang menggambarkan film fiksi ilmiah. Pada kata ini mengandung karakter "dash", yang mana apabila tidak dihilangkan ketika dilakukan perhitungan TF-IDF, kata ini akan diperlakukan sebagai 2 kata yang berbeda **Sci** dan **Fi**. Karena pada tahap TF-IDF selain melakukan vektorisasi juga melakukan tokenisasi.

7. **Remove Duplicate Data**

    Setelah dilakukan proses **Replace Values**, selanjutnya akan dilakukan pengecekan duplikasi data terhadap DataFrame. Berdasarkan hasil pengecekan tersebut, ternyata DataFrame mengandung data Duplicate sebanyak 999.115 data. Maka selanjutnya data duplikat ini akan di drop dari DataFrame.

    Setelah dilakukan penghapusan data duplicate, jumlah data yang tadinya **999.243** sekarang menjadi **128** data.

8. **DataFrame to List**

    Setelah dilakukan penghapusan data duplicate, proses selanjutnya adalah merubah values pada feature **movieId**, **Title**, **Genres** menjadi list, ini dilakukan untuk keperluan pada proses selanjutnya, yaitu pembuatan DataFrame baru.

9. **Create New DataFrame**

    Selanjutnya akan dibuat satu DataFrame baru yang bernama **df_movie**, yang mana terdiri dari 3 features diantaranya **id**, **title**, dan **genre**. Value-nya berasal dari variable list **movie_id**, **movie_title**, dan **movie_genre** yang sebelumnya sudah dibuat.

10. **Content-Based Filtering**
    - **TF-IDF Vectorizer**
     
        TF-IDF merupakan proses yang berfungsi untuk mentransformasikan teks menjadi representasi angka yang memiliki makna tertentu dalam bentuk matriks.

        Setelah proses ini selesai, Dimension dari Matrix yang didapatnya adalah **(128, 16)**. Berikut merupakan contoh dari hasil perhitungan TF-IDF.

        ![tfidf](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/TF-IDF.png "tfidf")

11. **Collaborative Filtering**
     - **Encode Label**

        Sebelum melakukan training model, Data harus dilakukan proses encoding terlebih dahulu terhadap fitur **userId** dan **movieId**. Ini merupakan proses yang berfungsi untuk merubah data kategorik menjadi data numerik.
    
     - **Mapping Encode**

        Setelah dilakukan proses encoding, kemudian nilai-nilai tersebut akan di Mapping kedalam DataFrame. Untuk hasilnya dapat dilihat pada gambar berikut.

        ![mapping](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/MappingCollaborative.png "mapping")

     - **Shuffling Data**

        Kemudian setelah dilakukan proses **Mapping**, selanjutnya DataFrame akan diacak secara random.
        
        Sehingga diperoleh jumlah users sebanyak **138.533**, jumlah film sebanyak **128**, nilai min rating adalah **1**, dan max rating adalah **5**.

     - **Data Splitting**

        Setelah dilakukan proses **Mapping** dan **pengacakan** pada DataFrame, langkah selanjutnya adalah DataFrame akan dibagi menjadi 2 bagian, yaitu **train_set** dan **val_set**. Dimana Proportion nya adalah **80% train_set** dan **20% val_set**.

## Modeling

Setelah melakukan tahap EDA dan Data Preprocessing, langkah selanjutnya adalah melakukan ML Model Development untuk Sistem Rekomendasi film, menggunakan metode **Content-Based Filtering** dan **Collaborative Filtering**.

1. **Content-Based Filtering**
    
   Content-Based Filtering merupakan suatu metode yang bekerja dengan cara memperhatikan kemiripan dari item yang disukai oleh user berdasarkan aktifitas user tersebut di masa lampau. Untuk menghitung tingkat kemiripan dari setiap data, dapat menggunakan formulas **Cosine Similarity**.

   - **Cosine Similarity**

     Cosine Similarity merupakan proses yang berfungsi untuk menghitung derajat kesamaan(similarity degree) antar judul film. Berikut merupakan persamaan dari **Cosine Similarity**,
     
     ![cosine](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/CosineEquation.png "cosine")

     Setelah selesai dilakukan perhitungan, Dimension dari matrix yang didapatkan adalah (128, 128). Berikut merupakan contoh dari hasil perhitungan Cosine Similarity.

        ![CosineSim](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/CosineSimilarity.png "CosineSim")

   - Top-N Recommendation

     Setelah melakukan perhitungan TF-IDF dan Cosine Similarity, model pun sudah siap untuk dilakukan pengujian. Berikut merupakan hasil Top-N Recommendation yang dihasilkan oleh model Content-Based Filtering.

     ![InputCB](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/InputContentBased.png "InputCB")

     Gambar di atas merupakan judul film yang dipilih oleh user.

     ![OutputCB](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/OutputContentBased.png "OutputCB")

     Dari hasil 5 recommendations di atas, terlihat bagaimana **Balto, Jumanji, Indian in the Cupboard, NeverEnding Story III, dan Muppet Treasure Island** merupakan movies yang di recommendation oleh ML Model berdasarkan movie Toy Story.
     
    Sekilas model sudah menghasilkan performa yang baik, tetapi untuk mengetahui seberapa baik performa dari model berdasarkan angka, pada BAB selanjutnya akan dilakukan perhitungan evaluasi menggunakan metrics Precision.

2. **Collaborative Filtering**

    Collaborative Filtering bekerja dengan cara bergantung pada pendapat komunitas pengguna. Metode ini tidak memerlukan atribut untuk setiap itemnya seperti pada Content-Based Filtering.

    - **Model Development**

      Setelah seluruh data sudah siap, langkah selanjutnya adalah pengembangan model yang bernama **RecommenderNet**. Model ini bekerja dengan menghitung kemiripan dari data film yang dicari, dan data yang memiliki tingkat kemiripan tinggi akan dimasukkan ke dalam variabel terdekat. Parameter **K** didefinisikan untuk menghasilkan rekomendasi teratas berdasarkan kemiripan tertinggi. Film yang dicari akan dihapus dari daftar agar tidak muncul dalam rekomendasi. Langkah terakhir adalah menggunakan perintah return untuk mengembalikan nilai dalam bentuk dataframe, di mana nilai yang dikembalikan merupakan rekomendasi film berdasarkan tingkat kemiripan. Berikut merupakan informasi tambahan yang digunakan pada model **RecommenderNet** ini,

      |       | Values |
      | :--- | ---  |
      | Loss  | Binary Crossentropy |
      | Optimizer | Adam |
      | metrics | RMSE |
      | batch_size | 32 |
      | epochs | 25 |

    - **Top-N Recommendation**

      Berikut merupakan hasil Top-N Recommendation dari model **Collaborative Filtering** yang dibangun.

      ![OutputColl](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/OutputCollaborative.png "OutputColl")

      Output di atas merupakan hasil dari recommendation ML Model Collaborative Filtering. Dimana user dengan id **24651** terlihat sangat menyukai movie dengan genre **Action**, **Crime**, dan **Thriller**.
      
      Kemudian model akan membandingkan antara film dengan rating tertinggi dari user dan semua film, kecuali film yang telah ditonton tersebut, lalu akan mengurutkan film yang akan direkomendasikan berdasarkan nilai rekomendasi yang tertinggi.
      
      Dan model pun berhasil memberikan 10 recommendation movies dengan genre yang serupa seperti film berjudul **The Usual Suspects**, dan **Hate (Haine, La)**.

    Sekilas model sudah menghasilkan performa yang baik, tetapi untuk mengetahui seberapa baik performa dari model berdasarkan angka, pada BAB selanjutnya akan dilakukan perhitungan evaluasi menggunakan metrics RMSE.


## Evaluation

1. **Content-Based Filtering**

    Pada tahap evaluasi model Content-Based Filtering, model dapat dievaluasi menggunakan metrics **precision**, berikut persamaannya:

    ![precision](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/RecSys-Precision.png "precision")

    Berikut merupakan hasil dari pengembangan model Content-Based Filtering berdasarkan metrics **precision**.

    ![InputCB](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/InputContentBased.png "InputCB")

    ![OutputCB](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/OutputContentBased.png "OutputCB")

    Dimana film **Toy Story** sebagai input merupakan film dengan genre **Adventure**, **Animation**, **Children**, **Comedy**, dan **Fantasy**. Berdasarkan inputan ini, berarti terdapat 1 film yang tidak relevant yang di rekomendasikan oleh model yaitu **Muppet Treasure Island**, yang mana film tersebut mengandung genre Musical.

    Sehingga berdasarkan hasil rekomendasi tersebut, berikut perhitungan **precision** nya:

    _P_ = (# of our recommendation that are relevan) / (# of items we recommended)
    
    _P_ = 4 / 5
    
    _P_ = 0.8
    
    _P_ = 80%

    Berdasarkan Top-5 Recommendation yang diberikan oleh model Content-Based Filtering, didapatkan nilai **precision** sebesar 80%. Sehingga dapat disimpulkan bahwa performa dari model ini cukup baik.

2. **Collaborative Filtering**

    Berdasarkan model Collaborative Filtering yang sudah dibangun, metrics evaluasi yang digunakan adalah **Root Mean Squared Error**(RMSE). Berikut merupakan persamaan dari perhitungan RMSE,

    ![rmse](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/RMSE-Formulas.png "rmse")

    _Dimana_:
    - yi: Nilai sebenarnya
    - ŷi: Nilai prediksi
    - P: Jumlah parameter yang diestimasi, termasuk konstanta.
    - N: Jumlah Data/Sample Spaces

    Hasil nilai RMSE yang rendah menunjukkan bahwa variasi nilai yang dihasilkan dari model sistem rekomendasi mendekati variasi nilai observasinya. Artinya, semakin **kecil** nilai RMSE, maka akan semakin **dekat** nilai yang diprediksi dan diamati.

    Berikut merupakan Data Visualization hasil **training** dan **validation** berdasarkan metrics RMSE dari model Collaborative Filtering pada project ini,

    ![DataViz](https://raw.githubusercontent.com/CarakaMuhamadRahman/RecSys-ML-Model/refs/heads/main/DataViz-RMSE.png "DataViz")

    Dari Data Visualization di atas, dapat disimpulkan bahwa model Collaborative Filtering lebih baik dalam memprediksi data latih dibandingkan data uji berdasarkan metrics RMSE. Dimana pada epochs ke-25, nilai RMSE pada data latih sebesar **0.2064** dan pada data uji sebesar **0.2352**.

Project ini telah berhasil memproses data film, pengguna, dan rating untuk keperluan pembuatan ML Model sistem rekomendasi dengan baik. Ini ditunjukkan dengan berhasilnya model memberikan rekomendasi, baik itu model Content-Based ataupun Collaborative Filtering. Hasil dari rekomendasi ini kemudian diukur menggunakan metrics Precision untuk Content-Based Filtering, dan RMSE untuk Collaborative Filtering.

Berdasarkan hasil metrics, sebetulnya kedua metode ini menunjukkan performa yang terbilang cukup baik dalam memberikan rekomendasi. Memang diperlukan eksperimen lebih lanjut untuk lebih meyakinkan metode mana yang paling optimal dalam kasus rekomendasi film ini sebelum memasuki tahap Deployment. Tetapi berdasarkan project ini, model dengan metode **Content-Based Filtering** dirasa memberikan rekomendasi yang lebih baik dibandingkan dengan Collaborative Filtering, dengan nilai precision sebesar **80%**.

# Laporan Proyek Machine Learning - Book Recommendation System - Andry Syva Maldini
---
### Domain Project
> **Domain Project yang dipilih dalam proyek machine learning ini adalah mengenai literasi dan minat baca dengan judul proyek "Book Recommendation System"**.



* Latar Belakang
  <p align="center">
  <img src="https://github.com/user-attachments/assets/c6f05b56-88c2-4e2c-914a-f409e1d2a216" alt="dataset-cover">
  </p>

  Minat baca masyarakat merupakan faktor penting dalam menciptakan masyarakat yang literate dan berpengetahuan luas. Namun, di Indonesia, minat baca masih tergolong rendah. Berdasarkan riset "World's Most Literate Nations Ranked" pada tahun 2016, Indonesia berada di peringkat ke-60 dari 61 negara dalam hal minat baca [[1]](https://www.kominfo.go.id/content/detail/10862/teknologi-masyarakat-indonesia-malas-baca-tapi-cerewet-di-medsos/0/sorotan_media). Salah satu cara yang dapat diupayakan untuk meningkatkan minat baca adalah dengan memanfaatkan teknologi, salah satunya melalui pengembangan sistem rekomendasi buku. Sistem ini dirancang untuk membantu pengguna menemukan buku yang relevan dengan minat dan preferensi mereka, baik berdasarkan pilihan mereka sebelumnya maupun kesamaan dengan pengguna lain yang memiliki minat serupa. Dengan demikian, sistem rekomendasi buku dapat meningkatkan pengalaman membaca, membantu pengguna menemukan buku-buku baru yang menarik, serta mendorong pertumbuhan minat baca masyarakat.

  Sistem rekomendasi telah lama digunakan dalam berbagai industri online seperti e-commerce, layanan streaming film, dan platform musik, dan terbukti efektif dalam meningkatkan performa sistem serta kepuasan pengguna [[2]](https://www.sciencedirect.com/science/article/abs/pii/S0957417416305309). Pengguna bisa mendapatkan saran yang dipersonalisasi, yang tidak hanya membuat mereka lebih puas dengan layanan yang diberikan, tetapi juga memperluas wawasan mereka tentang pilihan yang tersedia. Dalam konteks perpustakaan, sistem rekomendasi buku juga bisa memberikan kontribusi signifikan. Sistem ini memungkinkan pengunjung perpustakaan untuk menemukan buku yang sesuai dengan minat mereka, terutama ketika buku yang diinginkan tidak tersedia. Dengan begitu, pengguna tidak hanya terbatas pada pencarian manual, tetapi bisa diarahkan ke buku lain yang relevan dengan selera mereka [[3]](https://ejournal.bsi.ac.id/ejurnal/index.php/ijse/article/view/592). Dengan demikian, pengembangan sistem rekomendasi buku ini memiliki potensi yang besar untuk memberikan manfaat bagi pengguna, meningkatkan minat baca, dan memberikan kontribusi positif bagi literasi masyarakat.
___

## Business Understanding
---

### Problem Statements
berdasarkan latar belakang diatas, berikut ini rumusan masalah yang dapat diselesaikan pada project ini:
- Bagaimana cara melakukan pra-pemrosesan pada data book recomendation yang akan digunakan agar dapat membuat model yang baik menggunakan teknik content-base filtering?
- Bagaimana cara memberikan rekomendasi judul buku yang sesuai dengan preferensi pelanggan, berdasarkan rating yang telah mereka berikan pada setiap judul buku yang mereka input?

### Goals
Menjelaskan tujuan dari pernyataan masalah:
- Melakukan pra-pemrosesan dengan baik agar dapat digunakan dalam pembuatan model.
- Membuat pelanggan lebih mudah menemukan judul buku yang tepat dengan bantuan sistem rekomendasi judul buku berdasarkan rating yang diinputkan.

### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini diantaranya :
- Untuk pra-pemrosesan data dapat dilakukan beberapa teknik, diantaranya :
  - Menghapus kolom URL gambar `Image-URL-S`, `Image-URL-M`, `Image-URL-L`
  - Menggabungkan peringkat kerangka data dengan buku berdasarkan nilai `ISBN`
  - Memisahkan string lokasi dengan koma.
  - Menyimpan hanya bagian terakhir (nama negara).
  - Menghapus spasi di depan/di belakang.
- Untuk pembuatan model dipilih penggunaan model Content-Based Filtering (CBF) dan Collaborative Filtering (CF)
  - Cara Kerja
    - Content-Based Filtering (CBF):
      - Menganalisis atribut atau fitur item (genre, penulis, deskripsi, dll.).
      - Membangun profil pengguna berdasarkan preferensi terhadap fitur-fitur tersebut.
      - Merekomendasikan item dengan fitur serupa dengan item yang disukai pengguna.
    - Collaborative Filtering (CF):
      - Membangun matriks pengguna-item berdasarkan interaksi (rating, pembelian).
      - Mengidentifikasi pengguna atau item yang mirip.
        - User-based CF: Memprediksi rating pengguna terhadap item berdasarkan rating pengguna serupa, lalu merekomendasikan item dengan prediksi rating tinggi.
        - Item-based CF: Menghitung kemiripan antar item berdasarkan rating pengguna, lalu merekomendasikan item yang mirip dengan item yang disukai pengguna.
  - Kelebihan dan Kekurangan
    - Kelebihan Content-Based Filtering (CBF):
      - Berfungsi baik untuk pengguna/item baru (cold start).
      - Rekomendasi transparan dan dapat dijelaskan.
      - Menemukan item niche.
    - Kekurangan Content-Based Filtering (CBF):
      - Terbatas pada fitur yang diekstrak.
      - Sulit merekomendasikan item lintas domain.
      - Memerlukan ekstraksi fitur manual.
    - Kelebihan Collaborative Filtering (CF):
      - Menangkap preferensi kompleks dan tersembunyi.
      - Rekomendasi lintas domain.
      - Tidak memerlukan ekstraksi fitur manual.
    - Kekurangan Collaborative Filtering (CF):
      - Kesulitan menangani cold start dan data sparsity.
      - Rekomendasi kurang transparan.

## Data Understanding

![book](https://github.com/user-attachments/assets/75032150-a23f-4073-832d-9bbb45ce3cc6)

Informasi dataset dapat dilihat pada tabel dibawah ini:
Jenis | Keterangan
--- | ---
Sumber | [Kaggle Dataset : Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)
Lisensi | [CC0: Public Domain](https://creativecommons.org/publicdomain/zero/1.0/)
Kategori | Literature, Recommender Systems, Culture and Humanities
Jenis dan Ukuran Berkas | CSV (107.51 MB)

Pada Dataset ini terdapat 3 berkas csv diantaranya yaitu `Books.csv` , `Ratings.csv` , dan `Users.csv`

Pada berkas `Books.csv` memuat data-data buku yang terdiri dari 271.360 baris dan memiliki 8 kolom, diantaranya adalah :  

- `ISBN` : berisi kode ISBN dari buku  
- `Book-Title` : berisi judul buku
- `Book-Author` : berisi penulis buku
- `Year-Of-Publication` : tahun terbit buku  
- `Publisher` : penerbit buku  
- `Image-URL-S` : URL menuju gambar buku berukuran kecil
- `Image-URL-M` : URL menuju gambar buku berukuran sedang
- `Image-URL-L` : URL menuju gambar buku berukuran besar

![book](https://github.com/user-attachments/assets/8154c3e1-b760-472c-bc27-e231ae72b964)

Grafik "10 Penulis Terproduktif" menunjukkan jumlah buku yang telah diterbitkan oleh sepuluh penulis paling produktif sepanjang masa. Agatha Christie menduduki peringkat pertama dengan jumlah buku yang signifikan, diikuti oleh William Shakespeare. Penulis-penulis terkenal lainnya seperti Stephen King, Ann M. Martin, dan Carolyn Keene juga termasuk dalam daftar ini. Grafik ini memberikan gambaran menarik tentang produktivitas luar biasa dari para penulis ini dan kontribusi besar mereka terhadap dunia literatur.

Pada berkas `Ratings.csv` memuat data rating buku yang diberikan oleh pengguna. Data ini memiliki 1.149.780 baris dan memiliki 3 kolom, yaitu :  

 - `User-ID` : berisi ID unik pengguna
 - `ISBN` : berisi kode ISBN buku yang diberi rating oleh pengguna
 - `Book-Rating` : berisi nilai rating yang diberikan oleh pengguna berkisar antara 0-10

![rating](https://github.com/user-attachments/assets/484b1331-0f0b-4b19-963e-64b6707087b7)

Pada data `Rating` ini juga ditemukan bahwa `User-ID` berupa ID angka yang berukuran cukup besar. Lalu `ISBN` merupakan string unik identitas buku gabungan angka dan huruf. Kedua nilai ini nantinya perlu dilakukan encoding agar dapat menghasilkan rekomendasi. Data rating ini juga merupakan data utama dalam membuat sistem rekomendasi dengan Collaborative Filtering pada proyek ini.

Pada berkas `Users.csv` memuat data pengguna. Data ini terdiri dari 278.858 baris dan memiliki 3 kolom, yaitu : 

- `User-ID` : berisi ID unik pengguna
- `Location` : berisi data lokasi pengguna
- `Age` : berisi data usia pengguna 

## Data Preparation
Berikut adalah tahapan-tahapan dalam melakukan pra-pemrosesan data:
- **Data Preparation untuk Model Development dengan Content-Based Filtering**
  - Menangani nilai-nilai yang hilang.
    
    ![image](https://github.com/user-attachments/assets/ebf29290-47e2-4980-b504-d553caaa95d7)

    Terdapat nilai hilang dalam dataframe all_df. Fitur User-ID, ISBN, Book-Rating, dan Location tidak memiliki nilai hilang. Fitur dengan jumlah nilai hilang terbanyak adalah Book-Title, Book-Author, Year-Of-Publication, dan Publisher, masing-masing dengan 118.644 atau 118.646 nilai hilang.

    ![image](https://github.com/user-attachments/assets/004fabe8-5a99-4a8a-b428-f88e725a0236)
    
    Sekarang, kumpulan data terdiri dari 1.031.132 baris. Untuk memastikan tidak ada lagi nilai yang hilang dalam data, jalankan kode berikut.

    ![image](https://github.com/user-attachments/assets/af960a79-ebe7-4164-83ab-a243635ed871)
  
  - Menstandarkan tipe buku berdasarkan ISBN. <br /> Dalam sistem rekomendasi berbasis konten yang akan dikembangkan, setiap `ISBN` mewakili judul buku yang unik. Oleh karena itu, data perlu dipersiapkan terlebih dahulu agar bisa digunakan dalam proses pelatihan model.
 
    ![image](https://github.com/user-attachments/assets/eadfcf64-6d62-48b2-bc9d-975a7206a9f8)
    ![image](https://github.com/user-attachments/assets/3ec06bab-6a2b-43ef-9b62-50a9ba3fdec7)

    Berdasarkan informasi di atas, terdapat ketidakcocokan antara jumlah `ISBN` dan jumlah `Book-Title`, mengindikasikan adanya `ISBN` yang digunakan untuk lebih dari satu judul buku. Masalah ini perlu diatasi dengan mengubah dataset menjadi data unik, siap untuk proses pemodelan. Oleh karena itu, perlu dilakukan proses penghapusan data duplikat pada kolom `ISBN`, dan hasilnya disimpan dalam variabel baru bernama fix_df.

    ![image](https://github.com/user-attachments/assets/b2c448c7-e3f6-4f3a-9895-7d647fdb8ae6)

    Setelah itu, lakukan pengecekan kembali terhadap jumlah data untuk `ISBN`, `Book-Title`, dan nama pengarang buku `Book-Author`. Lakukan proses mengubah rangkaian data tersebut menjadi sebuah list dengan menggunakan fungsi tolist() dari library. Implementasikan kode berikut ini.

    ![image](https://github.com/user-attachments/assets/fa505f2f-ff7e-4fc0-a379-e46cbf94c6e5)

    Berdasarkan hasil tersebut, jumlah data untuk `ISBN`, `Book-Title`, `Book-Author`, `Year-Of-Publication`, `Publisher`, dan `Location` kini sudah sama atau unik. Dataset sekarang hanya memiliki 270.147 baris data setelah proses penghapusan duplikat. Langkah selanjutnya adalah membuat kamus untuk menentukan pasangan kunci-nilai untuk data isbn_id, book_title, book_author, year_of_publication, dan publisher yang telah disiapkan sebelumnya untuk pengembangan model sistem rekomendasi berbasis konten.

    ![image](https://github.com/user-attachments/assets/d128674a-6872-479d-acd9-79f51e829b5c)

    Karena dataset terlalu besar, dan alokasi memori yang digunakan akan sangat besar untuk memproses seluruh data dalam pengembangan model, untuk proyek ini, hanya 10.000 titik data pertama yang akan digunakan (tidak termasuk titik data 10.000).
    
    ![image](https://github.com/user-attachments/assets/40082e77-a940-4bc0-b0c5-65fabf6edbd8)

    Ini adalah data yang akan digunakan dalam proses pengembangan model dengan menggunakan teknik content-based filtering.

  - TF-IDF Vectorizer

    ![image](https://github.com/user-attachments/assets/5b004bfc-f9ca-421a-8351-0db7c7818037)

    Selanjutnya, sesuaikan dan ubah menjadi matriks.

    ![image](https://github.com/user-attachments/assets/2d2711ed-9332-47b8-a22e-14f3fc072b6d)

    Selanjutnya, mari kita lihat matriks tf-idf untuk beberapa judul buku dan nama pengarang dalam bentuk dataframe, di mana kolom diisi dengan nama pengarang buku, dan baris diisi dengan judul buku.

    ![image](https://github.com/user-attachments/assets/7268ab48-3ede-4465-9a6c-f3d0175a7200)

    Matriks TF-IDF berhasil mengidentifikasi fitur penting dari setiap judul buku menggunakan fungsi tfidfvectorizer. Karena dataset yang besar, hanya ditampilkan sampel acak 10 judul buku dan 15 nama penulis.    

- **Data Preparation untuk Model Development dengan Collaborative Filtering**

    Dalam pengembangan model collaborative filtering, data akan dibagi menjadi data pelatihan dan validasi. Sebelum itu, data perlu dipersiapkan agar mudah diproses oleh model. Data rating akan diubah menjadi matriks numerik. Pada tahap ini, beberapa teknik akan diterapkan untuk mempersiapkan data, seperti encoding fitur `User-ID` dan `ISBN` menjadi indeks integer, memetakan `User-ID` dan `ISBN` ke dataframe terkait, dan terakhir memeriksa beberapa aspek data, seperti jumlah pengguna, jumlah buku, dan mengonversi nilai rating ke float untuk digunakan dalam proses pelatihan model.

    ![image](https://github.com/user-attachments/assets/a0bebcfd-a2ae-4edd-8246-6539a0095b25)

    Karena dataset terlalu besar, dan alokasi memori yang digunakan akan sangat besar untuk memproses seluruh data dalam pengembangan model, untuk proyek ini, hanya 10.000 titik data pertama yang akan digunakan (tidak termasuk titik data 10.000).

    Pertama, dilakukan proses encoding fitur `User-ID` dan `ISBN` menjadi indeks integer.
  
    ![image](https://github.com/user-attachments/assets/bc6bbeda-1c99-4c2c-88f2-ab5f4a3aa2f0)
  
    Setelah itu, petakan `User-ID` dan `ISBN` ke dataframe yang terkait.

    ![image](https://github.com/user-attachments/assets/d3b755be-817a-49f4-8dbc-c878b88d8111)
  
    Secara keseluruhan, kode ini berusaha untuk memetakan kolom asli ke representasi baru yang lebih cocok untuk digunakan dalam algoritma sistem rekomendasi, seperti Collaborative Filtering atau Content-Based Filtering, yang memerlukan data dalam bentuk yang lebih efisien.
    
    ![image](https://github.com/user-attachments/assets/6dbc1ab9-8fb1-4ecd-a735-db34dcf522e7)
  
    Tahap persiapan data sudah selesai. Data sekarang siap digunakan dalam proses pembagian menjadi data pelatihan dan validasi dalam proses pengembangan model collaborative filtering.

    ![image](https://github.com/user-attachments/assets/9488a5ff-5dc0-4fde-a6d1-7eecd34d161f)

    Selanjutnya, data akan dibagi menjadi data pelatihan dan validasi dengan komposisi 80:20. Namun, sebelumnya, data pengguna dan judul buku perlu dipetakan menjadi nilai tunggal terlebih dahulu. Kemudian, buat rating pada skala 0 hingga 1 untuk memudahkan proses pelatihan.
  
  ![image](https://github.com/user-attachments/assets/42dff582-0b7e-455f-a990-abb06a25c40d)
  
  Sampai tahap ini, data sudah siap digunakan dalam pengembangan model collaborative filtering.
    
## Modeling
- **Membangun Model dengan Content-Based Filtering**
  - Cosine Similarity:
    - Cara Kerja: Cosine similarity digunakan untuk mengukur kesamaan antara dua vektor berdasarkan sudut kosinus antara mereka. Dalam konteks sistem rekomendasi, setiap item (buku) dan pengguna direpresentasikan sebagai vektor, dan kesamaan antara dua buku atau dua pengguna dihitung berdasarkan sudut antara vektor-vektor ini. Semakin kecil sudutnya (semakin dekat kosinusnya ke 1), semakin besar kemiripan antara keduanya.
    - Parameter yang Digunakan: Cosine similarity tidak memiliki parameter yang perlu dituning seperti model machine learning lainnya. Ini lebih merupakan metode pengukuran jarak, di mana skor kesamaan dihitung sebagai nilai antara -1 (sangat berbeda) hingga 1 (sangat mirip).
    - Hasil: Dengan menggunakan cosine similarity, sistem rekomendasi dapat memberikan rekomendasi buku yang serupa berdasarkan preferensi pengguna yang sudah ada. Hasil dari algoritma ini biasanya menghasilkan daftar buku yang memiliki tingkat kemiripan tinggi dengan buku yang sudah dinilai pengguna.
  
    ![image](https://github.com/user-attachments/assets/7632d15e-d881-4bad-acc0-9335baa20721)
  
    Perhatikan bahwa judul buku 'The End of the Affair' ditulis oleh 'Graham Greene'. Sekarang, gunakan fungsi `recommend_book` untuk mendapatkan rekomendasi berdasarkan judul buku ini.
  
    ![image](https://github.com/user-attachments/assets/83185365-39ac-40ac-8805-19e1f5f13827)
  
    Berdasarkan output di atas, sistem berhasil merekomendasikan 5 judul buku teratas dengan kategori nama penulis buku ('Graham Greene').

- **Membangun Model dengan Collaborative Filtering**
  - RecommenderNet dari Keras:
    - Cara Kerja: RecommenderNet adalah model deep learning yang digunakan untuk sistem rekomendasi. Ini biasanya menggunakan arsitektur embedding, di mana setiap pengguna dan item diwakili sebagai vektor embedding dalam ruang laten. Model ini belajar representasi laten dari pengguna dan item untuk memprediksi interaksi masa depan di antara mereka, seperti rating buku atau rekomendasi buku yang belum dibaca oleh pengguna.
  - Parameter yang Digunakan:
    - Optimizer: Optimizer seperti Adam atau RMSprop digunakan untuk mengupdate bobot model.
    - Loss Function: Mean Squared Error (MSE) atau Binary Crossentropy tergantung pada apakah model memprediksi nilai kontinu (rating) atau probabilitas.
    - Epoch: Jumlah epoch menentukan seberapa banyak model akan dilatih pada data.
    - Embedding Dimensions: Jumlah dimensi embedding menentukan ukuran representasi laten untuk pengguna dan item. Dimensi ini dipilih dengan trade-off antara akurasi dan kompleksitas model.
  - Hasil: RecommenderNet mampu memberikan hasil yang lebih kompleks dibandingkan metode berbasis kesamaan sederhana seperti cosine similarity. Karena model deep learning ini dapat menangkap interaksi non-linear antara pengguna dan item, hasil rekomendasi cenderung lebih akurat dan relevan. Model ini bisa memberikan rekomendasi buku yang belum pernah dibaca oleh pengguna, tetapi kemungkinan besar akan mereka sukai.
  - Proses training
    
    ![image](https://github.com/user-attachments/assets/ca667031-db5d-4fcd-b180-7a34abd025b8)

    Model ini menggunakan Binary Crossentropy untuk menghitung fungsi kerugian, Adam (Adaptive Moment Estimation) sebagai optimizer, dan Root Mean Squared Error (RMSE) sebagai metrik untuk evaluasi.

    ![image](https://github.com/user-attachments/assets/75db876d-e729-4a2c-b36e-f4fb41b5782d)

  - Mendapatkan Rekomendasi Buku

    ![image](https://github.com/user-attachments/assets/0bbe81e3-66a1-451b-96e6-fec4abf4036a)

    Berdasarkan output di atas, rekomendasi berhasil diberikan kepada pengguna. Hasil di atas merupakan rekomendasi untuk pengguna dengan ID 277351. Dari output ini, kita dapat membandingkan 'Buku dengan rating tinggi dari pengguna' dan '10 rekomendasi buku teratas' untuk pengguna tersebut.

    Perhatikan bahwa beberapa judul buku yang direkomendasikan juga menampilkan nama penulis buku yang sesuai dengan rating pengguna. 10 rekomendasi buku teratas beserta nama penulis untuk pengguna tersebut telah diperoleh, dan terdapat satu judul buku yang merupakan buku dengan rating tertinggi dari pengguna. 


## Evaluation

- **Keterkaitan Evaluasi Model dengan Business Understanding**
  - **1. Problem Statements & Goals**
    - **Problem Statement 1: Pra-pemrosesan data untuk content-based filtering** <br />
      Evaluasi model dengan precision, recall, dan F1-score yang tinggi menunjukkan bahwa pra-pemrosesan data yang dilakukan sudah tepat. Model mampu menangkap fitur-fitur penting dari buku (seperti yang direpresentasikan oleh TF-IDF) dan menghasilkan rekomendasi yang relevan. Ini berarti tahapan pembersihan data, penanganan missing values, serta pemilihan fitur sudah efektif.

    - **Problem Statement 2: Rekomendasi buku berdasarkan rating pengguna** <br />
      Evaluasi model collaborative filtering menggunakan RMSE menunjukkan bahwa model cukup akurat dalam memprediksi rating buku yang akan diberikan pengguna. Ini berarti sistem rekomendasi mampu menangkap preferensi pengguna berdasarkan riwayat rating mereka dan memberikan saran buku yang sesuai, sehingga menjawab problem statement ini.
      
  - **Goals:**
    - Pra-pemrosesan data yang baik: Tercapai, dibuktikan dengan performa model content-based filtering yang baik.
    - Memudahkan pengguna menemukan buku: RMSE yang rendah pada model collaborative filtering menunjukkan bahwa sistem mampu memberikan rekomendasi buku yang relevan dengan preferensi pengguna, sehingga tujuan ini tercapai.

  - **2. Solution Statements & Dampaknya**
    - **Content-Based Filtering (CBF)**
      - Evaluasi positif terhadap model CBF mengindikasikan bahwa solusi ini efektif.
      - Penggunaan TF-IDF dan cosine similarity berhasil menangkap fitur penting dari buku dan mengidentifikasi buku-buku yang mirip, sehingga memungkinkan pemberian rekomendasi yang relevan kepada pengguna, terutama untuk buku-buku baru atau yang kurang populer (cold start problem).
      - Hasil evaluasi model CBF menunjukkan precision, recall, dan F1-score yang sangat baik, mendekati 1.0. Ini menunjukkan bahwa model sangat akurat dalam memberikan rekomendasi yang relevan, hampir semua item yang relevan berhasil ditemukan, dan ada keseimbangan yang baik antara presisi dan recall.

        ![image](https://github.com/user-attachments/assets/c2d2aacd-9df8-49ca-ab7c-141385b56604)
        
    - **Collaborative Filtering (CF)**
      - RMSE yang rendah menunjukkan bahwa solusi CF juga berdampak positif.
      - Model mampu memberikan rekomendasi yang personalisasi berdasarkan riwayat rating pengguna, sehingga meningkatkan pengalaman pengguna dan kemungkinan mereka menemukan buku-buku baru yang menarik.
      - Visualisasi metrik evaluasi RMSE menunjukkan bahwa model mencapai konvergensi dengan nilai error akhir yang relatif kecil (0.2415 pada data pelatihan dan 0.2903 pada data validasi). Hal ini menunjukkan bahwa model CF cukup akurat dalam memprediksi preferensi pengguna terhadap buku.

        ![image](https://github.com/user-attachments/assets/35734033-30e5-4163-8586-156efb13d554)

## Kesimpulan

Secara keseluruhan, hasil evaluasi model menunjukkan bahwa solusi yang diimplementasikan, baik Content-Based Filtering (CBF) maupun Collaborative Filtering (CF), terbukti efektif dalam menjawab problem statements dan mencapai tujuan yang telah ditetapkan. Pra-pemrosesan data yang tepat serta pemilihan teknik pemodelan yang sesuai telah menghasilkan sistem rekomendasi yang mampu memberikan saran buku yang relevan dan terpersonalisasi kepada pengguna. Hal ini diharapkan dapat meningkatkan minat baca dan memberikan kontribusi positif bagi literasi masyarakat.

Evaluasi performa model CBF dan CF menunjukkan hasil yang sangat baik, dengan metrik evaluasi yang tinggi dan tingkat error yang rendah. Ini menunjukkan bahwa sistem rekomendasi mampu memberikan rekomendasi buku yang akurat dan relevan, sehingga meningkatkan kepuasan pengguna. Dengan demikian, pengguna lebih terdorong untuk aktif membaca dan mengeksplorasi koleksi buku yang tersedia.

Dampak positif dari sistem rekomendasi ini tidak hanya dirasakan oleh pengguna individu, tetapi juga dapat memberikan keuntungan strategis bagi bisnis. Dengan meningkatkan keterlibatan pengguna dan membantu mereka menemukan buku baru, sistem ini dapat meningkatkan penjualan buku, memperluas basis pelanggan, serta memperkuat posisi bisnis di pasar.
___
## Referensi
---

[[1]](https://www.kominfo.go.id/content/detail/10862/teknologi-masyarakat-indonesia-malas-baca-tapi-cerewet-di-medsos/0/sorotan_media) Devega, E. (2017). _TEKNOLOGI Masyarakat Indonesia: Malas Baca Tapi Cerewet di Medsos_. Kementrian Komunikasi dan Informatika. https://www.kominfo.go.id/content/detail/10862/teknologi-masyarakat-indonesia-malas-baca-tapi-cerewet-di-medsos/0/sorotan_media <br />
[[2]](https://www.sciencedirect.com/science/article/abs/pii/S0957417416305309) Wei, J., He, J., Chen, K., Zhou, Y., & Tang, Z. (2016). _Collaborative filtering and deep learning based recommendation system for cold start items_. Expert Systems with Applications
Volume 69, 1 March 2017, Pages 29-39. https://www.sciencedirect.com/science/article/abs/pii/S0957417416305309 <br />
[[3]](https://ejournal.bsi.ac.id/ejurnal/index.php/ijse/article/view/592) A. Prayitno, _Pemanfaatan Sistem Informasi Perpustakaan Digital Berbasis Website untuk Para Penulis_, Indonesian Journal on Software Engineering, vol. 1, no. 1, pp. 28–37, 2015. https://ejournal.bsi.ac.id/ejurnal/index.php/ijse/article/view/592

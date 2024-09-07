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
Sumber | [Kaggle Dataset : Book Recommendation Dataset]([https://www.kaggle.com/datasets/scarecrow2020/tech-students-profile-prediction/data](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset))
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
- ### Data Preparation untuk Model Development dengan Content-Based Filtering
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

    Karena dataset terlalu besar, dan alokasi memori yang digunakan akan sangat besar untuk memproses seluruh data dalam pengembangan model, untuk proyek ini, hanya 10.000 titik data pertama yang akan digunakan (tidak termasuk titik data 10.000).
    
    ![image](https://github.com/user-attachments/assets/40082e77-a940-4bc0-b0c5-65fabf6edbd8)

    Ini adalah data yang akan digunakan dalam proses pengembangan model dengan menggunakan teknik content-based filtering.

- ### Data Preparation untuk Model Development dengan Collaborative Filtering

    Dalam pengembangan model collaborative filtering, data akan dibagi menjadi data pelatihan dan validasi. Sebelum itu, data perlu dipersiapkan agar mudah diproses oleh model. Data rating akan diubah menjadi matriks numerik. Pada tahap ini, beberapa teknik akan diterapkan untuk mempersiapkan data, seperti encoding fitur `User-ID` dan `ISBN` menjadi indeks integer, memetakan `User-ID` dan `ISBN` ke dataframe terkait, dan terakhir memeriksa beberapa aspek data, seperti jumlah pengguna, jumlah buku, dan mengonversi nilai rating ke float untuk digunakan dalam proses pelatihan model.
  
    Pertama, dilakukan proses encoding fitur `User-ID` dan `ISBN` menjadi indeks integer.
  
    ![image](https://github.com/user-attachments/assets/bc6bbeda-1c99-4c2c-88f2-ab5f4a3aa2f0)
  
    Setelah itu, petakan `User-ID` dan `ISBN` ke dataframe yang terkait.
    
    ![image](https://github.com/user-attachments/assets/6dbc1ab9-8fb1-4ecd-a735-db34dcf522e7)
  
    Tahap persiapan data sudah selesai. Data sekarang siap digunakan dalam proses pembagian menjadi data pelatihan dan validasi dalam proses pengembangan model collaborative filtering.
    
## Modeling
- ### Membangun Model dengan Content-Based Filtering
  Pada tahap ini, akan dikembangkan model menggunakan teknik Content-Based Filtering. Teknik ini merekomendasikan item berdasarkan kesamaan karakteristik antara item yang disukai pengguna sebelumnya dengan item lain. Misalnya, jika pengguna menyukai buku "Pengantar Machine Learning" oleh "Alex Smola", sistem akan mencari buku lain dengan fitur serupa dan merekomendasikannya.
  
  Dalam pengembangan model, pencarian representasi fitur penting dari setiap judul buku dilakukan menggunakan TF-IDF Vectorizer, alat untuk mengubah dokumen teks menjadi representasi vektor berdasarkan nilai TF-IDF setiap kata. Vektor ini kemudian digunakan untuk mencari representasi fitur penting dari setiap judul buku berdasarkan nama penulis buku dalam model yang dikembangkan dengan Content-Based Filtering.
  
  Untuk menghitung tingkat kesamaan antara judul buku, digunakan teknik cosine similarity, yang mengukur kesamaan antara dua vektor dalam ruang berdimensi tinggi. Semakin kecil sudut kosinus, semakin besar kesamaan antara vektor.
  
  Sebelum memulai pengembangan model, dilakukan pemeriksaan ulang dataset, dan dataframe dari tahap sebelumnya disimpan dalam variabel "data".
  
  ![image](https://github.com/user-attachments/assets/c7dcb9fd-df2a-45a6-91f9-45f4bc9ea120)

  - TF-IDF Vectorizer

    ![image](https://github.com/user-attachments/assets/5b004bfc-f9ca-421a-8351-0db7c7818037)

    Selanjutnya, sesuaikan dan ubah menjadi matriks.

    ![image](https://github.com/user-attachments/assets/2d2711ed-9332-47b8-a22e-14f3fc072b6d)

    Selanjutnya, mari kita lihat matriks tf-idf untuk beberapa judul buku dan nama pengarang dalam bentuk dataframe, di mana kolom diisi dengan nama pengarang buku, dan baris diisi dengan judul buku.

    ![image](https://github.com/user-attachments/assets/7268ab48-3ede-4465-9a6c-f3d0175a7200)

    Matriks TF-IDF berhasil mengidentifikasi fitur penting dari setiap judul buku menggunakan fungsi tfidfvectorizer. Karena dataset yang besar, hanya ditampilkan sampel acak 10 judul buku dan 15 nama penulis.

  - Cosine Similarity

    ![image](https://github.com/user-attachments/assets/26c89532-a314-4f74-a7cc-a9007c67a11d)

    Pada tahap ini, dilakukan proses perhitungan kesamaan kosinus untuk dataframe `tfidf_matrix` yang didapatkan dari tahap sebelumnya. Dengan menggunakan fungsi `cosine_similarity` dari library sklearn, diperoleh nilai-nilai kemiripan antar judul buku. Kode di atas menghasilkan output berupa matriks kemiripan dalam format array.

    Selanjutnya, mari kita lihat matriks kemiripan dari masing-masing judul buku dengan menampilkan nama-nama judul buku pada 5 sampel kolom (`axis = 1`) dan 10 sampel baris (`axis = 0`).

    ![image](https://github.com/user-attachments/assets/44684213-862e-4e5c-abc3-e736e0c88b0b)

    Dengan cosine similarity, telah berhasil mengidentifikasi kemiripan antara satu judul buku dengan judul buku lainnya. Bentuk (10000, 10000) merepresentasikan ukuran matriks kemiripan dari data. Berdasarkan data yang tersedia, matriks di atas sebenarnya berukuran 10.000 judul buku x 10.000 judul buku (masing-masing di sepanjang sumbu X dan Y). Ini berarti bahwa sistem telah berhasil mengidentifikasi tingkat kemiripan untuk 10.000 judul buku. Namun, tidak mungkin untuk menampilkan semua data di sini. Oleh karena itu, hanya 10 judul buku pada sumbu vertikal dan 5 judul buku pada sumbu horizontal yang dipilih. Dengan data kemiripan yang telah didapatkan tadi, sistem akan merekomendasikan daftar judul buku yang mirip dengan judul buku yang pernah dibeli atau dibaca oleh pengguna.

  - Mendapatkan Recomendasi

    ![image](https://github.com/user-attachments/assets/6b77cafb-e6da-4aa1-a31d-7509420bae95)

    Perhatikan bahwa dengan menggunakan argpartition, proses pengambilan nilai k teratas dari data kemiripan (dalam kasus ini: dataframe cosine_sim_df) dilakukan. Selanjutnya, ambil data dari bobot tertinggi hingga terendah (tingkat kemiripan). Data ini kemudian disimpan dalam variabel yang paling dekat. Selanjutnya, perlu dilakukan penghapusan terhadap book_title yang dicari agar tidak muncul dalam daftar rekomendasi. Dalam hal ini, judul_buku perlu dihapus agar tidak muncul dalam daftar rekomendasi yang disediakan.

    Gunakan fungsi recommend_book untuk menghasilkan 5 rekomendasi buku teratas yang direkomendasikan oleh sistem.
  
    ![image](https://github.com/user-attachments/assets/7632d15e-d881-4bad-acc0-9335baa20721)
  
    Perhatikan bahwa judul buku 'The End of the Affair' ditulis oleh 'Graham Greene'. Sekarang, gunakan fungsi `recommend_book` untuk mendapatkan rekomendasi berdasarkan judul buku ini.
  
    ![image](https://github.com/user-attachments/assets/83185365-39ac-40ac-8805-19e1f5f13827)
  
    Berdasarkan output di atas, sistem berhasil merekomendasikan 5 judul buku teratas dengan kategori nama penulis buku ('Graham Greene').

- ### Membangun Model dengan Collaborative Filtering

  Dalam pengembangan model ini, kita akan menggunakan teknik collaborative filtering untuk membuat sistem rekomendasi. Teknik ini butuh data rating dari pengguna atau pembaca. Ide dasarnya adalah pengguna dengan preferensi yang mirip di masa lalu cenderung punya preferensi yang mirip juga untuk item di masa depan. Di proyek ini, kita akan bikin model collaborative filtering berbasis kesamaan pengguna (User-Based Collaborative Filtering).
  
  Hasil dari pengembangan model ini adalah rekomendasi sejumlah judul buku yang sesuai dengan preferensi pengguna berdasarkan rating yang sudah mereka berikan sebelumnya. Dari data rating pengguna, kita akan identifikasi dan rekomendasikan judul buku serupa yang belum pernah dibaca atau dibeli oleh pengguna.
  
  Setelah data siap dari tahap persiapan sebelumnya, langkah berikutnya adalah membagi data menjadi data pelatihan dan validasi, lalu melatih model. Dalam proses pelatihan, model menghitung skor kecocokan antara pengguna dan judul buku menggunakan teknik embedding. Pertama, proses embedding dilakukan pada data pengguna dan judul buku. Selanjutnya, dilakukan operasi perkalian dot product antara embedding pengguna dan buku. Selain itu, bias ditambahkan untuk setiap pengguna dan judul buku. Skor kecocokan diatur pada skala [0,1] dengan fungsi aktivasi sigmoid. Model dibuat dengan kelas RecommenderNet menggunakan kelas Keras Model. Kode untuk kelas RecommenderNet ini terinspirasi dari tutorial di website Keras dengan beberapa adaptasi agar sesuai dengan kasus ini. Model akan menggunakan Binary Crossentropy untuk menghitung fungsi loss, Adam (Adaptive Moment Estimation) sebagai optimizer, dan Root Mean Squared Error (RMSE) sebagai metrik evaluasi.
  
  ![image](https://github.com/user-attachments/assets/9488a5ff-5dc0-4fde-a6d1-7eecd34d161f)
  
  Selanjutnya, data akan dibagi menjadi data pelatihan dan validasi dengan komposisi 80:20. Namun, sebelumnya, data pengguna dan judul buku perlu dipetakan menjadi nilai tunggal terlebih dahulu. Kemudian, buat rating pada skala 0 hingga 1 untuk memudahkan proses pelatihan.
  
  ![image](https://github.com/user-attachments/assets/42dff582-0b7e-455f-a990-abb06a25c40d)
  
  Sampai tahap ini, data sudah siap digunakan dalam pengembangan model collaborative filtering.

  - Proses training
    
    ![image](https://github.com/user-attachments/assets/ca667031-db5d-4fcd-b180-7a34abd025b8)

    Model ini menggunakan Binary Crossentropy untuk menghitung fungsi kerugian, Adam (Adaptive Moment Estimation) sebagai optimizer, dan Root Mean Squared Error (RMSE) sebagai metrik untuk evaluasi.

    ![image](https://github.com/user-attachments/assets/75db876d-e729-4a2c-b36e-f4fb41b5782d)

  - Mendapatkan Rekomendasi Buku

    ![image](https://github.com/user-attachments/assets/0bbe81e3-66a1-451b-96e6-fec4abf4036a)

    Berdasarkan output di atas, rekomendasi berhasil diberikan kepada pengguna. Hasil di atas merupakan rekomendasi untuk pengguna dengan ID 277351. Dari output ini, kita dapat membandingkan 'Buku dengan rating tinggi dari pengguna' dan '10 rekomendasi buku teratas' untuk pengguna tersebut.

    Perhatikan bahwa beberapa judul buku yang direkomendasikan juga menampilkan nama penulis buku yang sesuai dengan rating pengguna. 10 rekomendasi buku teratas beserta nama penulis untuk pengguna tersebut telah diperoleh, dan terdapat satu judul buku yang merupakan buku dengan rating tertinggi dari pengguna. 


## Evaluation
- ### Model Evaluation Content-Based Filtering
  Metrik yang kita pakai untuk nilai model rekomendasi ini adalah Precision, Recall, dan F1-Score. Metrik-metrik ini sudah biasa dipakai buat ngukur seberapa bagus model kita. Precision itu kayak, dari semua rekomendasi yang dikasih model, berapa banyak yang beneran relevan. Recall itu kayak, dari semua rekomendasi yang harusnya dikasih, berapa banyak yang berhasil ditemukan model. Nah, F1 Score itu gabungan keduanya, jadi satu nilai yang nunjukin seimbang nggak antara Precision sama Recall.
  
  Sebelum ngitung metrik-metrik itu, kita butuh data yang punya label asli, buat bandingin sama hasil prediksi model; ini namanya data ground truth. Di proyek ini, data ground truth dibikin dari hasil cosine similarity, tiap baris dan kolom itu judul buku, dan nilainya nunjukin mirip atau nggak. Nilai 1 berarti mirip, 0 berarti nggak mirip. Kita juga perlu nentuin batas, jadi bisa mutusin nilai kemiripan antara dua buku itu masuk kategori 1 (mirip) atau 0 (nggak mirip).
  
  ![image](https://github.com/user-attachments/assets/16d24761-1842-4b95-a239-0328168a0680)
  
  Setelah matriks ground truth dibuat, yang isinya label asli dari hasil cosine similarity, kita lanjut ke proses evaluasi model dengan metrik precision, recall, dan f1 score. Pertama, kita perlu mengimpor fungsi `precision_recall_fscore_support` dari library Sklearn. Karena keterbatasan memori, kita cuma ambil sekitar 5.000 sampel dari matriks cosine similarity dan ground truth. Ini buat mempercepat proses perhitungan, apalagi matriksnya lumayan gede. Kedua matriks ini lalu diubah jadi array satu dimensi biar gampang dibandingkan dan dihitung metriknya.
  
  Kita juga pakai threshold buat mengelompokkan nilai cosine similarity jadi 1 atau 0. Kalau nilainya di atas atau sama dengan threshold, berarti 1 (positif), kalau di bawah berarti 0 (negatif). Hasilnya disimpan di array `predictions`. Terakhir, kita pakai fungsi `precision_recall_fscore_support` buat ngitung precision, recall, dan f1 score. Parameter `average='binary'` dipakai karena kita ngukur performa dalam konteks klasifikasi biner (1 atau 0). Parameter `zero_division=1` dipakai buat menghindari pembagian dengan nol kalau ada kelas yang nggak ada di prediksi. 
  
  ![image](https://github.com/user-attachments/assets/c2d2aacd-9df8-49ca-ab7c-141385b56604)
  
  Dari hasil evaluasi, kita lihat bahwa nilai precision, recall, dan F1 Score semuanya sangat baik. Precision 1.0 berarti semua prediksi positif model kita tepat, gak ada yang salah. Recall 1.0 nunjukin model berhasil nemuin hampir semua item yang relevan. F1 Score juga mendekati 1.0, artinya ada keseimbangan bagus antara precision dan recall, dan model kita cenderung kasih hasil yang sangat bagus untuk kedua kelas (positif dan negatif). Kesimpulannya, berdasarkan hasil evaluasi ini, model kita bekerja dengan sangat baik dalam merekomendasikan item pakai content-based filtering.

- ### Model Evaluation Collaborative Filtering
  Selama proses pelatihan model, sebagaimana dijelaskan dalam bagian pemodelan, metrik utama yang digunakan untuk mengevaluasi kinerja model Collaborative Filtering adalah Root Mean Squared Error (RMSE). RMSE berfungsi sebagai metrik evaluasi yang banyak digunakan untuk menilai keakuratan prediksi nilai kontinu dengan membandingkan nilai prediksi dengan nilai aktual. Dalam konteks collaborative filtering, RMSE secara khusus mengukur keefektifan model dalam memprediksi preferensi pengguna untuk berbagai item.
  
  Proses pelatihan model menghasilkan hasil pelatihan yang mencakup informasi RMSE untuk dataset pelatihan dan validasi. Untuk merepresentasikan perkembangan pembelajaran model secara visual, kami menggunakan matplotlib untuk membuat plot metrik evaluasi dari waktu ke waktu. Cuplikan kode berikut menunjukkan proses visualisasi ini. 
  
  ![image](https://github.com/user-attachments/assets/35734033-30e5-4163-8586-156efb13d554)
  
  Berdasarkan visualisasi metrik evaluasi RMSE pada model yang dikembangkan, terlihat bahwa model mencapai konvergensi sekitar epoch ke-50. Plot metrik model menunjukkan nilai MSE yang relatif kecil. Dari proses ini, diperoleh nilai error akhir sebesar 0.2415, dan error pada data validasi sebesar 0.2903. Angka-angka ini menunjukkan hasil yang cukup baik untuk sistem rekomendasi yang dihasilkan. Semakin kecil nilai RMSE, semakin baik model dalam memprediksi preferensi pengguna terhadap item. Hal inilah yang membuat hasil rekomendasi dari model cukup akurat. 

___
## Referensi
---

[[1]](https://www.kominfo.go.id/content/detail/10862/teknologi-masyarakat-indonesia-malas-baca-tapi-cerewet-di-medsos/0/sorotan_media) Devega, E. (2017). _TEKNOLOGI Masyarakat Indonesia: Malas Baca Tapi Cerewet di Medsos_. Kementrian Komunikasi dan Informatika. https://www.kominfo.go.id/content/detail/10862/teknologi-masyarakat-indonesia-malas-baca-tapi-cerewet-di-medsos/0/sorotan_media <br />
[[2]](https://www.sciencedirect.com/science/article/abs/pii/S0957417416305309) Wei, J., He, J., Chen, K., Zhou, Y., & Tang, Z. (2016). _Collaborative filtering and deep learning based recommendation system for cold start items_. Expert Systems with Applications
Volume 69, 1 March 2017, Pages 29-39. https://www.sciencedirect.com/science/article/abs/pii/S0957417416305309 <br />
[[3]](https://ejournal.bsi.ac.id/ejurnal/index.php/ijse/article/view/592) A. Prayitno, _Pemanfaatan Sistem Informasi Perpustakaan Digital Berbasis Website untuk Para Penulis_, Indonesian Journal on Software Engineering, vol. 1, no. 1, pp. 28–37, 2015. https://ejournal.bsi.ac.id/ejurnal/index.php/ijse/article/view/592

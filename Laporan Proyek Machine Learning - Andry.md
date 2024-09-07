# Laporan Proyek Machine Learning - Andry Syva Maldini

## Domain Project
> **Domain project yang dipilih dalam proyek machine learning ini adalah mengenai pendidikan dengan judul proyek "Prediksi Kelulusan Sertifikasi Profesi Berdasarkan Riwayat Belajar Peserta"**.

- Latar Belakang
  <p align="center">
  <img src="https://github.com/user-attachments/assets/5c9b35cd-945b-4696-98f6-a22a743c4ce6" alt="dataset-cover" width="500">
  </p>

  Dalam era globalisasi dan persaingan dunia kerja yang semakin ketat, sertifikasi profesi telah menjadi salah satu tolok ukur penting dalam menilai kompetensi individu di berbagai bidang [1](https://proceeding.unnes.ac.id/snpasca/article/view/281). Sertifikasi ini tidak hanya membantu individu dalam meningkatkan kredibilitas dan daya saing mereka, tetapi juga memberikan jaminan kepada pemberi kerja mengenai kemampuan dan pengetahuan yang dimiliki oleh calon pekerja [2](https://jimfeb.ub.ac.id/index.php/jimfeb/article/view/6853). Dengan demikian, sertifikasi profesional berfungsi sebagai bukti formal atas keterampilan dan pengetahuan, yang dapat meningkatkan peluang kerja serta pengembangan karir seseorang di masa depan. Namun, proses sertifikasi bukanlah hal yang sederhana. Penilaian kompetensi peserta oleh asesor merupakan tahap krusial dalam memastikan bahwa individu yang disertifikasi benar-benar memiliki kemampuan yang diperlukan. Penilaian ini sering kali melibatkan evaluasi berbagai aspek kompetensi, seperti pengetahuan teoritis, keterampilan praktis, dan pengalaman kerja . Dalam konteks ini, tantangan yang dihadapi asesor semakin kompleks, terutama ketika jumlah peserta meningkat dan kriteria penilaian menjadi lebih rumit [3](https://stiemmamuju.e-journal.id/FJIIM/article/download/115/70). Kondisi ini dapat meningkatkan risiko ketidak konsistenan dan subjektivitas dalam penilaian, yang dapat mempengaruhi keadilan dan akurasi hasil sertifikasi.

___
## Business Understanding
---

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:

- Bagaimana penerapan algoritma Neural Network dapat menghasilkan prediksi penilaian yang lebih akurat dan konsisten pada proses sertifikasi?
- Bagaimana cara mengurangi subjektivitas dalam penilaian asesor dengan memanfaatkan riwayat belajar peserta?
- Bagaimana sistem prediksi berbasis Neural Network dapat diintegrasikan ke dalam proses sertifikasi profesi untuk meningkatkan efisiensi dan efektivitas penilaian?

### Goals

Menjelaskan tujuan dari pernyataan masalah:

- Menerapkan algoritma Neural Network untuk menghasilkan prediksi penilaian yang lebih akurat dan konsisten.
- Mengurangi subjektivitas dalam penilaian asesor dengan memanfaatkan riwayat belajar peserta.
- Mengintegrasikan sistem prediksi berbasis Neural Network ke dalam proses sertifikasi profesi untuk meningkatkan efisiensi dan efektivitas penilaian.

#### Solution Statements

Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini diantaranya:

- Untuk pra-pemrosesan data dapat dilakukan beberapa teknik, diantaranya :

  - Melakukan _drop_ kolom pada kolom `Unnamed: 0`, `NAME`, `USER_ID`.
  - Mengatasi masalah data yang kosong dengan median.
  - Melakukan pembagian dataset menjadi dua bagian dengan rasio 70% untuk data latih dan 30% untuk data uji.
  - Melakukan _Standard Scaler_.

- Untuk pembuatan model dipilih penggunaan model dengan algoritma Random Forest dan K-Nearest Neighbor. Algoritma tersebut dipilih karena mudah digunakan dan juga cocok untuk kasus ini. Berikut cara kerja, kelebihan dan kekurangan algoritma Random Forest dan K-Nearest Neighbor:
  - Cara kerja Algoritma Neural Network [[4]](http://dx.doi.org/10.30865/mib.v4i2.2035):
    - Gunakan dataset untuk membangun model NN
    - Proses feedforward dan backpropagation diulang berkali-kali pada dataset pelatihan, sampai jaringan mencapai kinerja yang memuaskan.
  - Kelebihan dan kekurangan Algoritma Neural Network [[5]](http://publication.petra.ac.id/index.php/teknik-informatika/article/view/10496):
    - Neural network mampu belajar dari data dan pengalaman, meningkatkan kinerjanya seiring waktu tanpa perlu pemrograman eksplisit.
    - Proses pengambilan keputusan dalam neural network seringkali sulit dipahami, membuat sulit untuk menjelaskan bagaimana suatu kesimpulan dicapai.
  - Cara kerja Algoritma K-Nearest Neighbor [[6]](https://publikasi.dinus.ac.id/index.php/jais/article/view/1189/):
    - Menentukan jumlah tetangga terdekat K
    - Menghitung jarak dokumen _testing_ ke dokumen _training_
    - Urutkan data berdasarkan data yang mempunyai jarak Euclidean terkecil
    - Tentukan kelompok testing berdasarkan label pada K.
  - Kelebihan dan kekurangan Algoritma K-Nearest Neighbor [[7]](https://simdos.unud.ac.id/uploads/file_penelitian_1_dir/721bdb509a6f0bb9ccca6d7374b86759.pdf):
    - KNN memiliki beberapa kelebihan yaitu bahwa algoritmanya tangguh terhadap _training_ data yang _noisy_ dan efektif apabila data latihnya besar.
    - Kekurangan pada algoritma KKN yaitu perlu menentukan nilai dari parameter K (jumlah dari tetangga terdekat), Pembelajaran berdasarkan jarak tidak jelas mengenai jenis jarak apa yang harus digunakan dan atribut mana yang harus digunakan untuk mendapatkan hasil yang terbaik dan Biaya komputasi cukup tinggi karena diperlukan perhitungan dari jarak tiap sample uji pada keseluruhan sample latih.

## Data Understanding

![Image of Dataset](https://i.postimg.cc/3rjpjzfk/capture.jpg)
Informasi dataset dapat dilihat pada tabel dibawah ini:
Jenis | Keterangan
--- | ---
Sumber | [Kaggle Dataset : Tech-Student Profile Prediction](https://www.kaggle.com/datasets/scarecrow2020/tech-students-profile-prediction/data)
Lisensi | Data files © Original Authors
Kategori | Education, Multiclass Classification, Clustering
Jenis dan Ukuran Berkas | CSV (2.08 MB)

DataFrame ini memiliki 20.000 baris data dan 16 kolom. Terdapat beberapa tipe data yang digunakan, yaitu:

- float64: Sebagian besar kolom berisi data numerik dalam tipe float64, kemungkinan besar merepresentasikan nilai-nilai kontinu seperti jam belajar atau skor rata-rata.
- int64: Dua kolom bertipe int64, mungkin digunakan untuk ID pengguna atau nilai numerik lainnya yang tidak memerlukan presisi desimal.
- object: Dua kolom bertipe object, biasanya digunakan untuk menyimpan data teks atau campuran tipe data. Dalam kasus ini, kolom 'NAME' dan 'PROFILE' kemungkinan termasuk dalam kategori ini.

Beberapa kolom memiliki nilai null (missing values), yang perlu ditangani sebelum dilakukan analisis atau pemodelan lebih lanjut.

---

Pada berkas yang diuduh yakni dataset-tortuga.csv berisi 20000 baris dan 16 kolom. untuk penjelasan mengenai variabel-variabel pada dataset ini dapat dilihat sebagai berikut:

- Unnamed: 0: Ini biasanya adalah kolom indeks yang dihasilkan secara otomatis ketika data dibaca dari file (misalnya, CSV). Kolom ini mungkin tidak memiliki arti spesifik dan bisa diabaikan atau dihapus jika tidak diperlukan.
- NAME: Nama pengguna. Ini bisa berupa nama lengkap atau nama panggilan pengguna yang mengikuti kursus.
- USER_ID: ID unik pengguna. Ini adalah pengenal unik untuk setiap pengguna dalam dataset.
- HOURS_DATASCIENCE: Jumlah jam yang dihabiskan oleh pengguna untuk belajar atau mengikuti kursus terkait data science.
- HOURS_BACKEND: Jumlah jam yang dihabiskan oleh pengguna untuk belajar atau mengikuti kursus terkait pengembangan backend.
- HOURS_FRONTEND: Jumlah jam yang dihabiskan oleh pengguna untuk belajar atau mengikuti kursus terkait pengembangan frontend.
- NUM_COURSES_BEGINNER_DATASCIENCE: Jumlah kursus tingkat pemula yang diikuti pengguna dalam bidang data science.
- NUM_COURSES_BEGINNER_BACKEND: Jumlah kursus tingkat pemula yang diikuti pengguna dalam bidang pengembangan backend.
- NUM_COURSES_BEGINNER_FRONTEND: Jumlah kursus tingkat pemula yang diikuti pengguna dalam bidang pengembangan frontend.
- NUM_COURSES_ADVANCED_DATASCIENCE: Jumlah kursus tingkat lanjutan yang diikuti pengguna dalam bidang data science.
- NUM_COURSES_ADVANCED_BACKEND: Jumlah kursus tingkat lanjutan yang diikuti pengguna dalam bidang pengembangan backend.
- NUM_COURSES_ADVANCED_FRONTEND: Jumlah kursus tingkat lanjutan yang diikuti pengguna dalam bidang pengembangan frontend.
- AVG_SCORE_DATASCIENCE: Skor rata-rata yang diperoleh pengguna dalam kursus terkait data science.
- AVG_SCORE_BACKEND: Skor rata-rata yang diperoleh pengguna dalam kursus terkait pengembangan backend.
- AVG_SCORE_FRONTEND: Skor rata-rata yang diperoleh pengguna dalam kursus terkait pengembangan frontend.
- PROFILE: Profil pengguna. Ini bisa merujuk pada deskripsi singkat, statuskeahlian, atau kategori pengguna berdasarkan profil pembelajaran mereka.

- Men-drop kolom `Unnamed: 0`, `NAME`, `USER_ID`
- Menampilkan kolom unik <br />
  ![unik](https://github.com/user-attachments/assets/c5487af6-1958-4090-a951-1c36f5367af9)
- Menghapus kolom `PROFILE` sehingga menyisakan kolom untuk analisis lebih lanjut <br />
  ![profile](https://github.com/user-attachments/assets/43d8b1f4-44cf-4ebc-b6fa-c812c09e3416)
- Men-check missing value pada setiap kolom <br />
  ![missing value](https://github.com/user-attachments/assets/be585bd4-04b9-4309-96c5-84ef07565294)

## Data Preparation

Berikut adalah tahapan-tahapan dalam melakukan pra-pemrosesan data:

- Menangani Nilai yang Hilang: Nilai yang hilang pada dataset diatasi dengan menggunakan median dari setiap kolom. Hal ini dilakukan untuk memastikan bahwa tidak ada data yang hilang yang dapat mengganggu proses pelatihan model. <br />
  ![Image isi kolom](https://i.postimg.cc/FRKC8Rh1/median.jpg)
- Membagi Dataset: Dataset dibagi menjadi dua bagian:

    * Data latih (70%): Digunakan untuk melatih model machine learning.
    * Data uji (30%): Digunakan untuk mengevaluasi performa model yang telah dilatih. Pembagian ini penting untuk mencegah overfitting dan mendapatkan estimasi performa model yang lebih baik pada data yang belum pernah dilihat sebelumnya.
  
  ![Image of Dataset](https://i.postimg.cc/nr14w9gr/splidata.jpg)
- Standardisasi Fitur: Fitur-fitur pada data latih dan data uji distandardisasi sehingga memiliki rata-rata 0 dan standar deviasi 1. Proses ini penting untuk banyak algoritma machine learning, termasuk K-Nearest Neighbors dan Neural Network, karena dapat membantu model belajar lebih efisien dan menghasilkan performa yang lebih baik.. <br />
  ![Image of Dataset](https://i.postimg.cc/d3t8TtNy/standart.jpg)
- Pemisahan Fitur dan Target: Data dipisahkan menjadi fitur (X) dan target (y) baik untuk data latih maupun data uji. Fitur-fitur ini akan digunakan sebagai input untuk model, sedangkan target akan digunakan sebagai nilai yang akan diprediksi oleh model. <br />
  ![Image of Dataset](https://i.postimg.cc/tTZ0GWHr/data-x-y.jpg)

## Modeling

Setelah dilakukan pra-pemrosesan pada dataset, langkah selanjutnya adalah modeling terhadap data. Pada tahap ini menggunakan 2 algoritma yaitu K-Nearest Neighbor (KNN) dan Neural Network (NN) dengan tanpa parameter tambahan. Pertama-tama kedua model ini dilatih menggunakan data latih. Setelah itu kedua model akan diuji dengan data uji. Terakhir kedua model akan diukur nilai akurasinya. Perbandingan hasil dari kedua model akan dianalisis untuk menentukan algoritma terbaik.

Perbandingan Hasil dari kedua model sebagai berikut:<br />
![Image perfomance model](https://i.postimg.cc/HLs5H8R0/model.jpg)

- _Confussion Matrix_ algoritma K-Nearest Neighbor:<br />
  ![Image of Dataset](https://i.postimg.cc/bv9bWRBy/output-knn.png)
- _Confussion Matrix_ algoritma Neural Network:<br />
  ![Image of Dataset](https://i.postimg.cc/V6HSPZB8/output-nn.png)

### Cara Kerja Algoritma KNN:
![knn](https://github.com/user-attachments/assets/7c9b3ffe-3f88-4668-ba9b-b1f711295ea1)


KNN adalah algoritma klasifikasi yang bekerja berdasarkan prinsip "majority vote" atau suara terbanyak dari tetangga terdekat. Ketika ada data baru yang perlu diklasifikasikan, algoritma ini akan:

Mengukur Jarak: Menghitung jarak antara data baru tersebut dengan semua data yang sudah ada di dataset pelatihan. Jarak ini bisa diukur dengan berbagai metode, seperti Euclidean distance, Manhattan distance, atau lainnya.
Menemukan Tetangga Terdekat: Mengidentifikasi sejumlah 'K' data dari dataset pelatihan yang memiliki jarak terdekat dengan data baru tersebut. 'K' ini adalah parameter yang perlu ditentukan sebelumnya.
Melakukan Voting: Melihat label kelas dari 'K' tetangga terdekat tersebut. Label kelas yang paling banyak muncul di antara tetangga-tetangga ini akan menjadi label kelas yang diberikan kepada data baru tersebut.
Parameter yang Digunakan:

Pada laporan klasifikasi yang ditampilkan, terlihat bahwa model KNN menggunakan parameter n_neighbors=5. Artinya, algoritma ini akan mempertimbangkan 5 tetangga terdekat untuk melakukan voting dan menentukan kelas dari data baru.

* Kelebihan KNN:
  * Sederhana dan mudah dipahami.
  * Tidak memerlukan asumsi tentang distribusi data (non-parametric).
  * Dapat digunakan untuk klasifikasi maupun regresi.

* Kekurangan KNN:
  * Bisa menjadi lambat jika dataset pelatihan sangat besar karena harus menghitung jarak dengan semua data.
  * Sensitif terhadap fitur yang tidak relevan atau memiliki skala yang berbeda-beda.
  * Memerlukan pemilihan nilai 'K' yang tepat, yang bisa mempengaruhi performa model.

### Cara Kerja Algoritma MLP:
![mlp](https://github.com/user-attachments/assets/a75d52b8-3d91-45cf-9665-afcfba2b24ed)

* MLP terdiri dari beberapa lapisan neuron yang saling terhubung:

  * Lapisan Input: Menerima data masukan (fitur-fitur yang digunakan untuk klasifikasi).
  * Lapisan Tersembunyi: Terdiri dari satu atau lebih lapisan neuron yang melakukan transformasi non-linear pada data masukan. Setiap neuron di lapisan ini menerima input dari lapisan sebelumnya, melakukan pemrosesan dengan fungsi aktivasi, dan meneruskan output ke lapisan berikutnya.
  * Lapisan Output: Menghasilkan prediksi kelas. Jumlah neuron di lapisan ini biasanya sama dengan jumlah kelas yang mungkin.
Proses pembelajaran MLP melibatkan penyesuaian bobot koneksi antar neuron untuk meminimalkan kesalahan prediksi pada data pelatihan. Ini dilakukan dengan algoritma optimasi seperti backpropagation dan gradient descent.

* Parameter yang Digunakan:
  * `hidden_layer_sizes=(128, 64, 32)`: Menentukan arsitektur jaringan dengan 3 lapisan tersembunyi yang memiliki masing masing 128, 64, dan 32 neuron.
  * `solver='adam'`: Menggunakan algoritma optimasi Adam untuk melatih model.
  * `max_iter=500`: Menetapkan jumlah maksimum iterasi (epoch) selama pelatihan.

* Interpretasi Laporan Klasifikasi:
  * Akurasi keseluruhan 0.9535: Model MLP ini juga menunjukkan performa yang sangat baik, mampu memprediksi kelas dengan benar untuk sekitar 95.35% data uji.
  * Precision, recall, dan F1-score tinggi untuk sebagian besar kelas: Menunjukkan kemampuan model yang baik dalam mengidentifikasi kelas-kelas tersebut.
  * Perbedaan performa antar kelas: Beberapa kelas mungkin sedikit lebih sulit diprediksi daripada yang lain, tetapi secara umum model ini sangat efektif.

* Perbandingan dengan KNN:
  * MLP cenderung lebih kompleks daripada KNN: MLP memiliki lebih banyak parameter yang perlu diatur dan proses pelatihan yang lebih rumit.
  * MLP dapat mempelajari hubungan non-linear yang kompleks dalam data: Ini bisa menjadi keuntungan jika data memiliki pola yang tidak dapat dideteksi oleh KNN yang lebih sederhana.
  * KNN lebih mudah diinterpretasikan: Keputusan KNN didasarkan pada kemiripan dengan tetangga terdekat, sedangkan keputusan MLP lebih sulit dipahami karena melibatkan banyak lapisan dan bobot.

## Evaluation

* Metrik Evaluasi <br />
Dalam laporan ini, beberapa metrik evaluasi digunakan untuk mengukur performa model K-Nearest Neighbors (KNN) dan Multi-Layer Perceptron (MLP):

  * Akurasi: Mengukur proporsi prediksi yang benar dari keseluruhan prediksi.
  * Presisi: Mengukur proporsi prediksi positif yang benar dari keseluruhan prediksi positif.
  * Recall: Mengukur proporsi prediksi positif yang benar dari keseluruhan sampel yang sebenarnya positif.
  * F1-score: Merupakan rata-rata harmonik antara presisi dan recall, memberikan keseimbangan antara keduanya.

* Evaluasi Metrik <br />
Berdasarkan laporan klasifikasi, model Multi-Layer Perceptron (MLP) menunjukkan performa yang sedikit lebih baik daripada model K-Nearest Neighbors (KNN) dalam hal akurasi keseluruhan:

  * Akurasi MLP: 0.9535
  * Akurasi KNN: 0.9340

  Selain itu, MLP juga menunjukkan nilai presisi, recall, dan F1-score yang lebih tinggi atau setara untuk hampir semua kelas dibandingkan dengan KNN. Ini menunjukkan bahwa MLP lebih baik dalam mengidentifikasi kelas-kelas tersebut dengan benar dan mengurangi kesalahan klasifikasi.

* Evaluasi terhadap Business Understanding<br />
  * Prediksi penilaian yang lebih akurat dan konsisten:
Kedua model (KNN dan MLP), dengan akurasi di atas 90%, menunjukkan kemampuan yang baik dalam menghasilkan prediksi penilaian yang akurat. Hal ini menunjukkan potensi mereka untuk menghasilkan prediksi yang lebih baik dan lebih konsisten dibandingkan metode penilaian tradisional yang mungkin rentan terhadap subjektivitas dan ketidakkonsistenan antar asesor.
  * Mengurangi subjektivitas dalam penilaian:
Meskipun model-model ini tidak secara langsung menghilangkan subjektivitas asesor, mereka memberikan informasi tambahan yang objektif berdasarkan riwayat belajar peserta. Informasi ini dapat membantu asesor membuat keputusan yang lebih informatif dan mengurangi bias yang mungkin terjadi dalam penilaian manual. Dengan demikian, model-model ini dapat berkontribusi pada pengurangan subjektivitas dalam penilaian.
  * Meningkatkan efisiensi dan efektivitas penilaian:
Dengan otomatisasi sebagian proses penilaian, sistem prediksi dapat membantu mempercepat proses sertifikasi. Hal ini memungkinkan asesor untuk fokus pada tugas-tugas lain yang lebih kompleks, seperti memberikan umpan balik yang lebih mendalam kepada peserta atau mengembangkan materi pelatihan. Dengan demikian, model-model ini berpotensi meningkatkan efisiensi dan efektivitas penilaian secara keseluruhan.

## Kesimpulan
Berdasarkan evaluasi metrik dan business understanding, model MLP direkomendasikan sebagai model terbaik untuk prediksi penilaian dalam proses sertifikasi. Namun, penting untuk terus melakukan pengembangan dan evaluasi lebih lanjut, termasuk:

  * Mengumpulkan lebih banyak data: Semakin banyak data yang tersedia, semakin baik model dapat belajar dan menghasilkan prediksi yang lebih akurat.
  * Mencoba arsitektur dan hyperparameter lain: Mungkin ada konfigurasi MLP lain yang dapat menghasilkan performa yang lebih baik.
  * Mengevaluasi model dalam lingkungan nyata: Menguji model dengan data baru dan mendapatkan umpan balik dari asesor akan membantu mengidentifikasi area perbaikan lebih lanjut. <br />

Dengan pengembangan dan evaluasi yang berkelanjutan, sistem prediksi berbasis Neural Network ini memiliki potensi besar untuk meningkatkan kualitas, efisiensi, dan objektivitas proses sertifikasi profesi.

___
## Referensi
---

[[1]](https://proceeding.unnes.ac.id/snpasca/article/view/281) Nur Rohmah. (2019). _Sertifikasi Kompetensi sebagai Upaya Meningkatkan Keunggulan Kompetitif Lulusan Program Studi Tata Laksana Angkutan Laut dan Kepelabuhan Politeknik Ilmu Pelayaran Semarang di Era Disrupsi (Seminar Nasional Pascasarjana, Universitas Negeri Semarang)_. https://proceeding.unnes.ac.id/snpasca/article/view/281 <br />
[[2]](https://jimfeb.ub.ac.id/index.php/jimfeb/article/view/6853) Redyanto, M. (2020). _Analisis Rekrutmen Tenaga Kerja Industri Kreatif (Studi Di Perusahaan 24Slides Malang)_. https://jimfeb.ub.ac.id/index.php/jimfeb/article/view/6853 <br />
[[3]](https://stiemmamuju.e-journal.id/FJIIM/article/download/115/70) Rusman. (2022). _Tantangan Sumber Daya Manusia di Era Globalisasi. Jurnal Ilmiah Ilmu Nusantara_. 1(2), 78-84. https://stiemmamuju.e-journal.id/FJIIM/article/download/115/70 <br />
[[4]](http://dx.doi.org/10.30865/mib.v4i2.2035) Ridwan Ridwan, Hendarman Lubis, Prio Kustanto. (2020). _Implementasi Algoritma Neural Network dalam Memprediksi Tingkat Kelulusan Mahasiswa_. http://dx.doi.org/10.30865/mib.v4i2.2035 <br />
[[5]](http://publication.petra.ac.id/index.php/teknik-informatika/article/view/10496) Kevin Oktovio Lauw, Leo Willyanto Santoso, Rolly Intan. (2020). _Identifikasi Jenis Anjing Berdasarkan Gambar Menggunakan Convolutional Neural Network Berbasis Android_. http://publication.petra.ac.id/index.php/teknik-informatika/article/view/10496 <br />
[[6]](https://publikasi.dinus.ac.id/index.php/jais/article/download/1189/893/) Sani, M. S., Zeniarja, J., & Luthfiarta, A. _Penerapan Algoritma K-Nearest Neighbor pada Information Retrieval dalam Penentuan Topik Referensi Tugas Akhir_. UVol 1, No 2 (2016). https://publikasi.dinus.ac.id/index.php/jais/article/download/1189/893/ <br />
[[7]](https://simdos.unud.ac.id/uploads/file_penelitian_1_dir/721bdb509a6f0bb9ccca6d7374b86759.pdf) Penyelenggara PS. Teknik Informa ka, Jurusan Ilmu Komputer FMIPA - Universitas Udayana Kampus Bukit Jimbaran. _PROSIDING ISSN : X SEMINAR NASIONAL TEKNOLOGI INFORMASI & APLIKASINYA 2015 INOVASI TEKNOLOGI INFORMASI DAN KOMUNIKASI DALAM MENUNJANG TECHNOPRENEURSHIP. Universitas Udayana (2015)_. https://simdos.unud.ac.id/uploads/file_penelitian_1_dir/721bdb509a6f0bb9ccca6d7374b86759.pdfpdf

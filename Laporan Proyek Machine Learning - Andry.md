# Laporan Proyek Machine Learning - Andry Syva Maldini

## Domain Proyek

Domain proyek yang dipilih dalam proyek machine learning ini adalah mengenai pendidikan dengan judul proyek "Sistem Rekomendasi Penilaian Asesor Dalam
Sertifikasi Profesi Berdasarkan Riwayat Belajar Peserta".

- ##### Latar Belakang
  Dalam era globalisasi dan persaingan dunia kerja yang semakin ketat, sertifikasi profesi telah menjadi salah satu tolok ukur penting dalam menilai kompetensi individu di berbagai bidang [1](https://proceeding.unnes.ac.id/snpasca/article/view/281). Sertifikasi ini tidak hanya membantu individu dalam meningkatkan kredibilitas dan daya saing mereka, tetapi juga memberikan jaminan kepada pemberi kerja mengenai kemampuan dan pengetahuan yang dimiliki oleh calon pekerja [2](https://jimfeb.ub.ac.id/index.php/jimfeb/article/view/6853). Dengan demikian, sertifikasi profesional berfungsi sebagai bukti formal atas keterampilan dan pengetahuan, yang dapat meningkatkan peluang kerja serta pengembangan karir seseorang di masa depan. Namun, proses sertifikasi bukanlah hal yang sederhana. Penilaian kompetensi peserta oleh asesor merupakan tahap krusial dalam memastikan bahwa individu yang disertifikasi benar-benar memiliki kemampuan yang diperlukan. Penilaian ini sering kali melibatkan evaluasi berbagai aspek kompetensi, seperti pengetahuan teoritis, keterampilan praktis, dan pengalaman kerja . Dalam konteks ini, tantangan yang dihadapi asesor semakin kompleks, terutama ketika jumlah peserta meningkat dan kriteria penilaian menjadi lebih rumit [3](https://stiemmamuju.e-journal.id/FJIIM/article/download/115/70). Kondisi ini dapat meningkatkan risiko ketidak konsistenan dan subjektivitas dalam penilaian, yang dapat mempengaruhi keadilan dan akurasi hasil sertifikasi.

## Business Understanding

---

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:

- Bagaimana penerapan algoritma Neural Network dapat menghasilkan rekomendasi penilaian yang lebih akurat dan konsisten pada proses sertifikasi?
- Bagaimana cara mengurangi subjektivitas dalam penilaian asesor dengan memanfaatkan riwayat belajar peserta?
- Bagaimana sistem rekomendasi berbasis Neural Network dapat diintegrasikan ke dalam proses sertifikasi profesi untuk meningkatkan efisiensi dan efektivitas penilaian?

### Goals

Menjelaskan tujuan dari pernyataan masalah:

- Menerapkan algoritma Neural Network untuk menghasilkan rekomendasi penilaian yang lebih akurat dan konsisten.
- Mengurangi subjektivitas dalam penilaian asesor dengan memanfaatkan riwayat belajar peserta.
- Mengintegrasikan sistem rekomendasi berbasis Neural Network ke dalam proses sertifikasi profesi untuk meningkatkan efisiensi dan efektivitas penilaian.

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
  ![Image coloumn Unik](https://i.postimg.cc/qRtFZSvK/unik-kolom.jpg)
- Menghapus kolom `PROFILE` sehingga menyisakan kolom untuk analisis lebih lanjut <br />
  ![Image remove profile](https://i.postimg.cc/tRrFSJVL/remove-profile.jpg)
- Men-check missing value pada setiap kolom <br />
  ![Image missing value](https://i.postimg.cc/xCQT3vRL/missing-value.jpg)
- Mengimputasi nilai yang hilang dengan menggunakan median <br />
  ![Image isi kolom](https://i.postimg.cc/FRKC8Rh1/median.jpg)

## Data Preparation

---

Berikut adalah tahapan-tahapan dalam melakukan pra-pemrosesan data:

- Membagi dataset menjadi dua bagian: data latih (70%) dan data uji (30%) menggunakan fungsi train_test_split. Pembagian ini penting dalam pengembangan model machine learning untuk melatih model dan mengevaluasi performanya, serta mencegah overfitting. <br />
  ![Image of Dataset](https://i.postimg.cc/nr14w9gr/splidata.jpg)
- Melakukan standardisasi fitur pada data latih dan uji, sehingga fitur-fitur memiliki rata-rata 0 dan standar deviasi 1. Ini penting untuk banyak algoritma machine learning agar performa model optimal. <br />
  ![Image of Dataset](https://i.postimg.cc/d3t8TtNy/standart.jpg)
- Kode ini membagi data menjadi fitur (X) dan target (y) untuk pelatihan dan pengujian model.<br />
  ![Image of Dataset](https://i.postimg.cc/tTZ0GWHr/data-x-y.jpg)

## Modeling

---

Setelah dilakukan pra-pemrosesan pada dataset, langkah selanjutnya adalah modeling terhadap data. Pada tahap ini menggunakan 2 algoritma yaitu K-Nearest Neighbor (KNN) dan Neural Network (NN) dengan tanpa parameter tambahan. Pertama-tama kedua model ini dilatih menggunakan data latih. Setelah itu kedua model akan diuji dengan data uji. Terakhir kedua model akan diukur nilai akurasinya. Perbandingan hasil dari kedua model akan dianalisis untuk menentukan algoritma terbaik.

Perbandingan Hasil dari kedua model sebagai berikut:<br />
![Image perfomance model](https://i.postimg.cc/HLs5H8R0/model.jpg)

- _Confussion Matrix_ algoritma K-Nearest Neighbor:<br />
  ![Image of Dataset](https://i.postimg.cc/bv9bWRBy/output-knn.png)
- _Confussion Matrix_ algoritma Neural Network:<br />
  ![Image of Dataset](https://i.postimg.cc/V6HSPZB8/output-nn.png)

### Model Akhir yang Digunakan Neural Network

- Pembuatan Model <br />
  Model yang digunakan adalah Multi-Layer Perceptron (MLP), yang merupakan salah satu jenis jaringan saraf tiruan. MLP adalah model yang terdiri dari beberapa lapisan neuron (nodes) yang terhubung penuh (fully connected) antara satu lapisan dengan lapisan lainnya. Setiap neuron dalam lapisan tertentu terhubung dengan semua neuron di lapisan berikutnya.
- Konsep Algoritma Model <br />
  MLP bekerja dengan cara mengalirkan input (data) melalui lapisan-lapisan jaringan, melakukan transformasi non-linear di setiap lapisan, dan akhirnya menghasilkan output. Proses ini melibatkan perkalian matriks input dengan bobot-bobot (weights) pada setiap koneksi, penambahan bias, dan penerapan fungsi aktivasi untuk menentukan output dari neuron tersebut.
- Hyperparameter yang Digunakan <br />
  Dalam model yang dibuat, terdapat beberapa hyperparameter yang diatur, yaitu:
  - hidden_layer_sizes=(128,64,32): Ini berarti model memiliki tiga lapisan tersembunyi dengan jumlah neuron masing-masing sebanyak 128, 64, dan 32. Setiap lapisan ini bertugas untuk mengekstraksi fitur dari data secara berurutan, di mana lapisan yang lebih dalam diharapkan mampu menangkap pola yang lebih kompleks.
  - solver='adam': Solver yang digunakan untuk optimisasi adalah 'adam', yang merupakan salah satu metode optimasi berbasis gradien dengan adaptasi pembelajaran untuk setiap parameter. Adam sangat populer karena efisien dalam hal waktu dan performa yang baik pada berbagai jenis data.
  - max_iter=500: Ini adalah jumlah maksimum iterasi yang akan dijalankan selama proses pelatihan. Jika model belum mencapai konvergensi dalam 500 iterasi, maka proses pelatihan akan berhenti.
- Proses Pelatihan <br />
  Proses pelatihan dilakukan dengan menggunakan data pelatihan (X_train) dan label (y_train). Label y_train diubah menjadi vektor 1D menggunakan np.ravel() agar sesuai dengan format yang diharapkan oleh model.<br/> Model dilatih untuk meminimalkan kesalahan prediksi dengan memperbarui bobot-bobotnya pada setiap iterasi berdasarkan error yang dihitung melalui backpropagation. Proses ini berlangsung hingga model mencapai jumlah iterasi maksimal atau sampai model mencapai konvergensi, yaitu ketika perubahan dalam fungsi loss (kerugian) sudah sangat kecil.<br/>

## Evaluation

---

Setelah pelatihan selesai, model digunakan untuk memprediksi data uji (X_test). Hasil prediksi disimpan dalam variabel y_pred. Kemudian, performa model dievaluasi dengan menggunakan laporan klasifikasi (classification_report) yang menampilkan metrik-metrik penting seperti precision, recall, f1-score, dan akurasi.<br /> Dari hasil yang ditampilkan pada gambar, dapat dilihat bahwa model memiliki performa yang baik dengan precision, recall, dan f1-score yang konsisten tinggi pada setiap kelas yang diuji. Ini menunjukkan bahwa model MLP ini mampu mengklasifikasikan data uji dengan akurasi yang cukup tinggi. <br />

![Image of Dataset](https://i.postimg.cc/76FshrFN/evaluasi.png)

1. Penerapan Algoritma Neural Network untuk Rekomendasi Penilaian yang Lebih Akurat dan Konsisten <br />
Algoritma Neural Network dapat diterapkan dalam proses sertifikasi untuk mengolah data yang kompleks dan non-linear dari berbagai sumber, seperti riwayat belajar peserta, hasil ujian sebelumnya, umpan balik dari pelatihan, dan performa peserta selama kursus. Neural Network memiliki kemampuan untuk belajar dari data historis ini dan mengidentifikasi pola-pola penting yang mungkin tidak terlihat oleh manusia.
    * Pemrosesan Data Multi-Dimensional: Neural Network mampu menangani banyak fitur input, seperti waktu yang dihabiskan peserta dalam belajar, tingkat kesulitan materi yang dipelajari, dan hasil tes sebelumnya. Ini memungkinkan model untuk memberikan rekomendasi              penilaian yang mempertimbangkan semua aspek yang relevan, sehingga hasil penilaian menjadi lebih akurat dan konsisten.
    * Prediksi Berbasis Pola Historis: Dengan memanfaatkan data dari peserta sebelumnya yang memiliki karakteristik atau riwayat belajar yang serupa, model dapat memberikan prediksi atau rekomendasi penilaian yang sesuai dengan performa nyata yang diharapkan, sehingga          mengurangi bias atau inkonsistensi yang mungkin muncul dalam penilaian manual.
2. Mengurangi Subjektivitas dalam Penilaian Asesor dengan Memanfaatkan Riwayat Belajar Peserta <br />
Subjektivitas dalam penilaian sering kali muncul karena penilaian didasarkan pada persepsi individual dari asesor, yang bisa dipengaruhi oleh faktor-faktor non-akademis. Dengan menggunakan algoritma Neural Network, riwayat belajar peserta dapat diolah untuk memberikan penilaian yang lebih objektif.
    * Standardisasi Penilaian: Neural Network dapat digunakan untuk menciptakan model penilaian yang seragam berdasarkan data historis, sehingga penilaian yang dihasilkan menjadi lebih konsisten antara satu asesor dengan yang lain. Model ini secara otomatis dapat               mempertimbangkan faktor-faktor yang relevan dari riwayat belajar peserta tanpa dipengaruhi oleh preferensi atau bias asesor.
    * Penilaian Berdasarkan Data: Algoritma Neural Network dapat diberi akses ke data riwayat belajar, seperti kinerja dalam tugas-tugas tertentu, kecepatan dalam menyelesaikan materi, dan keterampilan yang telah dikuasai. Model kemudian dapat memberikan penilaian yang         didasarkan pada data yang valid, mengurangi kemungkinan penilaian yang dipengaruhi oleh opini atau persepsi asesor.
3. Integrasi Sistem Rekomendasi Berbasis Neural Network dalam Proses Sertifikasi Profesi <br />
Integrasi sistem rekomendasi berbasis Neural Network ke dalam proses sertifikasi profesi dapat meningkatkan efisiensi dan efektivitas penilaian melalui beberapa cara:
    * Automatisasi Penilaian Awal: Sistem Neural Network dapat diintegrasikan sebagai alat bantu untuk melakukan penilaian awal terhadap peserta berdasarkan data yang ada, sebelum asesor memberikan penilaian akhir. Ini bisa mengurangi beban kerja asesor dan mempercepat         proses sertifikasi.
    * Pemberian Umpan Balik yang Lebih Tepat: Sistem ini juga dapat digunakan untuk memberikan umpan balik secara otomatis kepada peserta berdasarkan hasil penilaian yang dihasilkan oleh Neural Network. Umpan balik ini dapat membantu peserta memahami kekuatan dan               kelemahan mereka serta memberikan rekomendasi untuk perbaikan, yang pada akhirnya meningkatkan kualitas peserta yang disertifikasi.
    * Pengambilan Keputusan yang Lebih Cepat dan Tepat: Dengan integrasi Neural Network, pengambilan keputusan dalam sertifikasi dapat dilakukan lebih cepat karena rekomendasi yang dihasilkan sistem dapat langsung digunakan oleh asesor sebagai referensi. Hal ini akan           meningkatkan efektivitas proses penilaian tanpa mengurangi kualitas hasil akhir.

## Kesimpulan
Menggunakan algoritma Neural Network dalam proses sertifikasi dapat secara signifikan meningkatkan akurasi dan konsistensi penilaian. Dengan memanfaatkan riwayat belajar peserta, sistem ini dapat mengurangi subjektivitas penilaian asesor, memberikan rekomendasi penilaian yang lebih objektif, dan mempercepat proses sertifikasi melalui automatisasi dan efisiensi yang lebih baik. Integrasi sistem ini ke dalam proses sertifikasi tidak hanya akan memperbaiki kualitas penilaian tetapi juga memberikan nilai tambah dalam hal peningkatan kompetensi peserta dan kredibilitas proses sertifikasi itu sendiri.

## Referensi

---

[[1]](https://proceeding.unnes.ac.id/snpasca/article/view/281) Nur Rohmah. (2019). _Sertifikasi Kompetensi sebagai Upaya Meningkatkan Keunggulan Kompetitif Lulusan Program Studi Tata Laksana Angkutan Laut dan Kepelabuhan Politeknik Ilmu Pelayaran Semarang di Era Disrupsi (Seminar Nasional Pascasarjana, Universitas Negeri Semarang)_. https://proceeding.unnes.ac.id/snpasca/article/view/281 <br />
[[2]](https://jimfeb.ub.ac.id/index.php/jimfeb/article/view/6853) Redyanto, M. (2020). _Analisis Rekrutmen Tenaga Kerja Industri Kreatif (Studi Di Perusahaan 24Slides Malang)_. https://jimfeb.ub.ac.id/index.php/jimfeb/article/view/6853 <br />
[[3]](https://stiemmamuju.e-journal.id/FJIIM/article/download/115/70) Rusman. (2022). _Tantangan Sumber Daya Manusia di Era Globalisasi. Jurnal Ilmiah Ilmu Nusantara_. 1(2), 78-84. https://stiemmamuju.e-journal.id/FJIIM/article/download/115/70 <br />
[[4]](http://dx.doi.org/10.30865/mib.v4i2.2035) Ridwan Ridwan, Hendarman Lubis, Prio Kustanto. (2020). _Implementasi Algoritma Neural Network dalam Memprediksi Tingkat Kelulusan Mahasiswa_. http://dx.doi.org/10.30865/mib.v4i2.2035 <br />
[[5]](http://publication.petra.ac.id/index.php/teknik-informatika/article/view/10496) Kevin Oktovio Lauw, Leo Willyanto Santoso, Rolly Intan. (2020). _Identifikasi Jenis Anjing Berdasarkan Gambar Menggunakan Convolutional Neural Network Berbasis Android_. http://publication.petra.ac.id/index.php/teknik-informatika/article/view/10496 <br />
[[6]](https://publikasi.dinus.ac.id/index.php/jais/article/download/1189/893/) Sani, M. S., Zeniarja, J., & Luthfiarta, A. _Penerapan Algoritma K-Nearest Neighbor pada Information Retrieval dalam Penentuan Topik Referensi Tugas Akhir_. UVol 1, No 2 (2016). https://publikasi.dinus.ac.id/index.php/jais/article/download/1189/893/ <br />
[[7]](https://simdos.unud.ac.id/uploads/file_penelitian_1_dir/721bdb509a6f0bb9ccca6d7374b86759.pdf) Penyelenggara PS. Teknik Informa ka, Jurusan Ilmu Komputer FMIPA - Universitas Udayana Kampus Bukit Jimbaran. _PROSIDING ISSN : X SEMINAR NASIONAL TEKNOLOGI INFORMASI & APLIKASINYA 2015 INOVASI TEKNOLOGI INFORMASI DAN KOMUNIKASI DALAM MENUNJANG TECHNOPRENEURSHIP. Universitas Udayana (2015)_. https://simdos.unud.ac.id/uploads/file_penelitian_1_dir/721bdb509a6f0bb9ccca6d7374b86759.pdfpdf

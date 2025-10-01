# Analisis Faktor Kinerja Akademik & Prediksi Kelulusan Mahasiswa Menggunakan AI

**Capstone Project untuk Program Student Development Initiative oleh Hacktiv8 & IBM SkillsBuild**

---

##  Daftar Isi
1.  [Deskripsi Proyek](#1-deskripsi-proyek)
2.  [Latar Belakang & Permasalahan](#2-latar-belakang--permasalahan)
3.  [Tujuan Proyek](#3-tujuan-proyek)
4.  [Dataset yang Digunakan](#4-dataset-yang-digunakan)
5.  [Metodologi & Alur Kerja](#5-metodologi--alur-kerja)
6.  [Peran AI & Penjelasan Dukungan (AI Support Explanation)](#6-peran-ai--penjelasan-dukungan-ai-support-explanation)
7.  [Temuan Utama & Wawasan (Insight & Findings)](#7-temuan-utama--wawasan-insight--findings)
8.  [Kesimpulan & Rekomendasi](#8-kesimpulan--rekomendasi)
9.  [Cara Menjalankan Proyek Ini](#9-cara-menjalankan-proyek-ini)
10. [Teknologi yang Digunakan](#10-teknologi-yang-digunakan)

---

## 1. Deskripsi Proyek
Proyek ini merupakan sebuah studi analisis data yang bertujuan untuk mengidentifikasi faktor-faktor kunci dari gaya hidup dan kebiasaan belajar yang mempengaruhi kinerja akademik mahasiswa. Dengan memanfaatkan model *Large Language Model* (LLM) canggih dari **IBM Granite**, proyek ini tidak hanya menganalisis data historis, tetapi juga membangun sebuah sistem prediktif untuk mengklasifikasikan potensi kelulusan mahasiswa. Hasil akhir dari proyek ini adalah serangkaian wawasan berbasis data dan rekomendasi strategis yang dapat ditindaklanjuti.

---

## 2. Latar Belakang & Permasalahan
Keberhasilan akademik seorang mahasiswa adalah hasil dari interaksi kompleks antara berbagai faktor, baik internal maupun eksternal. Institusi pendidikan seringkali kesulitan untuk mengidentifikasi mahasiswa yang berisiko mengalami kegagalan secara dini. Pendekatan tradisional yang hanya mengandalkan nilai seringkali reaktif, bukan proaktif.

**Permasalahan Utama:**
* Kurangnya pemahaman kuantitatif tentang faktor non-akademik (seperti jam tidur dan jam belajar) yang paling signifikan mempengaruhi kelulusan.
* Kesulitan dalam memprediksi mahasiswa mana yang membutuhkan intervensi sebelum ujian akhir berlangsung.
* Kebutuhan akan strategi berbasis data untuk meningkatkan angka kelulusan dan kualitas pembelajaran.

Proyek ini hadir untuk menjawab tantangan tersebut dengan menggunakan pendekatan *data science* dan AI.

---

## 3. Tujuan Proyek
Tujuan utama dari proyek ini dipecah menjadi tiga pilar utama:
1.  **Tujuan Analisis:** Melakukan *Exploratory Data Analysis* (EDA) secara mendalam untuk memvisualisasikan dan memahami korelasi antara variabel gaya hidup (jam belajar, jam tidur, kehadiran) dengan hasil akademik (nilai ujian).
2.  **Tujuan Prediksi:** Mengaplikasikan model AI **IBM Granite** untuk melakukan tugas klasifikasi, yaitu memprediksi status kelulusan ('Lulus' atau 'Gagal') untuk setiap mahasiswa berdasarkan profil data mereka, sekaligus memberikan justifikasi untuk setiap prediksi.
3.  **Tujuan Rekomendasi:** Meringkas temuan menjadi profil yang jelas dan menghasilkan rekomendasi strategis yang dapat ditindaklanjuti (*actionable*) bagi dua audiens utama: mahasiswa (untuk perbaikan diri) dan institusi pendidikan (untuk pengembangan sistem pendukung).

---

## 4. Dataset yang Digunakan
* **Nama Dataset:** Student Exam Scores: Extended Dataset
* **Sumber:** Kaggle
* **Link:** *https://www.kaggle.com/datasets/emanfatima2025/student-academic-performance-trends*
* **Deskripsi Kolom:**
    * `student_id`: Identifier unik untuk setiap mahasiswa.
    * `hours_studied`: Rata-rata jam belajar mahasiswa per hari.
    * `sleep_hours`: Rata-rata jam tidur mahasiswa per hari.
    * `attendance_percent`: Persentase kehadiran mahasiswa di kelas.
    * `previous_scores`: Skor kumulatif dari ujian-ujian sebelumnya.
    * `exam_score`: Skor ujian akhir (variabel target).

---

## 5. Metodologi & Alur Kerja
Proyek ini mengikuti alur kerja analisis data yang terstruktur:

1.  **Setup Environment:** Menginstal semua library Python yang dibutuhkan (`langchain`, `replicate`, `pandas`, `matplotlib`, `seaborn`) di Google Colab dan melakukan koneksi ke Replicate API.

2.  **Pemuatan & Pembersihan Data:** Memuat dataset dari file `.csv` dan melakukan pengecekan data kosong (*missing values*) untuk memastikan kualitas data.

3.  **Analisis Data Eksploratif (EDA):** Melakukan analisis statistik deskriptif dan membuat serangkaian visualisasi data (histogram, *scatter plot*, *pairplot*) untuk mengidentifikasi pola, distribusi, dan korelasi awal antar variabel.

4.  **Feature Engineering:** Mengubah masalah dari regresi (memprediksi nilai angka) menjadi klasifikasi (memprediksi kategori). Sebuah kolom baru bernama `status_kelulusan` dibuat dengan aturan: jika `exam_score` >= 75, maka statusnya 'Lulus', jika tidak maka 'Gagal'.

5.  **Prompt Engineering:** Merancang *prompt* (instruksi teks) yang detail dan terstruktur untuk berkomunikasi dengan model AI IBM Granite. Data numerik mahasiswa diubah menjadi format naratif agar mudah dipahami oleh AI untuk dua tugas utama: klasifikasi dan peringkasan.

6.  **Eksekusi AI & Interpretasi:** Menjalankan model AI dengan *prompt* yang telah dirancang. Karena jumlah data yang besar (200 baris), proses eksekusi dilakukan secara *batch* (per gelombang) untuk menghindari batas token dan memastikan semua data diproses. Hasil dari AI kemudian dianalisis dan diinterpretasikan.

---

## 6. Peran AI & Penjelasan Dukungan (AI Support Explanation)
Model AI **IBM Granite (`ibm-granite/granite-3.3-8b-instruct`)** adalah inti dari analisis prediktif dalam proyek ini. Perannya dibagi menjadi dua tugas utama:

1.  **Klasifikasi sebagai Konselor Akademik:**
    * **Peran:** AI diminta untuk berperan sebagai seorang konselor akademik yang ahli.
    * **Tugas:** Berdasarkan data naratif setiap mahasiswa, AI harus memprediksi status kelulusan mereka ('Lulus' atau 'Gagal').
    * **Justifikasi:** AI tidak hanya memberikan prediksi, tetapi juga diinstruksikan untuk memberikan alasan singkat di balik setiap prediksinya, meniru proses pengambilan keputusan seorang konselor. Ini menambah tingkat interpretasi pada hasil.

2.  **Peringkasan sebagai Manajer Produk Pendidikan:**
    * **Peran:** AI kemudian diminta untuk mengambil peran sebagai seorang manajer yang perlu melaporkan temuan.
    * **Tugas:** Berdasarkan hasil klasifikasi sebelumnya, AI harus menganalisis dan menyarikan karakteristik umum dari kelompok mahasiswa 'Lulus' dan 'Gagal'.
    * **Output:** Hasilnya adalah dua profil ringkas yang menyoroti faktor-faktor kunci keberhasilan dan faktor-faktor risiko kegagalan, yang sangat berguna untuk penyusunan strategi.

---

## 7. Temuan Utama & Wawasan (Insight & Findings)
* **Wawasan dari Visualisasi:**
    * Grafik *scatter plot* dengan jelas menunjukkan adanya **korelasi positif yang kuat** antara `hours_studied` dan `exam_score`. Semakin lama mahasiswa belajar, semakin tinggi potensi nilainya.
    * Hal yang sama berlaku untuk `attendance_percent`. Mahasiswa dengan tingkat kehadiran tinggi secara konsisten mendapatkan skor yang lebih baik.

* **Wawasan dari Analisis AI:**
    * **Profil Mahasiswa Lulus:** AI mengidentifikasi bahwa mahasiswa yang berhasil secara konsisten memiliki **jam belajar di atas 6 jam per hari** dan **persentase kehadiran melebihi 90%**. Faktor-faktor ini bahkan lebih dominan daripada skor ujian sebelumnya.
    * **Profil Mahasiswa Gagal:** Faktor risiko utama yang disorot oleh AI adalah kombinasi **jam belajar yang sangat rendah (kurang dari 4 jam per hari)** dan **tingkat kehadiran di bawah 75%**.
    * **Insight Paling Krusial:** Proyek ini membuktikan bahwa **disiplin dan konsistensi (diukur dari jam belajar dan kehadiran) adalah prediktor keberhasilan akademik yang lebih andal** daripada bakat atau riwayat akademik semata.

---

## 8. Kesimpulan & Rekomendasi
**Kesimpulan:**
Keberhasilan akademik bukanlah sebuah kebetulan, melainkan hasil dari perilaku yang dapat diukur dan diperbaiki. Faktor-faktor seperti alokasi waktu belajar dan partisipasi aktif di kelas adalah pilar utama yang menopang prestasi mahasiswa. Analisis berbasis AI ini berhasil mengkonfirmasi hipotesis tersebut dan memberikan dasar yang kuat untuk intervensi.

**Rekomendasi Strategis:**
1.  **Untuk Mahasiswa (Rekomendasi Mikro):**
    * Secara proaktif membuat jadwal belajar yang menargetkan **durasi minimal 6 jam per hari**.
    * Menjadikan **kehadiran di kelas sebagai prioritas utama**, karena ini adalah indikator paling sederhana dari keterlibatan dalam proses belajar.

2.  **Untuk Institusi Pendidikan (Rekomendasi Makro):**
    * Mengembangkan dan mengimplementasikan **sistem peringatan dini (*early warning system*)** yang terotomatisasi.
    * Sistem ini dapat menggunakan data absensi sebagai pemicu utama. Mahasiswa dengan **tingkat kehadiran di bawah 75%** pada pertengahan semester harus secara otomatis ditandai untuk menerima sesi konseling akademik proaktif dari pihak fakultas atau dosen wali.

---

## 9. Cara Menjalankan Proyek Ini
1.  **Prasyarat:** Anda harus memiliki akun Google dan akun Replicate untuk mendapatkan API Token.
2.  **Unduh Repository:** Lakukan `git clone` pada repository ini atau unduh sebagai file ZIP.
3.  **Buka Google Colab:** Buka file `.ipynb` yang ada di repository ini menggunakan Google Colab.
4.  **Setup API Token:**
    * Klik ikon **kunci (🔑)** di sidebar kiri Colab untuk membuka *Secrets*.
    * Buat *secret* baru dengan nama `api_token`.
    * Masukkan nilai API Token Anda dari Replicate ke dalam kolom *Value*.
    * Aktifkan *toggle* "Notebook access".
5.  **Upload Dataset:** Unggah file `student_exam_scores.csv` ke sesi Colab dengan mengklik ikon folder di sidebar kiri, lalu klik tombol "Upload".
6.  **Jalankan Notebook:** Klik `Runtime` > `Run all` untuk menjalankan semua cell secara berurutan.

---

## 10. Teknologi yang Digunakan
* **Bahasa Pemrograman:** Python
* **Lingkungan Kerja:** Google Colaboratory
* **Library Utama:**
    * `Pandas`: Untuk manipulasi dan analisis data.
    * `Matplotlib` & `Seaborn`: Untuk visualisasi data.
    * `LangChain`: Sebagai framework untuk berinteraksi dengan LLM.
* **Platform AI:** Replicate
* **Model AI:** IBM Granite (`ibm-granite/granite-3.3-8b-instruct`)

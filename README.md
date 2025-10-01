# Capstone-Project-Student-Performance

# 1. Title Project
Analisis Faktor Kinerja Akademik & Prediksi Kelulusan Mahasiswa Menggunakan AI

---

# 2. Project Overview
Proyek ini bertujuan untuk menganalisis faktor-faktor gaya hidup yang mempengaruhi kinerja akademik mahasiswa. Dengan menggunakan model AI IBM Granite, proyek ini melakukan klasifikasi untuk memprediksi status kelulusan ('Lulus'/'Gagal') dan membuat peringkasan untuk mengidentifikasi profil mahasiswa yang berisiko dan yang berprestasi. Tujuannya adalah untuk memberikan rekomendasi berbasis data yang dapat ditindaklanjuti bagi mahasiswa dan institusi pendidikan.

---

# 3. Raw Dataset Link
- **Nama Dataset:** Student Exam Scores
- **Sumber:** Kaggle
- **Link:** [MASUKKAN LINK DATASET DARI KAGGLE DI SINI]

---

# 4. Insight & Findings
Berdasarkan analisis visual dan hasil dari IBM Granite, ditemukan beberapa wawasan kunci:
- **Korelasi Kuat:** Terdapat korelasi positif yang kuat antara `hours_studied` (jam belajar) dan `attendance_percent` (kehadiran) terhadap `exam_score` (nilai ujian).
- **Profil Kelulusan:** AI berhasil meringkas bahwa profil mahasiswa "Lulus" secara konsisten menunjukkan jam belajar di atas 6 jam dan kehadiran di atas 90%.
- **Faktor Risiko Kegagalan:** Sebaliknya, profil mahasiswa "Gagal" ditandai dengan jam belajar yang sangat rendah (< 4 jam) dan tingkat kehadiran di bawah 75%.
- **Insight Utama:** Disiplin (jam belajar & kehadiran) terbukti menjadi prediktor kelulusan yang lebih kuat daripada skor ujian sebelumnya.

---

# 5. AI Support Explanation
Model AI **IBM Granite (`ibm-granite/granite-3.3-8b-instruct`)** digunakan untuk dua tugas utama *Natural Language Processing* (NLP) dalam proyek ini:
1.  **Klasifikasi Teks:** Setelah data numerik diubah menjadi format deskriptif, model AI digunakan untuk memprediksi status kelulusan setiap mahasiswa berdasarkan profil kebiasaan mereka.
2.  **Peringkasan Teks:** Model AI menganalisis dan menyarikan karakteristik umum dari kelompok mahasiswa 'Lulus' dan 'Gagal', lalu membuat profil ringkas yang mudah dipahami.

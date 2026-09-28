# Praktikum Machine Learning - Pertemuan 5: SVM & Naïve Bayes
**Repository:** `pertemuan5-tugas-svm-naivebayes`  
**Nama:** Arifian Ilham Nur Riandana  
**Username GitHub:** `arifianilhamnrr`  
**Studi Kasus:** Sistem Klasifikasi Sentimen Komentar Konten Dakwah Media Sosial Pesantren  

---

## 📌 Deskripsi Proyek
Proyek ini mengimplementasikan pipeline klasifikasi teks lengkap untuk memfilter dan mengelompokkan komentar dakwah di media sosial pesantren ke dalam 3 kelas:
1. **Positif:** Testimoni, apresiasi, doa, dan kesan pencerahan hati.
2. **Netral:** Pertanyaan teknis, jadwal pengajian, info kitab rujukan, kontak panitia.
3. **Negatif:** Kritik kualitas audio/visual, komplain tema/durasi, retorika provokatif.

Proyek ini mencakup perbandingan algoritma **Support Vector Machine (SVM)** dan **Naïve Bayes (Multinomial & Bernoulli)**, baik implementasi *from scratch* (dengan Laplace Smoothing) maupun menggunakan library `scikit-learn` dengan representasi ekstraksi fitur **CountVectorizer** dan **TfidfVectorizer**.

---

## 📁 Struktur Direktori
```text
pertemuan5-tugas-svm-naivebayes/
├── dataset_komentar_dakwah.csv           # Dataset teks (75 data: 25 positif, 25 netral, 25 negatif)
├── Tugas_Praktikum_SVM_Naive_Bayes.ipynb # Notebook Jupyter lengkap dengan output & visualisasi
├── .gitignore                            # Git ignore file
└── README.md                             # Dokumentasi proyek & ringkasan hasil
```

---

## 📊 Hasil Eksperimen & Perbandingan Model
Evaluasi dilakukan pada 20% data pengujian terstratifikasi ($N = 15$ data uji, 5 per kelas):

| Model Klasifikasi | Ekstraksi Fitur | Accuracy | Precision | Recall | F1-Score |
|---|---|:---:|:---:|:---:|:---:|
| **NB Scratch ($\alpha = 1.0$)** | Count | 86.67% | 88.89% | 86.67% | 85.61% |
| **NB Multinomial** | Count | 86.67% | 88.89% | 86.67% | 85.61% |
| **NB Multinomial** | TF-IDF | 86.67% | 88.89% | 86.67% | 85.61% |
| **NB Bernoulli** | Count | 86.67% | 87.78% | 86.67% | 86.60% |
| **SVM Linear** | Count | 80.00% | 84.92% | 80.00% | 77.13% |
| **SVM Linear** | TF-IDF | **86.67%** | **88.89%** | **86.67%** | **85.61%** |
| **SVM RBF** | TF-IDF | **86.67%** | **88.89%** | **86.67%** | **85.61%** |
| **SVM Polynomial ($d=3$)**| TF-IDF | 86.67% | 87.78% | 86.67% | 86.60% |

### Temuan Utama:
1. **Multinomial Naïve Bayes from Scratch** menghasilkan prediksi yang identik secara matematis dengan `scikit-learn` berkat implementasi Laplace smoothing $\frac{N_{ci} + \alpha}{N_c + \alpha |V|}$.
2. Nilai $\alpha = 1.0$ dan $\alpha = 2.0$ memberikan performa optimal (F1 85.61%) dibanding smoothing kecil ($\alpha = 0.01$ hanya 77.13%) karena dataset teks berukuran terfokus membutuhkan regularisasi kata jarang.
3. Ekstraksi fitur **TF-IDF mendongkrak performa SVM Linear** dari 80.00% menjadi 86.67% (F1 naik dari 77.13% ke 85.61%), membuktikan reduksi penalti kata frekuensi tinggi sangat krusial bagi margin hyperplane SVM.
4. **5-Fold Cross Validation:** Model Naive Bayes mencatat skor CV F1 rata-rata sebesar **0.8923 ± 0.0808**, sedangkan SVM mencatat **0.8669 ± 0.1101**.

---

## 🔍 Kata-Kata Paling Indikatif (Top Feature Importance)
* **Positif:** *bermanfaat, menyejukkan, ceramahnya, ustadz, alhamdulillah, ilmu, terima, kasih, hikmah, santun*.
* **Netral:** *kajian, apakah, jadwal, informasi, mohon, kitab, tanya, link, lokasi, panitia*.
* **Negatif:** *membosankan, materi, ustadz, terlalu, panjang, buruk, audionya, kecewa, dangkal, kasar*.

---

## ⚖️ Refleksi Etika Keislaman
1. **Prinsip 'Adl (Keadilan Objektif):** Menjaga agar kritik santun yang konstruktif (*nashihatul mukminin*) tidak disalahartikan sebagai sentimen negatif/ujaran kebencian.
2. **Menghormati Khazanah Ikhtilaf:** Istilah madzhab atau diskusi fiqhiyah tidak boleh dilabeli negatif secara bias oleh algoritma.
3. **Prinsip Maslahah & Tabayyun:** AI bertindak sebagai asisten administratif (*khadim*), sedangkan keputusan intervensi penting tetap melalui musyawarah (*Syura*) dan verifikasi manusia (*Tabayyun*, QS. Al-Hujurat: 6).

---

## 🚀 Cara Menjalankan di Google Colab
1. Buka [Google Colab](https://colab.research.google.com/).
2. Pilih tab **GitHub**, masukkan URL repository ini: `https://github.com/arifianilhamnrr/pertemuan5-tugas-svm-naivebayes`.
3. Klik file `Tugas_Praktikum_SVM_Naive_Bayes.ipynb` dan pilih **Runtime → Run all**.

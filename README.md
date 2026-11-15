---
# Analisis Sentimen Ulasan Google Maps Rumah Sakit di Kota Batam

[![Proyek PBL](https://img.shields.io/badge/PBL-PBLIF3--PD12-blue)](https://github.com/users/ryanthimothy184-ux/projects/1)
[![Institusi](https://img.shields.io/badge/Politeknik%20Negeri%20Batam-Teknik%20Informatika-orange)]()
[![Python](https://img.shields.io/badge/Python-3.11-green)]()

## 📌 Deskripsi Proyek

Projek ini menganalisis sentimen ulasan Google Maps terhadap pelayanan rumah sakit di Kota Batam menggunakan pendekatan *Natural Language Processing* (NLP) dan *Machine Learning*. Data ulasan melewati tahap *preprocessing*, lalu diklasifikasikan menjadi tiga kategori sentimen: **Positif**, **Netral**, atau **Negatif**. Hasilnya berupa distribusi sentimen pengguna yang dapat menjadi bahan evaluasi berbasis data bagi manajemen rumah sakit.

Proyek ini dikembangkan untuk memenuhi mata kuliah **IF314 Proyek Inovasi Agile** di Program Studi Teknik Informatika, Politeknik Negeri Batam (2026).

---

## 🎯 Tujuan & Ruang Lingkup

* **Akuisisi Data Ulasan:** Mengumpulkan ulasan publik Google Maps rumah sakit di Kota Batam menggunakan *scraper* otomatis (Apify / Playwright) di luar aplikasi utama.
* **Pra-pemrosesan & Pelabelan:** Membersihkan teks ulasan (*cleaning*, *case folding*, normalisasi kata tidak baku, *stopword removal*, dan *stemming* bahasa Indonesia) serta melabeli sentimen secara terstruktur.
* **Pemodelan Klasifikasi Sentimen:**
  * **Model Baseline:** Ekstraksi fitur **TF-IDF** (*unigram* & *bigram*) dengan algoritma **Linear SVM**, *Logistic Regression*, dan *Multinomial Naïve Bayes* (target `F1-macro ≥ 0,65`).
  * **Model Utama:** *Fine-tuning* **IndoBERT** (`indobenchmark/indobert-base-p1`) dengan penanganan ketimpangan kelas (target `F1-macro ≥ 0,75` dan `Recall kelas negatif ≥ 0,80`).
* **Aplikasi Web & Dashboard:** Menyediakan antarmuka web bagi admin/analis untuk menguji klasifikasi teks satuan maupun unggah berkas CSV, memfilter hasil per rumah sakit/sentimen, melihat *word cloud* keluhan, serta mengekspor laporan dalam format PDF.

---

## ⚙️ Alur Kerja Sistem

1. **Akuisisi Data:** Pengumpulan ulasan publik rumah sakit di Batam (kolom: `nama_tempat`, `bintang`, `ulasan`) tanpa menyimpan nama akun *reviewer*.
2. **Pipeline Data & Model:** Pra-pemrosesan teks $\rightarrow$ Pembagian data *stratified* (70% latih, 15% validasi, 15% uji) $\rightarrow$ Ekstraksi fitur & pelatihan model $\rightarrow$ Evaluasi (*Accuracy*, *Precision*, *Recall*, *F1-macro*, *Confusion Matrix*) $\rightarrow$ Penyimpanan artefak model.
3. **Aplikasi Web:** Autentikasi pengguna $\rightarrow$ Input ulasan (teks/CSV) $\rightarrow$ Inferensi model $\rightarrow$ Penyimpanan ke PostgreSQL $\rightarrow$ Visualisasi *dashboard* & ekspor laporan PDF.

---

## 🛠️ Teknologi yang Digunakan

| Kategori | Teknologi / Pustaka | Kegunaan |
| :--- | :--- | :--- |
| **Bahasa Pemrograman** | Python 3.11 | Pengembangan *pipeline* data, pemodelan, dan aplikasi |
| **Pengolahan Data** | `pandas`, `numpy` | Manipulasi dan pembersihan dataset tabular |
| **NLP Bahasa Indonesia** | `PySastrawi`, `difflib` | *Stemming*, *stopword removal*, dan koreksi *typo* label |
| **Machine Learning** | `scikit-learn`, `imbalanced-learn` | Ekstraksi fitur TF-IDF, SVM, evaluasi metrik, dan SMOTE |
| **Deep Learning** | `PyTorch`, `Hugging Face Transformers` | *Fine-tuning* dan inferensi model `indobert-base-p1` |
| **Web & Database** | Streamlit / Web App, PostgreSQL | Antarmuka *dashboard* analitik dan penyimpanan hasil |

---

## 📁 Struktur Repositori

```text
pbl-analisis-sentimen-rs-batam/
├── data/                    # Dokumentasi struktur dataset & tautan penyimpanan terbatas
├── dokumentasi/             # Dokumen laporan kemajuan, RPP, slide presentasi, & diagram
├── notebook/                # Jupyter/Colab notebooks (eksplorasi, preprocessing, check_typo, training)
├── src/                     # Modul skrip pra-pemrosesan, pelatihan, dan inferensi (tahap integrasi)
├── app/                     # Kode sumber aplikasi web & dashboard visualisasi (tahap integrasi)
├── models/                  # Metadata & konfigurasi artefak model terlatih
├── scrapping_data_opsi.md   # Dokumentasi teknis proses scraping data ulasan
└── README.md                # Dokumentasi utama repositori

# Time-series Sentiment Tracking pada Trend Penggunaan APP Gojek (Play Store Reviews)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2C2D72?style=for-the-badge&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge&logo=python&logoColor=white)
![Functional Programming](https://img.shields.io/badge/Paradigm-Functional_Programming-00599C?style=for-the-badge)

Repositori ini berisi implementasi Tugas Besar mata kuliah **Pemrograman Fungsional (Semester 6)**, Program Studi Informatika, Fakultas Teknik, Universitas Muhammadiyah Malang (UMM).

**Dosen Pengampu:** Fera Putri Ayu Lestari, S.Kom., M.T.
### Tim Pengembang (Kelompok)
1. **Tricahyo Diqolbu** (NIM: 202310370311309)
2. **Natasya Salsabila** (NIM: 202310370311019)
3. **Senyiur Putri Hallinda** (NIM: 202310370311021)

### 🎯 Peran Saya dalam Proyek Ini
Di dalam proyek kelompok ini, saya (Tricahyo Diqolbu) bertanggung jawab sebagai **Lead Data Analyst / Data Engineer**, dengan fokus kontribusi utama pada:
1. **Arsitektur Pipeline Fungsional:** Merancang dan membangun alur pemrosesan data utama (*data pipeline*) yang mematuhi kaidah murni *Functional Programming*. Ini mencakup implementasi pola *Higher-Order Functions* (seperti *Closure* sebagai *factory function* untuk filter dinamis) dan *Decorator* untuk keperluan *profiling* performa.
2. **Pengembangan Smart Sentiment Algorithm:** Menciptakan fungsi pintar (*Pure Function*) yang tidak hanya bergantung pada *rating* numerik, melainkan mampu mendeteksi konteks emosi pengguna melalui kata kunci spesifik, sarkasme, dan emoji (*context-aware classification*).
3. **Data Visualization & Business Intelligence:** Mengubah struktur data mentah menjadi wawasan bisnis lintas departemen (IT, Keuangan, Operasional, Keamanan). Merancang dan membangun *Executive Dashboard* interaktif (Matplotlib & Seaborn) yang menyajikan metrik makro serta deteksi anomali finansial (risiko *Fraud* Fintech) secara komprehensif.
---

## 📌 Deskripsi Proyek
Proyek ini bertujuan untuk membangun *pipeline* analisis sentimen berbasis waktu (*Time-series*) terhadap ulasan pengguna aplikasi Gojek di Google Play Store. Analisis ini menggunakan pendekatan **Aspect-Based Sentiment Analysis** untuk mengklasifikasikan ulasan ke dalam 4 pilar isu bisnis:
1. Isu Teknis (Bug/Error)
2. Isu Harga (Tarif/Promo)
3. Isu Driver (Operasional)
4. Isu Fraud (Keamanan Finansial/Saldo)

Alih-alih menggunakan paradigma *Object-Oriented Programming* (OOP) atau prosedural biasa, seluruh arsitektur kode di dalam proyek ini dibangun menggunakan **Paradigma Pemrograman Fungsional (Functional Programming/FP) Murni** sesuai dengan kriteria dan capaian pembelajaran mata kuliah.

## 📊 Dataset
Dataset yang digunakan dalam proyek ini bersumber dari Kaggle:
* **Judul:** Gojek Playstore Reviews
* **Author:** Dewana Kretarta L
* **Tautan:** [Kaggle - Gojek Playstore Reviews](https://www.kaggle.com/datasets/dewanakretarta/gojek-playstore-reviews)

---

## 🧠 Implementasi Pemrograman Fungsional (Sesuai Kriteria Penilaian)

Proyek ini mendemonstrasikan kelima konsep utama FP yang diwajibkan dalam tugas besar:

### 1. Pure Function
Fungsi-fungsi dasar dirancang untuk tidak memiliki *side-effect* dan selalu mengembalikan output yang sama untuk input yang sama.
* `bersihkan_teks(teks)`: Memproses pembersihan teks *(lowercase & strip)*.
* `parsing_tanggal(str_date)`: Mengekstrak format bulan dan tahun dari *string* waktu.
* `klasifikasi_sentimen_cerdas(baris)`: Melabeli sentimen berdasarkan kombinasi skor bintang, deteksi *keyword* kritis (sarkasme/apresiasi), dan emoji.

### 2. Immutability & Method Chaining
Data mentah (`df`) tidak pernah ditimpa (mutasi). Transformasi data dieksekusi menggunakan *pipeline* deklaratif melalui metode `.copy()` dan `.assign()`.
```python
df_clean = (
    df.copy()
    .assign(
        content     = lambda x: x['content'].apply(bersihkan_teks),
        at          = lambda x: x['at'].apply(parsing_tanggal),
        score_label = lambda x: x.apply(klasifikasi_sentimen_cerdas, axis=1)
    )
)

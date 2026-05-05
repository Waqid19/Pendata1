# Klasifikasi Diabetes Menggunakan Gaussian Naive Bayes: Integrasi KNIME & Scikit-Learn

Laporan ini mendokumentasikan proses implementasi model pembelajaran mesin untuk memprediksi status diabetes pada pasien berdasarkan dataset **diabetes_2.csv**. Proyek ini menggabungkan kemudahan visual workflow dari **KNIME Analytics Platform** dengan fleksibilitas library **Scikit-Learn (Python)**.

## 1. Arsitektur Workflow
Workflow yang dibangun terdiri dari beberapa tahapan utama: Pre-processing, Data Partitioning, Modeling, dan Evaluation.

![Integrasi KNIME dan Python](NaivBayes/workflowDiabetes.png)

*Gambar: Alur kerja (workflow) lengkap di KNIME.*

## 2. Langkah-Langkah Implementasi

### A. Pre-processing Data
Sebelum masuk ke tahap pemodelan, data harus dibersihkan untuk memastikan kualitas prediksi:

1.  **Missing Value Handling**: Menggunakan teknik imputasi **Median** untuk tipe data *Integer* dan *Float*. Median dipilih karena lebih stabil terhadap pencilan (outlier) dibandingkan rata-rata.
![Integrasi KNIME dan Python](NaivBayes/MisngValueHandling.png)

*Gambar: Missing Value.*

2.  **Data Transformation**: Menggunakan node **Number to String** untuk mengubah kolom `Outcome` menjadi tipe data kategorikal (String). Fitur lainnya tetap dipertahankan dalam bentuk numerik agar sesuai dengan algoritma Gaussian.
![Integrasi KNIME dan Python](NaivBayes/DataPartitioning.png)

*Gambar: Data Transformation.*

### B. Data Partitioning
Data dibagi menggunakan node **Table Partitioner** dengan rasio **70% Training** dan **30% Testing**. Teknik sampling yang digunakan adalah **Stratified Sampling** pada kolom `Outcome` untuk menjaga keseimbangan proporsi kelas target.
![Integrasi KNIME dan Python](NaivBayes/DataPartitioning.png)

*Gambar: Data Partitioning.*

### C. Implementasi Gaussian Naive Bayes (Python)
Modeling dilakukan menggunakan library `sklearn.naive_bayes` melalui node **Python Script (legacy)**. Algoritma Gaussian Naive Bayes sangat cocok karena sebagian besar fitur medis dalam dataset ini bersifat kontinu.
![Integrasi KNIME dan Python](NaivBayes/PythonScript.png)

*Gambar: Python Script.*

**Cuplikan Kode Utama:**
```python
import pandas as pd
from sklearn.naive_bayes import GaussianNB

# Inisialisasi model sesuai standar API Scikit-Learn
model = GaussianNB()

# Melatih model menggunakan data training
model.fit(X_train, y_train)

# Melakukan prediksi pada data testing
y_pred = model.predict(X_test)
```

### D. Evaluasi Model
Evaluasi dilakukan menggunakan node Scorer dengan membandingkan nilai aktual pada kolom Outcome terhadap nilai Prediction (Outcome).

![Integrasi KNIME dan Python](NaivBayes/EvaluasiModel.png)

*Gambar: Evaluasi Model.*

### E. Hasil
Setelah melakukan langkah-langkah di atas maka di hasilkan Confusion Matrix seperti berikut
![Integrasi KNIME dan Python](NaivBayes/ConfusionMatrix.png)

*Gambar: Confusion Matrix.*

## 3. Kesimpulan
Melalui integrasi ini, kita dapat memanfaatkan kekuatan pemrosesan data KNIME yang terstruktur dan menerapkannya langsung ke fungsi API Scikit-Learn yang kuat. Penggunaan GaussianNB memberikan dasar yang kuat untuk analisis prediktif pada data kesehatan yang memiliki distribusi normal.
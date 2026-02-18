# Modelling
Modelling (Pemodelan) adalah tahap dalam proses analisis data (seperti CRISP-DM) di mana data yang sudah dipersiapkan digunakan untuk membangun model analitik atau machine learning guna menjawab tujuan bisnis.

Pada tahap ini, kita memilih teknik atau algoritma yang paling sesuai untuk menyelesaikan masalah.

## Tujuan Modelling
- Membuat model yang dapat memprediksi, mengklasifikasi, atau menemukan pola dalam data
- Menguji berbagai algoritma untuk mendapatkan hasil terbaik
- Mengoptimalkan performa model

## Langkah-Langkah dalam Modelling
1. Memilih Teknik/Algoritma
Pemilihan tergantung pada jenis masalah:
- Klasifikasi → Logistic Regression, Decision Tree, Random Forest, SVM
- Regresi → Linear Regression, Ridge, Lasso
- Clustering → K-Means, Hierarchical Clustering
- Prediksi deret waktu → ARIMA, LSTM

2. Membagi Data
Biasanya data dibagi menjadi:
- Training set → untuk melatih model
- Testing set → untuk menguji performa model
Kadang juga menggunakan:
- Validation set → untuk tuning parameter

3. Melatih Model (Training)
Model belajar dari data training untuk mengenali pola.

4. Evaluasi Model
Menggunakan metrik seperti:
- Accuracy (akurasi)
- Precision & Recall
- F1-Score
- RMSE / MAE (untuk regresi)
- Confusion Matrix

5. Optimasi Model
- Hyperparameter tuning
- ross-validation
- Feature selection
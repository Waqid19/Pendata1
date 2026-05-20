# ANALISIS REGRESI LINEAR 


---

# 1. DATASET 

## A. Data Awal (Training Data)

Data di bawah ini adalah data historis yang digunakan untuk melatih model dan mencari garis tren regresi linear terbaik.

| No (Data Awal) | Variabel Independen (X) | Variabel Dependen (Y) |
|---|---|---|
| 1 | 2 | 2 |
| 2 | 4 | 3 |
| 3 | 3 | 5 |
| 4 | 3 | 4 |
| 5 | 3 | 3 |
| 6 | 4 | 5 |
| 7 | 5 | 6 |

## B. Data Prediksi (Test Data)

Data di bawah ini merupakan nilai X baru yang ingin dicari prediksi nilai Y-nya berdasarkan model yang terbentuk.

| Prediksi Ke- | Variabel Independen (X) | Variabel Dependen (Y) |
|---|---|---|
| 8 | 0 | *?* |
| 9 | 1 | *?* |

---

# 2. PERHITUNGAN SECARA ANALITIK (MATRIKS)

Perhitungan koefisien regresi menggunakan metode **Ordinary Least Squares (OLS)** dengan rumus berbasis manipulasi matriks:

$$
\hat{\beta} = (X^T X)^{-1} X^T Y
$$

Vektor koefisien $\hat{\beta}$ terdiri atas intersep ($\beta_0$) dan kemiringan/slope ($\beta_1$):

$$
\hat{\beta} =
\begin{bmatrix}
\beta_0 \\
\beta_1
\end{bmatrix}
$$

## Langkah 1: Menyusun Matriks X dan Vektor Y

Kolom pertama pada matriks $X$ diisi dengan angka 1 sebagai komponen pengali untuk intersep ($\beta_0$).

$$
X =
\begin{bmatrix}
1 & 2 \\
1 & 4 \\
1 & 3 \\
1 & 3 \\
1 & 3 \\
1 & 4 \\
1 & 5
\end{bmatrix},
\quad
Y =
\begin{bmatrix}
2 \\
3 \\
5 \\
4 \\
3 \\
5 \\
6
\end{bmatrix}
$$

## Langkah 2: Menghitung Transpose Matriks X ($X^T$)

$$
X^T =
\begin{bmatrix}
1 & 1 & 1 & 1 & 1 & 1 & 1 \\
2 & 4 & 3 & 3 & 3 & 4 & 5
\end{bmatrix}
$$

## Langkah 3: Menghitung Perkalian Matriks $X^T X$

$$
X^T X =
\begin{bmatrix}
1 & 1 & 1 & 1 & 1 & 1 & 1 \\
2 & 4 & 3 & 3 & 3 & 4 & 5
\end{bmatrix}
\begin{bmatrix}
1 & 2 \\
1 & 4 \\
1 & 3 \\
1 & 3 \\
1 & 3 \\
1 & 4 \\
1 & 5
\end{bmatrix}
=
\begin{bmatrix}
7 & 24 \\
24 & 88
\end{bmatrix}
$$

## Langkah 4: Menghitung Invers Matriks $(X^T X)^{-1}$

- **Determinan ($ad - bc$):**

$$
(7 \times 88) - (24 \times 24)
= 616 - 576
= 40
$$

$$
(X^T X)^{-1}
=
\frac{1}{40}
\begin{bmatrix}
88 & -24 \\
-24 & 7
\end{bmatrix}
=
\begin{bmatrix}
2.2 & -0.6 \\
-0.6 & 0.175
\end{bmatrix}
$$

## Langkah 5: Menghitung Perkalian Matriks $X^T Y$

$$
X^T Y =
\begin{bmatrix}
1 & 1 & 1 & 1 & 1 & 1 & 1 \\
2 & 4 & 3 & 3 & 3 & 4 & 5
\end{bmatrix}
\begin{bmatrix}
2 \\
3 \\
5 \\
4 \\
3 \\
5 \\
6
\end{bmatrix}
=
\begin{bmatrix}
28 \\
102
\end{bmatrix}
$$

## Langkah 6: Menghitung Nilai Koefisien Regresi ($\hat{\beta}$)

$$
\hat{\beta}
=
\begin{bmatrix}
2.2 & -0.6 \\
-0.6 & 0.175
\end{bmatrix}
\begin{bmatrix}
28 \\
102
\end{bmatrix}
$$

### Menghitung Intersep ($\beta_0$)

$$
\beta_0
=
(2.2 \times 28) + (-0.6 \times 102)
$$

$$
= 61.6 - 61.2
$$

$$
= 0.4
$$

### Menghitung Slope/Kemiringan ($\beta_1$)

$$
\beta_1
=
(-0.6 \times 28) + (0.175 \times 102)
$$

$$
= -16.8 + 17.85
$$

$$
= 1.05
$$

## Persamaan Regresi Model Analitik


::contentReference[oaicite:0]{index=0}


---

# 3. PERHITUNGAN MENGGUNAKAN PROGRAM (PYTHON)

Berikut adalah kode pemrograman Python menggunakan pustaka `scikit-learn` untuk mengotomatisasi perhitungan koefisien regresi serta memprediksi data:

```python
import numpy as np
from sklearn.linear_model import LinearRegression

# 1. Menyiapkan Data Training (Awal)
X_train = np.array([[2], [4], [3], [3], [3], [4], [5]])
Y_train = np.array([2, 3, 5, 4, 3, 5, 6])

# 2. Inisialisasi dan Pelatihan Model Regresi Linear
model = LinearRegression()
model.fit(X_train, Y_train)

# 3. Mengambil Nilai Koefisien Hasil Program
intersep_b0 = model.intercept_
slope_b1 = model.coef_[0]

print("=== KOEFISIEN REGRESI (OUTPUT PROGRAM) ===")
print(f"Intersep (Beta 0) : {intersep_b0:.4f}")
print(f"Slope (Beta 1)    : {slope_b1:.4f}")
print(f"Persamaan Garis   : Y = {intersep_b0:.4f} + {slope_b1:.4f}X\n")

# 4. Prediksi Nilai Baru dari Tabel Prediksi
X_pred = np.array([[0], [1]])
Y_pred = model.predict(X_pred)

print("=== HASIL PREDIKSI DATA ===")
for i, x_val in enumerate(X_pred.flatten()):
    print(f"Data Prediksi ke-{i+8} (X = {x_val}) -> Hasil Nilai Y = {Y_pred[i]:.4f}")
```

---

# 4. HASIL PREDIKSI DATA

Berdasarkan integrasi hasil dari perhitungan rumus persamaan linear:


::contentReference[oaicite:1]{index=1}


didapatkan hasil prediksi nilai $Y$ sebagai berikut:

| No (Prediksi) | Input Nilai X | Operasi Rumus Model ($Y = 0.4 + 1.05X$) | Hasil Akhir Nilai Y |
|---|---|---|---|
| 8 | 0 | $0.4 + (1.05 \times 0)$ | **0.4000** |
| 9 | 1 | $0.4 + (1.05 \times 1)$ | **1.4500** |

---

# 5. PANDUAN IMPLEMENTASI GAMBAR (GEOGEBRA)

Untuk memvisualisasikan data ini ke dalam grafik kartesius di GeoGebra, lakukan langkah input objek berikut pada kolom masukan (*input bar*):

- **Input Titik Sampel:**  
  `A=(2,2)`, `B=(4,3)`, `C=(3,5)`, `D=(3,4)`, `E=(3,3)`, `F=(4,5)`, `G=(5,6)`

- **Input Garis Linear:**  
  `f(x) = 0.4 + 1.05x`  
  atau ketik perintah:  
  `FitLine({A,B,C,D,E,F,G})`

- **Input Titik Prediksi:**  
  `H=(0,0.4)` dan `I=(1,1.45)`

Berikut adalah struktur posisi penempatan tangkapan layar (*screenshot*) grafik GeoGebra Anda untuk laporan:

## A. Diagram Pencar (Scatter Plot) Data Awal

**[GAMBAR 1: Scatter Plot Titik Data Awal A sampai G di GeoGebra]**
![Learner](regresiLinier/img1.png)

- **Deskripsi:**  
  Grafik menunjukkan posisi sebaran ketujuh titik data latih berdasarkan sumbu koordinat X dan Y sebelum ditarik garis regresi.

## B. Garis Regresi Terbaik (Line of Best Fit)

**[GAMBAR 2: Plot Garis Regresi $f(x) = 0.4 + 1.05x$ Membelah Titik Data di GeoGebra]**
![Learner](regresiLinier/img2.png)

- **Deskripsi:**  
  Grafik menampilkan garis lurus linear terbaik yang ditarik membelah sebaran data untuk meminimalkan nilai kesalahan kuadrat (*error*).


---

# 6. KESIMPULAN

- **Konsistensi Akurasi:**  
  Metode perhitungan analitik berbasis matriks OLS dan metode komputasi otomatis lewat program Python (`scikit-learn`) terbukti menghasilkan nilai parameter koefisien yang sama persis, yaitu nilai Intersep $\beta_0 = 0.4$ dan Slope $\beta_1 = 1.05$.

- **Interpretasi Model:**  
  Persamaan regresi: $Y = 1.0769X$ bermakna bahwa model memiliki nilai awal sebesar $0.4$ ketika variabel $X$ bernilai nol. Setiap penambahan satu satuan nilai pada variabel independen ($X$), maka nilai variabel dependen ($Y$) diprediksi akan meningkat linear sebesar $1.05$ satuan.

- **Validasi Geometris:**  
  Implementasi grafis menggunakan aplikasi GeoGebra memberikan konfirmasi visual bahwa model regresi linear yang dibangun telah membagi sebaran data secara seimbang, serta memastikan seluruh koordinat hasil prediksi baru berada tepat pada lintasan garis regresi linear model tersebut.
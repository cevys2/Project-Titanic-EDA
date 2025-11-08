# Analisis Data Eksploratif (EDA) Dataset Titanic

## Ringkasan Proyek
Proyek ini adalah Analisis Data Eksploratif (EDA) pada dataset Titanic. Tujuannya adalah untuk memahami data penumpang dan menemukan faktor-faktor kunci yang paling memengaruhi tingkat keselamatan (apakah seseorang selamat atau tidak).

Analisis ini dilakukan sepenuhnya di Python, menggunakan library **Pandas** untuk manipulasi data dan **Matplotlib/Seaborn** untuk visualisasi.

![Screenshot Grafik Titanic](./titanic-charts.png)

---

## Tools yang Digunakan
* **Python**
* **Pandas** (untuk pembersihan dan analisis data)
* **Matplotlib & Seaborn** (untuk visualisasi data)

---

## Proses Analisis
Alur kerja proyek ini mencakup empat tahap utama:

1.  **Data Loading & Inspection:** Memuat file `train.csv` ke DataFrame. Inspeksi awal menggunakan `.info()` dan `.describe()` untuk memahami struktur dan tipe data.

2.  **Data Quality & Cleaning (Menangani Caveat):**
    * **Kolom `Age`:** Ditemukan **177 nilai hilang**. Nilai yang hilang ini ditangani menggunakan "mean imputation" (diisi dengan nilai rata-rata umur) agar data tetap bisa digunakan untuk analisis.
    * **Kolom `Cabin`:** Ditemukan **687 nilai hilang** (77% data kosong). Karena terlalu banyak data yang hilang, kolom ini tidak digunakan dalam analisis `groupby` utama.
    * **Kolom `Embarked`:** Ditemukan 2 nilai hilang, yang diabaikan karena jumlahnya tidak signifikan.

3.  **Feature Engineering:**
    * Membuat kolom `AgeGroup` (Anak-anak, Remaja, Dewasa, Lansia) dari data `Age` yang sudah bersih.
    * Membuat kolom `FamilySize` dengan menjumlahkan `SibSp` dan `Parch` untuk menganalisis dampak bepergian sendiri vs. bersama keluarga.

4.  **Analysis & Visualization:** Menggunakan `groupby` dan `value_counts` untuk menemukan pola, serta `seaborn` untuk memvisualisasikan temuan tersebut.

---

## Temuan Utama & Insight
Analisis ini mengungkap beberapa faktor kunci yang sangat memengaruhi tingkat keselamatan:

### 1. Faktor Jenis Kelamin (`Sex`)
Faktor ini memiliki dampak paling signifikan. Analisis menunjukkan bahwa sekitar **74% penumpang perempuan selamat**, dibandingkan dengan hanya **19% penumpang laki-laki**.

### 2. Faktor Status Sosial-Ekonomi (`Pclass`, `Fare`, & `Cabin`)
Status sosial-ekonomi adalah prediktor kuat kedua:
* Penumpang **Kelas 1 (`Pclass` 1)** memiliki tingkat keselamatan **~63%**.
* Penumpang **Kelas 3 (`Pclass` 3)** memiliki tingkat keselamatan terendah, yaitu hanya **~24%**.

*Insight* ini lebih dalam dari sekadar "kelas sosial". Data ini sangat terkait dengan **`Fare` (Harga Tiket)** dan **`Cabin` (Lokasi Kabin)**:
* Penumpang Kelas 1 membayar tarif termahal, yang memberi mereka kabin di **dek atas (upper decks)**.
* Penumpang Kelas 3 membayar tarif termurah dan ditempatkan di **dek bawah (lower decks)**.
* Saat evakuasi, penumpang di dek atas memiliki akses yang jauh lebih cepat dan mudah ke sekoci di dek kapal bagian atas, sementara penumpang di dek bawah terjebak dan lebih jauh dari lokasi penyelamatan.

### 3. Faktor Kelompok Umur (`AgeGroup`)
**Anak-anak (0-12 tahun) memiliki tingkat selamat tertinggi (~58%)**. Ini mendukung hipotesis "wanita dan anak-anak dulu". Tingkat keselamatan kemudian menurun seiring bertambahnya usia, dengan Lansia (60+) memiliki peluang terendah (~23%).

### 4. Faktor Ukuran Keluarga (`FamilySize`)
Peluang selamat tertinggi dimiliki oleh mereka yang bepergian dengan **keluarga kecil (1-3 orang)**. Bepergian sendirian (30% selamat) atau dengan keluarga yang sangat besar (0-20% selamat) ternyata jauh lebih berbahaya.

---

## Notebook Proyek
Untuk melihat kode lengkap, analisis, dan semua visualisasi, silakan buka file Jupyter Notebook di repositori ini:

[**Proyek_Titanic_Visual.ipynb**](./Proyek_Titanic_Visual.ipynb)

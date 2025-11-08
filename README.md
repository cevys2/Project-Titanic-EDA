# Analisis Data Eksploratif (EDA) Dataset Titanic

## Ringkasan Proyek
Proyek ini adalah Analisis Data Eksploratif (EDA) pada dataset Titanic. Tujuannya adalah untuk memahami data penumpang dan menemukan faktor-faktor kunci yang paling memengaruhi tingkat keselamatan (apakah seseorang selamat atau tidak).

Analisis ini dilakukan sepenuhnya di Python, menggunakan library **Pandas** untuk manipulasi data dan **Matplotlib/Seaborn** untuk visualisasi.

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
    * **Kolom `Age`:** Ditemukan **177 nilai hilang**. Nilai yang hilang ini ditangani menggunakan "mean imputation" (diisi dengan nilai rata-rata umur).
    * **Kolom `Cabin`:** Ditemukan **687 nilai hilang** (77% data kosong). Kolom ini diabaikan untuk analisis utama karena terlalu banyak data yang hilang.
3.  **Feature Engineering:**
    * Membuat kolom `AgeGroup` (Anak-anak, Remaja, Dewasa, Lansia) dari data `Age` yang sudah bersih.
    * Membuat kolom `FamilySize` dengan menjumlahkan `SibSp` dan `Parch`.
4.  **Analysis & Visualization:** Menggunakan `groupby` dan `value_counts` untuk menemukan pola, serta `seaborn` untuk memvisualisasikan temuan tersebut.

---

## Temuan Utama & Visualisasi
Analisis ini mengungkap beberapa faktor kunci yang sangat memengaruhi tingkat keselamatan:

| Faktor Utama | Temuan |
| :--- | :--- |
| **1. Jenis Kelamin (`Sex`)** | Faktor ini memiliki dampak paling signifikan. Sekitar **74% penumpang perempuan selamat**, dibandingkan dengan hanya **19% penumpang laki-laki**. |
| **2. Kelas Sosial (`Pclass`)** | Status sosial-ekonomi adalah prediktor kuat. Penumpang **Kelas 1 (`Pclass` 1)** memiliki tingkat keselamatan **~63%**, sedangkan penumpang **Kelas 3 (`Pclass` 3)** hanya memiliki **~24%**. Ini sangat terkait dengan lokasi kabin di dek atas (Kelas 1) vs. dek bawah (Kelas 3). |

<table width="100%">
  <tr>
    <td width="50%"><img src="chart_sex.png" alt="Grafik Sex vs Survived"></td>
    <td width="50%"><img src="chart_pclass.png" alt="Grafik Pclass vs Survived"></td>
  </tr>
  <tr>
    <td width="50%"><img src="chart_agegroup.png" alt="Grafik AgeGroup vs Survived"></td>
    <td width="50%"><img src="chart_distribution.png" alt="Grafik Distribusi Survived"></td>
  </tr>
</table>

| Faktor Lain | Temuan |
| :--- | :--- |
| **3. Kelompok Umur (`AgeGroup`)** | **Anak-anak (0-12 tahun) memiliki tingkat selamat tertinggi (~58%)**. Ini mendukung hipotesis "wanita dan anak-anak dulu". Tingkat selamat kemudian menurun seiring bertambahnya usia. |
| **4. Ukuran Keluarga (`FamilySize`)** | Bepergian sendirian (30% selamat) atau dengan keluarga yang sangat besar (0-20% selamat) adalah yang paling berbahaya. Peluang selamat tertinggi dimiliki oleh mereka yang bepergian dengan **keluarga kecil (1-3 orang)**. |

---

## Cara Menggunakan File Ini
* **`Proyek_Titanic_Visual.ipynb`**: Ini adalah file Jupyter Notebook utama. Buka file ini untuk melihat semua kode, analisis, dan visualisasi.
* **`train.csv`**: Ini adalah data mentah yang digunakan oleh notebook di atas. Anda harus memilikinya di folder yang sama agar kode bisa berjalan.
* **File `.png`**: Ini adalah gambar-gambar yang digunakan untuk menampilkan visualisasi di file README ini.

---

## Notebook Proyek
Untuk melihat kode lengkap, analisis, dan semua visualisasi, silakan buka file Jupyter Notebook di repositori ini:

[**Proyek_Titanic_Visual.ipynb**](./Proyek_Titanic_Visual.ipynb)

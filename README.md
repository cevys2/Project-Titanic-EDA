# Analisis Data Eksploratif (EDA) Dataset Titanic

## Ringkasan Proyek
Proyek ini adalah Analisis Data Eksploratif (EDA) pada dataset Titanic. Tujuannya adalah untuk memahami data penumpang dan menemukan faktor-faktor kunci yang paling memengaruhi tingkat keselamatan (apakah seseorang selamat atau tidak).

Analisis ini dilakukan sepenuhnya di Python, menggunakan library **Pandas** untuk manipulasi data dan **Matplotlib/Seaborn** untuk visualisasi.

---

## Tools yang Digunakan
* **Python** (Bahasa Pemrograman Utama)
* **Jupyter Notebook** (Lingkungan Pengembangan Interaktif)
* **Pandas** (Untuk memuat, membersihkan, dan menganalisis data)
* **Matplotlib & Seaborn** (Untuk visualisasi data)

---

## Cara Menjalankan Proyek Ini
1.  Pastikan Anda memiliki **Anaconda** (yang menyertakan Python, Pandas, dan Jupyter Notebook) terinstal di komputer Anda.
2.  Unduh (atau *clone*) repositori ini ke komputer Anda.
3.  Pastikan file notebook (`Proyek_Titanic_Visual.ipynb`) dan file data (`train.csv`) berada di dalam folder yang sama.
4.  Buka Jupyter Notebook dari Anaconda Navigator, navigasikan ke folder proyek, dan buka file `.ipynb` tersebut.
5.  Anda bisa menjalankan semua sel (`Cell` -> `Run All`) untuk melihat semua analisis dan visualisasi.

---

## Dataset & Data Dictionary
Dataset yang digunakan adalah `train.csv`, yang berisi data detail dari 891 penumpang. Kolom-kolom kunci yang dianalisis adalah:

* **`Survived`**: Faktor utama. **0** = Tidak Selamat, **1** = Selamat.
* **`Pclass`**: Kelas tiket (proksi untuk status sosial-ekonomi). **1** = Kelas 1 (Atas), **2** = Kelas 2 (Menengah), **3** = Kelas 3 (Bawah).
* **`Sex`**: Jenis kelamin (`male`, `female`).
* **`Age`**: Usia penumpang (dalam tahun).
* **`SibSp`**: Jumlah saudara kandung (siblings) / pasangan (spouses) yang ikut berlayar.
* **`Parch`**: Jumlah orang tua (parents) / anak (children) yang ikut berlayar.
* **`Fare`**: Harga tiket yang dibayar penumpang.
* **`Cabin`**: Nomor kabin penumpang.
* **`Embarked`**: Pelabuhan keberangkatan (C = Cherbourg, Q = Queenstown, S = Southampton).

---

## Alur Kerja Analisis (Workflow)
Proyek ini mengikuti alur kerja analisis data standar:

1.  **Inspeksi Data:** Memuat data dan menggunakan `.info()` & `.describe()`.
2.  **Identifikasi Masalah (Caveat):** Menemukan bahwa kolom `Age` memiliki 177 data hilang dan `Cabin` memiliki 687 data hilang.
3.  **Pembersihan Data:** Mengisi nilai `Age` yang hilang menggunakan nilai rata-rata (*mean imputation*). Kolom `Cabin` diabaikan karena terlalu banyak data yang hilang.
4.  **Feature Engineering:** Membuat kolom baru untuk analisis yang lebih dalam:
    * `AgeGroup`: Mengelompokkan `Age` ke dalam kategori (Anak-anak, Remaja, Dewasa, Lansia).
    * `FamilySize`: Menjumlahkan `SibSp` dan `Parch` untuk melihat dampak bepergian sendiri vs. berkelompok.
5.  **Analisis & Visualisasi:** Menggunakan `.groupby()` dan `.value_counts()` untuk menemukan pola, dan `Seaborn` untuk memvisualisasikan setiap temuan kunci.

---

## Temuan Utama & Visualisasi
Analisis ini mengungkap beberapa faktor kunci yang sangat memengaruhi tingkat keselamatan:

<table width="100%">
  <tr>
    <td width="50%" align="center">
      <strong>Distribusi Keselamatan</strong><br>
      <img src="chart_distribution.png" alt="Grafik Distribusi Survived" width="95%">
    </td>
    <td width="50%" align="center">
      <strong>Keselamatan berdasarkan Jenis Kelamin</strong><br>
      <img src="chart_sex.png" alt="Grafik Sex vs Survived" width="95%">
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <strong>Keselamatan berdasarkan Kelas Sosial</strong><br>
      <img src="chart_pclass.png" alt="Grafik Pclass vs Survived" width="95%">
    </td>
    <td width="50%" align="center">
      <strong>Keselamatan berdasarkan Kelompok Umur</strong><br>
      <img src="chart_agegroup.png" alt="Grafik AgeGroup vs Survived" width="95%">
    </td>
  </tr>
</table>

### Rangkuman Insight:
* **Jenis Kelamin (`Sex`):** Faktor ini memiliki dampak paling signifikan. Sekitar **74% penumpang perempuan selamat**, dibandingkan dengan hanya **19% penumpang laki-laki**.
* **Kelas Sosial (`Pclass`):** Status sosial-ekonomi adalah prediktor kuat. Penumpang **Kelas 1 (`Pclass` 1)** memiliki tingkat keselamatan **~63%**, sedangkan penumpang **Kelas 3 (`Pclass` 3)** hanya memiliki **~24%**. Ini sangat terkait dengan lokasi kabin di dek atas (Kelas 1) vs. dek bawah (Kelas 3).
* **Kelompok Umur (`AgeGroup`):** **Anak-anak (0-12 tahun) memiliki tingkat selamat tertinggi (~58%)**. Ini mendukung hipotesis "wanita dan anak-anak dulu". Tingkat selamat kemudian menurun seiring bertambahnya usia, dengan Lansia (60+) memiliki peluang terendah (~23%).
* **Ukuran Keluarga (`FamilySize`):** Bepergian sendirian (30% selamat) atau dengan keluarga yang sangat besar (0-20% selamat) adalah yang paling berbahaya. Peluang selamat tertinggi dimiliki oleh mereka yang bepergian dengan **keluarga kecil (1-3 orang)**.

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
3.  **Pembersihan Data:** Mengisi nilai `Age` yang hilang menggunakan nilai rata-rata (*mean imputation*). Kolom `Cabin` diabaikan untuk analisis *kuantitatif* karena terlalu banyak data yang hilang.
4.  **Feature Engineering:**
    * Membuat kolom `AgeGroup` (Anak-anak, Remaja, Dewasa, Lansia) dari data `Age` yang sudah bersih.
    * Membuat kolom `FamilySize` dengan menjumlahkan `SibSp` dan `Parch`.
5.  **Analisis & Visualisasi:** Menggunakan `.groupby()` dan `Seaborn` untuk menemukan dan memvisualisasikan setiap temuan kunci.

---

## Temuan Utama & Visualisasi
Analisis ini menceritakan sebuah kisah yang jelas tentang siapa yang selamat dan siapa yang tidak. Temuan-temuan ini tidak terpisah, melainkan saling terkait.

<table width="100%">
  <tr>
    <td width="50%" align="center">
      <strong>Keselamatan berdasarkan Jenis Kelamin</strong><br>
      <img src="chart_sex.png" alt="Grafik Sex vs Survived" width="95%">
    </td>
    <td width="50%" align="center">
      <strong>Keselamatan berdasarkan Kelas Sosial</strong><br>
      <img src="chart_pclass.png" alt="Grafik Pclass vs Survived" width="95%">
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <strong>Keselamatan berdasarkan Kelompok Umur</strong><br>
      <img src="chart_agegroup.png" alt="Grafik AgeGroup vs Survived" width="95%">
    </td>
    <td width="50%" align="center">
      <strong>Distribusi Keselamatan</strong><br>
      <img src="chart_distribution.png" alt="Grafik Distribusi Survived" width="95%">
    </td>
  </tr>
</table>

### Rangkuman Insight: Sebuah Cerita dari Data

#### 1. "Wanita dan Anak-anak Dulu" ... Tapi Bersyarat
Frasa terkenal "wanita dan anak-anak dulu" terlihat sangat jelas dalam data. Analisis demografi menunjukkan:
* **Jenis Kelamin (`Sex`):** Menjadi perempuan adalah faktor keselamatan terbesar. Sekitar **74% penumpang perempuan selamat**, sementara hanya **19% penumpang laki-laki** yang berhasil.
* **Umur (`AgeGroup`):** Menjadi muda juga merupakan keuntungan besar. **Anak-anak (0-12 tahun)** memiliki tingkat selamat **~58%**, yang tertinggi dari semua kelompok umur. Sebaliknya, Lansia (60+) memiliki peluang terendah (~23%).

#### 2. Faktor Kekayaan (`Pclass`, `Fare`, & `Cabin`)
Namun, "wanita dan anak-anak dulu" tidak berlaku sama untuk semua orang. Faktor status sosial-ekonomi (yang diwakili oleh `Pclass`) adalah pembeda yang kejam:
* Penumpang **Kelas 1 (`Pclass` 1)** memiliki tingkat keselamatan **~63%**.
* Penumpang **Kelas 3 (`Pclass` 3)**, yang merupakan kelompok terbesar di kapal, hanya memiliki peluang selamat **~24%**.

*Insight* ini lebih dalam dari sekadar "kelas sosial". Data ini sangat terkait dengan **`Fare` (Harga Tiket)** dan **`Cabin` (Lokasi Kabin)**. Penumpang Kelas 1 membayar tarif termahal, yang memberi mereka kabin di **dek atas (A, B, C, D)**. Penumpang Kelas 3 ditempatkan di **dek bawah (E, F, G)**. Saat evakuasi, mereka yang berada di dek atas memiliki akses yang jauh lebih cepat dan mudah ke sekoci, sementara mereka yang berada di dek bawah terjebak.

#### 3. Hubungan Antar Faktor: Siapa yang Paling Aman?
Ketika kita menggabungkan temuan di atas, ceritanya menjadi sangat jelas:
* **Kelompok Paling Aman:** Perempuan di Kelas 1 & 2 (>90% selamat).
* **Kelompok Paling Berisiko:** Laki-laki di Kelas 2 & 3 (~13-15% selamat).
* Menariknya, analisis gabungan menunjukkan bahwa seorang **perempuan di Kelas 3 (50% selamat)** memiliki peluang selamat yang lebih baik daripada seorang **laki-laki di Kelas 1 (37% selamat)**.

#### 4. Faktor Ukuran Keluarga (`FamilySize`)
Terakhir, data menunjukkan bahwa bepergian dalam kelompok kecil itu ideal.
* Peluang selamat tertinggi dimiliki oleh mereka yang bepergian dengan **keluarga kecil (1-3 orang)**.
* Bepergian **sendirian (30% selamat)** atau dengan **keluarga yang sangat besar (0-20% selamat)** ternyata jauh lebih berbahaya, kemungkinan karena sulit untuk mengoordinasikan evakuasi.

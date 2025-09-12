# PRAKTIKUM 2: SELEKSI DATA

## 2.1. TUJUAN DAN INDIKATOR CAPAIAN

Setelah menyelesaikan praktikum ini mahasiswa diharapkan:

1. Mampu memahami konsep dasar selection (seleksi data).
2. Mampu memahami proses dalam seleksi data.
3. Mampu melakukan proses data seleksi pada studi kasus menggunakan python.

Indikator ketercapaian diukur dengan:

1. Mahasiswa memahami dan menerapkan konsep data selection pada studi kasus.
2. Mahasiswa mampu menghasilkan data selection pada studi kasus menggunakan python.

## 2.2. TEORI PENDUKUNG

Seleksi data menurut Han dan Kamber (2006) Data yang terdapat dalam database datawarehouse kemudian direduksi dengan berbagai teknik. Proses reduksi diperlukan untuk mendapatkan hasil yang lebih akurat dan mengurangi waktu komputasi terutama untuk masalah dengan skala besar (large scale problem)

Beberapa cara seleksi, antara lain:

1. Sampling, adalah seleksi subset reprensentative dari populasi data yang besar.
2. Denoising adalah proses menghilangkan noise dari data yang akan ditransformasikan.
3. Feature extraction, adalah proses membuka spesifikasi data yang signifikan dalam konteks tertentu.

## 2.3. ALAT DAN BAHAN

Alat dan bahan yang digunakan dalam praktikum ini yaitu:

1. Komputer
2. vs code
3. Dataset

## 2.4. LANGKAH PRAKTIKUM

ikuti langkah praktikum berikut ini:

1.  Jika akan dilakukan analisis data mining menggunakan Data Alumni untuk mengetahui hubungan antra Tempat Tanggal Lahir, Tahun masuk, Tahun lulus, Status pekerjaan, Lama masa tunggu, Nilai TOEFL, dan IPK. Maka lakukanlah analisis Data Alumni untuk kemudian dilakukan proses seleksi data.
2.  Buka dataset alumni dengan nama _Data Alumni.xlxs_.
3.  Perhatikan record-record pada tabel tersebut.
4.  Lakukan proses seleksi data menggunakan Jupyter Notebook.

**Seleksi data "Sampling"**
Menampilkan data pada kolom NIM dan TTL.

```python
df.loc[:, ["NIM", "TTL"]]
```

**Seleksi data "Feature Extraction"**

a. Mencari umur

untuk mencari umur, kita bisa menggunakan kolom TTL/Tempat dan tanggal Lahir. Dari kolom TLL, kita akan mengambil nilai tahun atau 4 karakter dari belakang. Kemudian kita akan hitung dengan menggunakan rumus, Tahun sekarang dikurangi dengan tahun lahir.

- mengambil 4 karakter terakhir dari kolom TTL, dan memasukkan ke dalam kolom baru Tahun Lahir.

```python
for index, row in df.iterrows():
    df.loc[index, "Tahun Lahir"] = row["TTL"][-4:]
df
```

- setelah tahun lahir didapatkan, langkah berikutnya adalah mencari tahun sekarang, kemudian mengurangi tahun sekarang dengan tahun lahir untuk mendapatkan umur.

```python
from datetime import date
now = datetime.now()

now.year
for index, row in df.iterrows():
    df.loc[index, "Umur"] = now.year - int(row["Tahun Lahir"])
df
```

b. Mencari Masa Studi

Untuk mencari masa studi yaitu didapatkan dari tahun lulus dikurangi dengan tahun masuk.

```python
for index, row in df.iterrows():
    df.loc[index, "Masa Studi"] = int(row["Tahun Lulus"]) - int(row["Tahun Masuk"])

```

c. Untuk seleksi data denoising sama dengan sampling.

d. Sebutkan data-data yang diseleksi, mengapa dan berikan penjelasannya!

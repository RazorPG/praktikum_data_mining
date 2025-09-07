# PRAKTIKUM 1: IMPORT DATA DAN PEMBERSIHAN DATA

## 1.1. TUJUAN DAN INDIKATOR CAPAIAN

Setelah menyelesaikan praktikum ini mahasiswa diharapkan:

1. Mahasiswa mampu menjelaskan pengertian data mining.
2. Mahasiswa mampu melakukan proses import data dan pembersihan data.

Indikator ketercapaian diukur dengan:

1. Import data untuk data mining dapat dilakukan dengan baik.
2. Dapat melakukan pembersihan data pada dataset yang diperoleh sebelumnya.

## 1.2. TEORI PENDUKUNG

Saat memulai suatu proyek tentang data science, kemungkinan besar kita akan sering mengambil data melalui web scrapping, dan tidak menutup kemungkinan juga mengambil data dari kumpulan data yang di unduh dari tempat lain, seperti Kaggle, Quandl, dll. Data tersebut mungkin dalam format file Excel atau disimpan dalam extensi .csv.

### **Pembersihan Data**

Menurut Han dan Kamber (2006) Proses Cleaning dan pembersihan data adalah sebagai berikut: Pembersihan data dan (cleaning) merupakan Proses yang digunakan untuk membuang data yang tidak konsisten dan bersifat noise dari data yang terdapat di berbagai basis data yang mungkin berbeda format maupun platform yang kemudian diintegrasikan dalam satu database datawarehouse. Garbage in garbage out (hanya sampah yang akan dihasilkan bila dimasukkan juga sampah) merupakan istilah yang sering dipakai untuk menggambarkan tahap ini. Pembersihan data juga akan mempengaruhi formasi dari sistem data mining karena data yang ditangani akan berkurang jumlah dan kompleksitasnya.

## 1.3. ALAT DAN BAHAN

Alat dan bahan yang digunakan dalam praktikum ini yaitu:

1. Komputer
2. vs code
3. Dataset

## 1.4. LANGKAH PRAKTIKUM

ikuti langkah praktikum berikut ini:

1.  Lakukan analisis data mining menggunakan Data Alumni untuk dilakukan proses import data.
2.  Buka dataset alumni dengan nama _Data Alumni.xlxs_.
3.  Perhatikan record-record pada tabel tersebut.
4.  Lakukan langkah berikut:

    - Membuka vs code Jupyter Notebook.
    - Import library yang akan digunakan.

      ```python
      from openpyxl import load_workbook
      import pandas as dm
      ```

      a. _openpyxl_: library yang digunakan untuk read dan write file Excel

      b. _pandas_: library data analysis, untuk mengolah data secara terstruktur

    - Inisialisasi file excel yang akan di import.

      ```python
      wb = load_workbook(filename="D:\Studied_at_UNP\SEMESTER-5\praktikum_data_mining\praktikum_1\Data Alumni.xlsx")
      sheet_ranges = wb['Sheet1']
      df = dm.DataFrame(sheet_ranges.values)
      df
      ```

      a. _*load_workbook*_ : nama function dari library openpyxl yang digunakan melakukan import data dari excel (kemudian disimpan dalam variabel wb)

      b. _*sheet_ranges*_ : variable yang menampung data dari sheet mana yang akan diambil dalam file excel (pada contoh ini adalah Sheet1).

      c. _DataFrame_ : adalah function dari library pandas yang digunakan untuk melakukan parsing data terstruktur kedalam bentuk kolom dan baris, dengan demikian data yang telah diparsing akan menjadi sebuah table yang nampak seperti susunan pada relational database, dimana sebuah baris tunggal mewakili sebuah contoh tunggal dan kolom mewakili atribut tertentu. (Kemudian dimasukkan ke dalam variabel df).

    - Setting data ke dalam template.

      ```python
      d = df[1:9][[1, 2, 3, 4, 5, 6, 7, 8]]
      d.columns = ["NIM", "TTL", "IPK", "Lama Waktu Tunggu", "Tahun Masuk", "Tahun Lulus", "Gaji", "TOEFL"]
      d
      ```

      a. _d = df[1:9][1,3,6,7,4,2,5,8]]_ : digunakan untuk memasukkan dataframe df kedalam variable d

      b. _columns_ : function dari library pandas

    - Menampilkan data pada kolom TTL
      ```python
      d['TTL']
      ```
    - Menampilkan data pada kolom TTL dengan bentuk tabel
      ```python
      d[['TTL']]
      ```
    - Menampilkan data dengan jumlah tertentu
      ```python
      d[:3]
      ```
    - Menampilkan data secara ascending atau descending berdasarkan kolom TTL
      ```python
      d.sort_values(['TTL'], ascending=[1])
      ```

### **PEMBERSIHAN DATA**

ikuti langkah praktikum berikut ini:

1. Jika akan dilakukan analisis data mining dengan menghapus data yang kosong pada atributUmur, IPK, Toefl, lama studi, gaji pertama bekerja dan lama masa tunggu mencari kerja. Makalakukanlah analisis data siswa untuk kemudian dilakukan proses pembersihan data. Datakosong pada dataframe biasanya ditampilkan dengan None. None adalah objek tunggal Pythonyang sering digunakan untuk mewakili data yang hilang pada Python. NA adalah istilah yangdigunakan untuk data hilang
2. Buka data set siswa dengan nama Data Alumni.xlxs
3. Perhatikan record-record pada tabel tersebut
4. Lakukan pembersihan data menggunakan
   ```python
   d = d.dropna(axis=0, how'any')
   d
   ```
   - _dropna()_ : akan menghapus semua baris di mana ada (any) nilai null. sebagai alternatif, kitadapat menurunkan nilai NA sepanjang sumbu yang berbeda,
   - _axis = 0_ : digunakan untuk menghapus semua baris yang mengandung nilai null.Hasil :
     | NIM | TTL | IPK | Lama Waktu Tunggu | Tahun Masuk | Tahun Lulus | Gaji | TOEFL |
     |----------|----------------------------|------|------------------|-------------|-------------|---------|-------|
     | 9018263 | Tapuih, 4 November 1989 | 2.13 | 2.4 | 2009 | 2016 | 2000000 | 390 |
     | 9018269 | Koto Anau, 19 Desember 1990| 2.75 | 2.4 | 2009 | 2016 | 2000000 | 413 |
     | 9020026 | Lampung, 27 Maret 1992 | 3.24 | 2.4 | 2009 | 2016 | 2000000 | 400 |
     | 12018060 | Padang, 23 Maret 1994 | 3.37 | 2.4 | 2012 | 2016 | 2000000 | 396 |
     | 11018022 | Jakarta, 22 Juni 1993 | 3.2 | 2.4 | 2011 | 2016 | 2000000 | 460 |
     | 9018212 | Pekanbaru, 3 Juni 1991 | 3.24 | 0 | 2009 | 2016 | 1200000 | 403 |
     | 9018301 | Purbalingga, 08 Oktober 1991| 3.06 | 2.4 | 2009 | 2016 | 2000000 | 450 |
     | 12022020 | Bukittinggi, 29 Maret 1992 | 3.47 | 2.4 | 2012 | 2016 | 1500000 | 423 |

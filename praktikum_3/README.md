# PRAKTIKUM 3: TRANSFORMASI DATA

## 3.1. TUJUAN DAN INDIKATOR CAPAIAN

Setelah menyelesaikan praktikum ini mahasiswa diharapkan:

1. Mampu memahami konsep dasar transformation (transformasi data).
2. Mampu memahami jenis-jenis data transformation.
3. Mampu memahami dan menerapkan beberapa proses data transformasi seperti: centering, normalisasi, dan scalling.

Indikator ketercapaian diukur dengan:

1. Mahasiswa dapat menghasilkan Transformasi data pada studi kasus dapat dilakukan dengan baik.

## 3.2. TEORI PENDUKUNG

Tranformasi merupakan proses transformasi data yaitu proses pengkategorian atau perubahan data ke format yang sesuai untuk proses dalam data mining sehingga lebih mudah untuk diolah. Adapun proses transformasi dapat dilakukan dengan cara:

1. Smoothing (binning, clustering, dan regresi).
2. Agresi (summarize, menggunakan dimensi yang lebih general (cube construction)).
3. Generalisasi, misal menggunakan dimensi propinsi daripada kabupaten atau grouping (hirarki konsep).
4. Normalisasi, mengelompokkan data sesuai skala tertentu, misal IPK.
5. Normalisasi min-max, standarisasi data dengan menempatkan data dalam range 0 sampai 1, nilai terkecil sebagai 0, dan nilai terbesar sebagai 1. Nilai baru = ((nilai_lama - nilai_minimal) / (nilai_maksimal - nilai_minimal)) (range_maksimal = range_minimal) + range_minimal. range_minimal = 0, range_maksimal = 1.
6. Normalisasi z-index, nilai_baru = (nilai_lama = rata_rata) / standar_deviasi
7. Normalisasi skala desimal, nilai_baru = nilai_lama / 10^x,
8. Centering, mengurangi setiap data dengan rata-rata dari setiap atribut yang ada.
9. Normalization, membagi setiap data yang di centering dengan standar deviasi dari atribut bersangkutan.
10. Scalling, mengubah data sehingga berada dalam skala tertentu.

## 3.3. ALAT DAN BAHAN

Alat dan bahan yang digunakan dalam praktikum ini yaitu:

1. Komputer
2. vs code
3. Dataset

## 3.4. LANGKAH PRAKTIKUM

ikuti langkah praktikum berikut ini:

1. Jika akan dilakukan analisi data mining menggunakan Data Alumni untuk mengetahi hubungan.
   antara IPK, TOEFL, Waktu mendapatkan pekerjaan, Lama studi, Umur, Gaji. Maka lakukanlah
   analisis Data Alumni untuk kemudian dilakukan proses transformasi data.
2. Buka data set alumni dengan nama _Data Alumni.xlxs_.
3. Perhatikan record-record pada tabel tersebut.
4. Lakukan proses transformasi data menggunakan Anaconda Jupyter Notebook.

a. IPK

Nilai IPK dikategorikan menjadi 3, seperti yang terlihat pada tabel dibawah ini:
| Kategori | Keterangan |
|----------|----------------------------|
| IPK Minimum (Min) | Untuk IPK <2.75 |
| IPK Rata-rata (Rat) | Untuk IPK >=2.75 - 3.50|
| IPK Maksimum (Max) | IPK >3.50 - 4.00 |

- merubah format data pada kolom IPK.

```python
df['IPK'] = df['IPK'].apply(str)
df['IPK'] = df['IPK'].str.replace(',', '.').apply(float)

df
```

b. TOEFL

Nilai TOEFL dikategorikan menjadi 3, seperti yang terlihat pada tabel dibawah ini:
| Kategori | Keterangan |
|----------|----------------------------|
| T1 | 400 - 449 |
| T2 | 450 - 499 |
| T3 | >=500 |

maka datat diterapkan pada syntax seperti berikut ini:

```python
for index, row in df.iterrows():
    if row['TOEFL'] > 500:
        df.loc[index, 'nilai_ipk'] = 'T3'
    elif row ['TOEFL'] >= 450:
        df.loc[index, 'Kategori'] = 'T2'
    else:
        df.loc[index, 'Kategori'] = 'T1'
df[['NIM', 'IPK', 'TOEFL', 'Kategori']]
```

c. waktu mendapatkan pekerjaan

Nilai waktu tunggu mendapatkan pekerjaan dikategorikan menjadi 4, seperti yang terlihat pada tabel dibawah ini:
| Kategori | Keterangan |
|----------|------------|
| W1 | 0 - 2.9 bulan |
| W2 | 3 - 5.9 bulan |
| W3 | 6 - 8.9 bulan |
| W4 | 9 - 12 bulan |

maka dapat diterapkan seperti ini pada syntax:

```python
for index, row in df.iterrows():
    if row['MasaTunggu'] > 9:
        df.loc[index, 'MasaTunggu'] = 'W4'
    elif row ['TOEFL'] >= 6:
        df.loc[index, 'MasaTunggu'] = 'W3'
    elif row ['MasaTunggu'] >= 3:
        df.loc[index, 'MasaTunggu'] = 'W2'
    else:
        df.loc[index, 'MasaTunggu'] = 'W1'
df[['NIM', 'IPK', 'TOEFL', 'MasaTunggu']]
```

d. Lama Studi

Nilai lama studi dikategorikan menjadi 2, seperti yang terlihat pada tabel di bawah ini:
| Kategori | Keterangan |
|----------|------------|
| Tepat Waktu (TW) | Jika lama studi <= 4 tahun |
| Tidak Tepat Waktu | Jika lama studi > 4 tahun |

Maka dapat diterapkan seperti ini pada sysntax:

```python
def perbaiki_masastudi(df):
    for index, row in df.iterrows():
        if row['MasaStudi'] > 3:
            df.loc[index, 'MasaStudi'] = 'TTW'
        else:
            df.loc[index, 'MasaStudi'] = 'TW'
df[['NIM', 'IPK', 'TOEFL', 'Lama Waktu Tunggu', 'MasaStudi']]
```

e. Umur

Nilai umur dikategorikan menjadi 2, seperti yang terlihat pada tabel dibawah ini:
| Kategori | Keterangan |
|----------|------------|
| Usia produktif (UP) | Untuk umur 15 - 24 tahun |
| Tidak Produktif (TP) | Untuk umur 25 - 54 tahun |

Maka dapat diterapkan pada syntax seperti berikut ini:

```python
def perbaiki_umur(df):
    for index, row in df.iterrows():
        if row['Umur'] >= 25:
            df.loc[index, 'Umur'] = 'TP'
        else:
            df.loc[index, 'Umur'] = 'Muda'

df[['NIM', 'IPK', 'TOEFL', 'Lama Waktu Tunggu', 'MasaStudi', 'Umur']]
```

f. Gaji

Nilai gaji dikategorikan menjadi 2, seperti yang terlihat pada tabel dibawah ini:
| Kategori | Keterangan |
|----------|------------|
| Atas UMR (A.UMR) | Gaji >= 1.572.200 |
| Bawah UMR (B.UMR) | Gaji < 1.572.200 |

Maka dapat diterpakan di dalam syntax seperti berikut:

```python
for index, row in df.iterrows():
    if row['Gaji'] >= 1572200:
        df.loc[index, 'Gaji'] = 'A.UMR'
    else:
        df.loc[index, 'Gaji'] = 'B.UMR'

df[['NIM', 'IPK', 'TOEFL', 'MasaTunggu', 'Gaji']]
```

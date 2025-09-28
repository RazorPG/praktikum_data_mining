# PRAKTIKUM 4: ASSOCIATION RULE

## 4.1. TUJUAN DAN INDIKATOR CAPAIAN

Setelah mengikuti praktikum ini mahasiswa diharapkan:

1. Mampu memahami pengertian association rule mining
2. Mampu memahami metode-metode pada association rule

Indikator ketercapaian diukur dengan:

1. Mahasiswa dapat menerapkan Associative and sequential patterns, Market Based Analysis
2. Mahasiswa dapat membuat data mining dengan teknik Association Rule dan menganalisa hasil data mining dengan teknik Association Rule

## 4.2. TEORI PENDUKUNG

Association Rule adalah teknik data mining yang berguna untuk menemukan suatu korelasi atau pola yang terpenting/menarik dari sekumpulan data besar (Margaret, 2003).

Motivasi awal Association Rule berasal dari keinginan untuk menganalisa data transaksi supermarket ditinjau dari perilaku pelanggan dalam membeli produk. Association Rule menjelaskan seberapa sering suatu produk dibeli secara bersamaan. Sebagai contoh: seorang pelanggan membeli sabun maka seberapa mungkin juga ia membeli pasta gigi (Kuswardani dkk, 2011)

Penting tidaknya suatu aturan asosiatis dapat diketahui dengan dua parameter:

- Support: persentase kombinasi item tersebut dalam database
- Confidence: kuatnya hubungan antar item dalam aturan asosiatif

## 4.3. ALAT DAN BAHAN

Alat dan bahan yang digunakan dalam praktikum ini yaitu:

1. Komputer
2. Anaconda app
3. Dataset

## 4.4. LANGKAH PRAKTIKUM

Ikuti langkah praktikum berikut ini:

1. Analisis data mining menggunakan data alumni untuk mengetahui hubungan antara:

   - Fasilitas memadai
   - SDM berpengaruh
   - Kerja sesuai jurusan
   - Kurikulum sesuai dengan dunia kerja

2. Buka dataset siswa dengan nama "Data Alumni.xlsx"

   - Import dataset menggunakan pandas

   ```python
   df = pd.read_excel('Data Alumni.xlsx')
   ```

   - Periksa struktur data dengan df.head() dan df.info()

   ```python
   print(df.head())
   print("\nInformasi Dataset:")
   print(df.info())
   ```

   - Lakukan pembersihan data jika diperlukan

   ```python
   # Menghapus missing values jika ada
   df = df.dropna()
   # Reset index setelah pembersihan
   df = df.reset_index(drop=True)
   ```

3. Lakukan proses association rule mining menggunakan Python:

   - Import library yang diperlukan (pandas, mlxtend)
   - Konversi data ke format yang sesuai untuk association rule

   ```python
   # Mengubah data menjadi format boolean
   df_encoded = pd.get_dummies(df[['Fasilitas_Memadai', 'SDM_Berpengaruh',
                                 'Kerja_Sesuai_Jurusan', 'Kurikulum_Sesuai']])
   ```

   - Terapkan algoritma Apriori

   ```python
   # Menerapkan algoritma apriori dengan minimum support 0.3
   frequent_itemsets = apriori(df_encoded, min_support=0.3, use_colnames=True)
   ```

   - Hitung support dan confidence

   ```python
   # Membuat rules dengan minimum confidence 0.7
   rules = association_rules(frequent_itemsets, metric="confidence", min_threshold=0.7)
   ```

4. Import Library yang akan digunakan:

   ```python
   import pandas as pd
   from mlxtend.frequent_patterns import apriori
   from mlxtend.frequent_patterns import association_rules
   import matplotlib.pyplot as plt
   import networkx as nx
   import seaborn as sns
   ```

5. Analisis hasil association rule:

   - Tentukan minimum support dan confidence

   ```python
   min_support = 0.3
   min_confidence = 0.7
   ```

   - Interpretasi hasil rules yang didapat

   ```python
   # Menampilkan rules dengan sorting berdasarkan confidence
   print(rules.sort_values('confidence', ascending=False))
   ```

   - Visualisasikan hasil dengan scatter plot atau network graph

   ```python
   # Scatter plot
   plt.scatter(rules['support'], rules['confidence'])
   plt.xlabel('Support')
   plt.ylabel('Confidence')
   plt.title('Support vs Confidence')
   plt.show()
   ```

   - Dokumentasikan temuan penting dalam DataFrame

6. Buat kesimpulan:
   - Identifikasi pola hubungan yang kuat berdasarkan nilai support dan confidence
   - Berikan rekomendasi berdasarkan rules dengan confidence tertinggi
   - Dokumentasikan insight yang diperoleh dalam bentuk laporan terstruktur

Catatan:

- Pastikan semua library terinstal sebelum menjalankan kode
- Sesuaikan nilai minimum support dan confidence sesuai kebutuhan
- Lakukan interpretasi hasil dengan mempertimbangkan konteks bisnis

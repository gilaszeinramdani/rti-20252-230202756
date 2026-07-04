# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : data_log_pengering_padi_esp32.csv
Jumlah data awal  : 100 record

Cleaning:
| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing | 3 kasus | Data yang kosong pada kolom suhu dan kelembapan dihapus | Jumlah data kosong masih sedikit, yaitu 3 dari 100 data, sehingga tidak terlalu memengaruhi keseluruhan data |
| Duplikat | 2 kasus | Data duplikat dihapus setelah dicek berdasarkan waktu pencatatan dan nilai sensor | Data memiliki timestamp dan nilai sensor yang sama, sehingga dianggap sebagai data tercatat ganda |
| Error format | 4 kasus | Format angka diperbaiki, misalnya koma diganti titik dan satuan dihapus | Data perlu dibuat seragam agar dapat dihitung dan dianalisis dengan benar |


Transformation:
| Transformasi | Variabel | Detail | Alasan |
|-------------|----------|--------|--------|
| Konversi tipe data | suhu, kelembapan, waktu_pengeringan | Diubah dari teks menjadi angka | Supaya data bisa dihitung secara statistik |
| Penghapusan satuan | suhu, kelembapan | Contoh: "35°C" menjadi 35 dan "70%" menjadi 70 | Agar format data lebih bersih dan tidak mengganggu proses analisis |
| Pembuatan status kondisi | suhu dan kelembapan | Dibuat kategori: normal, terlalu tinggi, atau terlalu lembap | Untuk memudahkan pembacaan kondisi sistem saat pengujian |
| Penyamaan format waktu | timestamp | Format waktu dibuat seragam | Supaya urutan data pengujian lebih mudah dibaca |

Normalization:
  Metode    : Tidak dilakukan normalisasi 
  Alasan    : Data yang dianalisis masih berupa suhu, kelembapan, waktu, dan status alat. Nilainya masih mudah dibaca dalam satuan asli, sehingga normalisasi belum terlalu dibutuhkan.
  Parameter : Tidak ada, karena normalisasi tidak digunakan.

Leakage Check:
  [x] Parameter normalisasi dari training set saja
  [x] Tidak ada informasi test set dalam preprocessing
  [x] Cross-validation dilakukan setelah split

Jumlah data akhir : 91 record
Script tersedia   : [ ] Ya → path: ____ | [x] Belum
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing di kolom suhu dan kelembapan | 3 dari 100 data | Data dihapus | Karena jumlahnya kecil dan tidak sampai 5%, penghapusan data masih aman dilakukan |
| Data duplikat pada timestamp yang sama | 2 dari 100 data | Salah satu data dihapus | Karena timestamp dan nilai sensornya sama persis, data dianggap tercatat dua kali |
| Format suhu tidak seragam | 2 dari 100 data | Format diperbaiki | Ada data yang tertulis “35°C”, sedangkan data lain hanya angka. Format harus disamakan |
| Format kelembapan tidak seragam | 2 dari 100 data | Simbol persen dihapus | Data seperti “70%” diubah menjadi “70” agar bisa dihitung |
| Nilai suhu tidak masuk akal | 1 dari 100 data | Data dicek ulang, lalu dihapus | Nilai terlalu jauh dari kondisi normal pengeringan sehingga dianggap error pembacaan sensor |

**Jumlah data sebelum cleaning:** 100 record 
**Jumlah data setelah cleaning:** 91 record  
**Persentase data yang hilang/berubah:** 9%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| Suhu | 28°C – 55°C | Cenderung normal | Tidak terlalu terlihat | Tidak perlu | Nilai suhu masih mudah dibaca dan memang dibutuhkan dalam satuan aslinya |
| Kelembapan | 40% – 85% | Menurun selama proses pengeringan | Tidak | Tidak perlu | Kelembapan lebih jelas dianalisis dalam bentuk persen |
| Waktu pengeringan | 0 – 120 menit | Bertambah sesuai proses | Tidak | Tidak perlu | Waktu lebih mudah dipahami dalam satuan menit |
| Status kipas | ON/OFF | Kategori | Tidak | Encoding sederhana | Karena datanya berbentuk kategori, cukup diubah menjadi 1 untuk ON dan 0 untuk OFF jika diperlukan |
| Status motor | ON/OFF | Kategori | Tidak | Encoding sederhana | Sama seperti status kipas, cukup dikodekan jika akan dianalisis secara numerik |


**Apakah normalisasi diperlukan?** [ ] Ya / [x] Tidak
**Justifikasi:**
> Normalisasi belum diperlukan karena data yang digunakan masih dalam skala yang jelas dan mudah dipahami. Suhu, kelembapan, dan waktu pengeringan lebih baik tetap ditampilkan dalam satuan aslinya agar hasil analisis lebih mudah dijelaskan. Selain itu, penelitian ini lebih fokus pada pengamatan kinerja alat, bukan pada model machine learning berbasis jarak seperti KNN atau clustering.
**Leakage check:**
- [x] Parameter dihitung dari training set saja
- [x] Normalisasi diterapkan setelah train-test split

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset: data_log_pengering_padi_esp32.csv
2. Data awal: 100 records records, 6 features features
  Fitur yang digunakan:
   - timestamp
   - suhu
   - kelembapan
   - waktu_pengeringan
   - status_kipas
   - status_motor
3. Cleaning:
   - Missing values: 3 kasus kasus, metode: listwise deletion  
     Data yang kosong dihapus karena jumlahnya masih kecil dan tidak terlalu memengaruhi jumlah data keseluruhan.
   - Duplikat: 2 kasus kasus, tindakan: hapus salah satu data  
     Data duplikat ditemukan pada timestamp dan nilai sensor yang sama, sehingga hanya satu data yang dipertahankan.
   - Error: 4 kasus kasus, tindakan: format diperbaiki  
     Error yang ditemukan berupa format suhu dan kelembapan yang tidak seragam, seperti penggunaan simbol °C dan %. Format tersebut dibersihkan agar data dapat diproses.
4. Transformation: Transformasi dilakukan dengan mengubah kolom suhu, kelembapan, dan waktu pengeringan menjadi tipe numerik. Selain itu, status kipas dan motor dapat diubah menjadi kode angka, yaitu 1 untuk ON dan 0 untuk OFF, apabila dibutuhkan dalam analisis lanjutan.
5. Normalisasi: Tidak dilakukan normalisasi.  
   Alasannya, data masih lebih mudah dibaca dalam satuan asli. Suhu tetap menggunakan Celcius, kelembapan tetap dalam persen, dan waktu tetap dalam menit. (metode), parameter dari tidak ada, karena normalisasi tidak digunakan.
6. Data akhir:  91 records records, 6 features
7. Leakage check: [x] Lulus / [ ] Ada masalah
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> Saya pernah berpikir bahwa normalisasi itu seperti langkah wajib sebelum data dianalisis. Padahal setelah dipahami, normalisasi tidak selalu diperlukan. Dalam penelitian sistem pengering padi ini, data seperti suhu, kelembapan, dan waktu justru lebih mudah dibaca jika tetap menggunakan satuan aslinya. Kalau semua data langsung dinormalisasi tanpa alasan yang jelas, hasilnya bisa menjadi kurang mudah dipahami.

> Risiko dari over-preprocessing adalah data bisa berubah terlalu jauh dari kondisi aslinya. Data yang sebenarnya masih wajar bisa dianggap aneh, atau sebaliknya data yang penting malah dihapus karena dianggap mengganggu. Selain itu, terlalu banyak preprocessing juga bisa membuat hasil penelitian terlihat rapi, tetapi sebenarnya kehilangan makna aslinya. Karena itu, preprocessing harus dilakukan seperlunya saja, sesuai kebutuhan analisis, dan setiap langkahnya harus dijelaskan dengan jujur.


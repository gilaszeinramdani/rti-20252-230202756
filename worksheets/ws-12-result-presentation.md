# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Apakah sistem pengering padi otomatis berbasis ESP32 dapat meningkatkan efisiensi waktu pengeringan dan menjaga kestabilan suhu serta kelembapan dibandingkan metode pengeringan konvensional?
Metrik Utama      : Waktu pengeringan sampai kondisi padi mendekati kering stabil.

Tabel Hasil:
| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
| ESP32 otomatis + kipas + motor | 92 ± 6 menit | 2,1 ± 0,4 °C | 10 |
| ESP32 otomatis + kipas | 105 ± 8 menit | 2,8 ± 0,6 °C | 10 |
| Pengeringan konvensional | 165 ± 15 menit | 5,6 ± 1,1 °C | 10 |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 | Bar chart + error bar | Sistem ESP32 otomatis lebih cepat dibandingkan pengeringan konvensional | Waktu pengeringan mean ± std |
| 2 | Line chart | Suhu pada sistem otomatis lebih stabil selama proses pengeringan | Perubahan suhu terhadap waktu |
| 3 | Scatter plot | Ada hubungan antara kestabilan suhu dan waktu pengeringan | Fluktuasi suhu vs waktu pengeringan |

Bias Check:
  [x] Y-axis mulai dari 0 (atau dijustifikasi)
  [x] Error bar/CI ditampilkan
  [x] Semua data disertakan (tidak cherry-picked)
  [x] Tidak menggunakan 3D tanpa alasan
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
| ESP32 otomatis + kipas + motor | 92 ± 6 menit | 39 ± 3 %RH | 10 |
| ESP32 otomatis + kipas | 105 ± 8 menit | 43 ± 4 %RH | 10 |
| Pengeringan konvensional | 165 ± 15 menit | 55 ± 6 %RH | 10 |
**Checklist tabel:**
- [x] Self-contained (judul jelas, satuan ada, N tercantum)
- [x] Mean ± std (bukan single number)
- [x] Diurutkan berdasarkan metrik utama
- [x] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | Bar chart + error bar | Membandingkan waktu pengeringan pada setiap skenario | Mean waktu pengeringan ± std |
| 2 | Line chart | Menunjukkan kestabilan suhu selama proses pengeringan | Data suhu tiap 10 menit |
| 3 | Scatter plot | Melihat hubungan antara fluktuasi suhu dan lama waktu pengeringan | Rata-rata fluktuasi suhu dan waktu pengeringan |

## Penjelasan Rencana Grafik

### 1. Bar Chart + Error Bar

Grafik pertama menggunakan **bar chart** karena tujuannya adalah membandingkan waktu pengeringan antar skenario. Error bar perlu ditampilkan supaya pembaca tidak hanya melihat rata-rata, tetapi juga mengetahui seberapa besar variasi hasil percobaan.

Pesan utama dari grafik ini adalah bahwa sistem otomatis berbasis ESP32 memiliki waktu pengeringan yang lebih cepat dibandingkan pengeringan konvensional.

### 2. Line Chart

Grafik kedua menggunakan **line chart** karena data suhu berubah dari waktu ke waktu. Grafik ini cocok untuk melihat apakah suhu selama proses pengeringan stabil atau naik turun terlalu jauh.

Pesan utama dari grafik ini adalah sistem otomatis lebih mampu menjaga suhu agar tidak terlalu berubah drastis selama proses pengeringan.

### 3. Scatter Plot

Grafik ketiga menggunakan **scatter plot** untuk melihat hubungan antara fluktuasi suhu dan waktu pengeringan. Dari grafik ini dapat dilihat apakah suhu yang lebih stabil cenderung membuat waktu pengeringan menjadi lebih cepat.

Pesan utama dari grafik ini adalah semakin kecil fluktuasi suhu, maka proses pengeringan cenderung lebih efisien.

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | Ya. Perbedaannya hanya 0,4%, tetapi karena Y-axis dimulai dari 90%, selisih kecil tersebut bisa terlihat sangat besar. |
| Apakah error bar ditampilkan? | Tidak disebutkan. Jika error bar tidak ditampilkan, pembaca tidak tahu apakah perbedaan 0,4% itu benar-benar berarti atau hanya variasi biasa. |
| Apakah semua kondisi ditampilkan? | Belum jelas. Jika hanya dua metode yang ditampilkan tanpa kondisi lain, grafik bisa kurang lengkap. |
| Apa solusinya? | Gunakan Y-axis mulai dari 0, tampilkan error bar, tuliskan nilai angka secara jelas, dan sertakan semua metode atau skenario yang memang diuji. |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [x] Semua bias check lulus
- [x] Ada yang perlu diperbaiki: Pada grafik line chart, data suhu harus diambil secara rutin, misalnya setiap 10 menit. Jika jarak pengambilan data tidak konsisten, grafik bisa membuat pembaca salah memahami perubahan suhu yang sebenarnya.

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel dan grafik sama-sama diperlukan karena keduanya punya fungsi yang berbeda. Tabel membantu pembaca melihat angka secara lebih jelas dan detail. Misalnya, pembaca bisa langsung melihat waktu pengeringan, kelembapan akhir, standar deviasi, dan jumlah percobaan. Dengan tabel, data terlihat lebih rapi dan mudah dicek satu per satu.

> Sementara itu, grafik membantu pembaca melihat pola secara cepat. Kalau hanya membaca tabel, kadang perbedaan antar skenario tidak langsung terlihat. Dengan grafik, pembaca bisa lebih mudah melihat bahwa sistem ESP32 otomatis lebih cepat dibandingkan pengeringan konvensional. Jadi, tabel memberikan ketelitian angka, sedangkan grafik membantu memperlihatkan pola dan perbandingan.

> Saya pernah membuat grafik yang tanpa sadar bisa menyesatkan, misalnya ketika sumbu Y tidak dimulai dari 0. Akibatnya, perbedaan kecil terlihat seperti perbedaan yang sangat besar. Dari materi ini, saya memahami bahwa membuat grafik tidak boleh hanya mengejar tampilan menarik, tetapi juga harus jujur, jelas, dan tidak membuat pembaca salah paham.


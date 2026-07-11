# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:
   | Skenario | Mean | Std | Median | Min | Max | n |
   |----------|------|-----|--------|-----|-----|---|
   | Pengeringan manual | Diisi setelah pengujian | Diisi setelah pengujian | Diisi setelah pengujian | Diisi setelah pengujian | Diisi setelah pengujian | Diisi sesuai jumlah percobaan |
   | Pengeringan otomatis berbasis ESP32 | Diisi setelah pengujian | Diisi setelah pengujian | Diisi setelah pengujian | Diisi setelah pengujian | Diisi setelah pengujian | Diisi sesuai jumlah percobaan |

2. Uji Hipotesis:
   Uji yang digunakan  : Paired t-test atau Wilcoxon signed-rank test
   Justifikasi          : Uji ini digunakan karena penelitian membandingkan dua kondisi, yaitu pengeringan manual dan pengeringan otomatis berbasis ESP32. Jika data berdistribusi normal, maka digunakan paired t-test. Namun, jika data tidak normal, maka digunakan Wilcoxon signed-rank test.
   Hasil: p = Diisi setelah pengujian, effect size (d/r/η²) = Cohen's d
   CI 95%               : [Diisi setelah pengujian]

3. Keputusan:
   [ ] H₀ ditolak → H₁ diterima
   [x] H₀ tidak ditolak

4. Interpretasi:
   Hubungan ke RQ       : Hasil analisis digunakan untuk menjawab pertanyaan penelitian, yaitu apakah sistem pengering padi otomatis berbasis ESP32 dapat membantu proses pengeringan menjadi lebih efektif, stabil, dan efisien dibandingkan metode manual.
   Practical significance: Secara praktik, sistem dianggap bermanfaat apabila mampu menjaga suhu dan kelembapan lebih stabil, mengurangi waktu pengeringan, serta mengurangi kebutuhan pengawasan manual oleh pengguna. Jadi, tidak hanya dilihat dari hasil statistik saja, tetapi juga dari manfaat langsung alat ketika digunakan.
   Perbandingan literatur: Hasil penelitian ini dapat dibandingkan dengan penelitian terdahulu tentang sistem pengering gabah otomatis berbasis mikrokontroler dan IoT. Jika hasil pengujian menunjukkan bahwa sistem mampu membaca suhu dan kelembapan secara real-time serta mengontrol kipas dan motor secara otomatis, maka penelitian ini sejalan dengan penelitian sebelumnya yang menyatakan bahwa sistem otomatis dapat membantu meningkatkan efisiensi pengeringan.

5. Limitation:
   | Jenis | Ancaman | Dampak | Mitigasi |
   |-------|---------|--------|----------|
   | Internal validity | Kondisi suhu dari sumber panas tidak selalu stabil | Hasil pengeringan bisa berubah-ubah antar percobaan | Mengatur jarak sumber panas dan melakukan pengujian berulang |
   | External validity | Pengujian masih berupa prototype | Hasil belum tentu sama jika diterapkan pada skala besar | Melakukan pengembangan alat dengan kapasitas lebih besar |
   | Construct validity | Sensor DHT11 hanya membaca suhu dan kelembapan udara, bukan kadar air gabah secara langsung | Data kelembapan belum sepenuhnya mewakili kadar air gabah | Menambahkan sensor kadar air gabah pada pengembangan berikutnya |
   | Statistical limitation | Jumlah pengujian masih terbatas | Kesimpulan statistik belum terlalu kuat | Menambah jumlah percobaan agar data lebih valid |
   | Technical limitation | Relay, kipas, dan motor bergantung pada kestabilan power supply | Sistem dapat tidak bekerja optimal jika tegangan tidak stabil | Menggunakan power supply yang sesuai dan stabil |

6. Failure Analysis (jika H₀ tidak ditolak): Failure analysis dilakukan apabila hasil pengujian tidak sesuai dengan hipotesis awal. Misalnya, sistem otomatis ternyata belum mampu mempercepat proses pengeringan secara signifikan dibandingkan metode manual.
   Penyebab potensial  : Beberapa kemungkinan penyebabnya adalah suhu dari sumber panas tidak stabil, posisi sensor kurang tepat, sirkulasi udara panas belum merata, atau kapasitas kipas belum cukup kuat untuk menyebarkan panas ke seluruh ruang pengering.
   Boundary condition   : Sistem ini kemungkinan hanya bekerja optimal pada jumlah padi tertentu dan ruang pengering berukuran kecil. Jika jumlah padi terlalu banyak atau ruang pengering terlalu besar, maka panas tidak tersebar merata dan proses pengeringan menjadi kurang maksimal.
   Insight              : Hasil yang tidak sesuai bukan berarti penelitian gagal total. Dari kondisi tersebut dapat diketahui batas kemampuan sistem. Misalnya, sistem sudah mampu membaca suhu dan kelembapan, tetapi masih perlu peningkatan pada desain ruang pengering, posisi sensor, kekuatan kipas, atau penambahan sensor kadar air gabah.
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | 2 grup, yaitu pengeringan manual dan pengeringan otomatis berbasis ESP32 |
| Apakah data berpasangan atau paired? | Ya, karena kedua metode dapat diuji pada jenis padi, berat padi, dan kondisi awal yang sama |
| Apakah distribusi normal? | Perlu diuji terlebih dahulu menggunakan uji normalitas, misalnya Shapiro-Wilk |
| **Uji yang dipilih:** | Paired t-test jika data normal, Wilcoxon signed-rank jika data tidak normal |
| **Justifikasi:** | Karena penelitian membandingkan dua metode pengeringan pada kondisi yang dibuat sama atau mendekati sama |

**Effect size yang akan dilaporkan:** [x] Cohen's d / [ ] Eta-squared / [ ] Lainnya: ____

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
| Model | Accuracy (mean ± std) | n |
|-------|----------------------|---|
| Sistem otomatis ESP32 | 89.2 ± 1.5 | 10 |
| Metode manual | 87.8 ± 2.1 | 10 |

p = 0.045, Cohen's d = 0.74, CI 95% = [0.03, 2.77]

| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik | Nilai p = 0.045 lebih kecil dari 0.05, sehingga hasil dapat dikatakan signifikan secara statistik pada taraf α = 0.05 |
| Effect size | Cohen's d = 0.74 menunjukkan efek sedang menuju besar. Artinya, perbedaan antara sistem otomatis dan metode manual cukup terlihat |
| Practical significance | Secara praktik, sistem otomatis berbasis ESP32 dapat dikatakan bermanfaat jika mampu membuat suhu lebih stabil, mengurangi waktu pengeringan, dan mengurangi pengawasan manual |
| Hubungan ke RQ | Hasil ini mendukung pertanyaan penelitian bahwa sistem pengering padi otomatis berbasis ESP32 berpotensi meningkatkan efektivitas proses pengeringan |
| Perbandingan literatur | Hasil ini sejalan dengan penelitian terdahulu yang menunjukkan bahwa penggunaan mikrokontroler dan sensor dapat membantu proses monitoring serta kontrol otomatis pada sistem pengering |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru Anda mendapat F1 = 83.2%, baseline = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | Tidak bisa langsung disebut gagal total. Hasil tersebut menunjukkan bahwa hipotesis belum didukung oleh data, tetapi tetap menjadi temuan penting untuk mengetahui batas kemampuan sistem |
| Kemungkinan penyebab? | Kemungkinan penyebabnya adalah suhu sumber panas tidak stabil, kipas kurang kuat, sensor kurang tepat posisinya, atau motor pengaduk belum mampu meratakan padi dengan baik |
| Boundary condition? | Sistem mungkin hanya efektif pada ruang pengering kecil, jumlah padi terbatas, dan kondisi sumber panas yang stabil. Jika digunakan pada kondisi yang lebih besar atau panas tidak stabil, hasilnya bisa menurun |
| Insight yang bisa diambil? | Sistem otomatis tidak cukup hanya membaca suhu dan kelembapan. Desain mekanik, aliran udara panas, posisi sensor, dan pengadukan padi juga sangat berpengaruh terhadap hasil pengeringan |
| Apakah layak dilaporkan? Mengapa? | Ya, sangat layak dilaporkan. Hasil negatif tetap penting karena dapat menunjukkan bagian sistem yang perlu diperbaiki dan menjadi dasar pengembangan alat berikutnya |

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| Statistical | Jumlah percobaan masih sedikit | Hasil analisis belum terlalu kuat untuk dijadikan kesimpulan umum |
| Internal validity | Suhu dari sumber panas tidak stabil | Sistem sulit menjaga proses pengeringan tetap konsisten |
| Construct validity | Sensor DHT11 tidak mengukur kadar air gabah secara langsung | Data kelembapan udara belum tentu sama dengan kadar air gabah |
| External validity | Alat masih berupa prototype | Hasil belum tentu sama jika digunakan pada skala petani yang lebih besar |
| Technical | Kipas dan motor pengaduk belum tentu cukup kuat | Pengeringan bisa tidak merata pada seluruh bagian padi |

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Failure dalam riset tidak selalu berarti gagal sepenuhnya. Dalam penelitian, hasil yang tidak sesuai hipotesis tetap dapat menjadi kontribusi apabila dianalisis dengan jujur dan jelas. Dari hasil yang kurang berhasil, peneliti dapat mengetahui kelemahan sistem, batas penggunaan alat, serta bagian yang perlu diperbaiki.

> Pada penelitian sistem pengering padi otomatis berbasis ESP32, failure analysis dapat membantu melihat bahwa keberhasilan alat tidak hanya ditentukan oleh sensor dan program saja. Faktor lain seperti sumber panas, aliran udara, kapasitas kipas, posisi sensor, dan desain ruang pengering juga sangat berpengaruh. Dengan begitu, hasil negatif justru dapat menjadi dasar untuk membuat alat yang lebih baik pada penelitian berikutnya.


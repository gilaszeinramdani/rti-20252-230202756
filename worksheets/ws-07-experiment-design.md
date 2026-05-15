# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Apakah sistem pengering padi otomatis berbasis ESP32 dengan sensor suhu dan kelembapan mampu meningkatkan efisiensi dan kestabilan proses pengeringan dibanding metode konvensional?
Hypothesis        : Sistem otomatis berbasis ESP32 mampu mempercepat waktu pengeringan dan menjaga kestabilan suhu serta kelembapan lebih baik dibanding pengeringan manual.
Tipe Eksperimen   : [✓] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control |Pengeringan padi konvensional/manual|Tanpa sistem otomatis|Jenis gabah sama, berat gabah sama, ruangan sama|
| Treatment |Pengeringan menggunakan sistem otomatis berbasis ESP32|ESP32 + DHT11 + relay + kipas|Jenis gabah sama, berat gabah sama, ruangan sama|

Fairness Checklist:
  [✓] Dataset identik untuk semua kondisi
  [✓] Preprocessing setara
  [✓] Tuning effort setara
  [✓] Environment identik
  [✓] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    |Perubahan suhu lingkungan selama eksperimen|Pengujian dilakukan pada ruang dan waktu yang sama|
| External    |Sistem hanya diuji pada satu jenis gabah|Menguji beberapa jenis gabah dan kondisi lingkungan berbeda|
| Construct   |Sensor DHT11 memiliki akurasi terbatas|Melakukan kalibrasi sensor sebelum pengujian|
| Conclusion  |Jumlah sampel pengujian terlalu sedikit|Melakukan pengulangan eksperimen beberapa kali|

Statistical Plan:
  Uji statistik   : Independent t-test
  Justifikasi      : Membandingkan rata-rata waktu pengeringan antara metode manual dan sistem otomatis
  Alpha            : 0.05
  Effect size min  : 0.5
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah sistem pengering padi otomatis berbasis ESP32 dengan sensor suhu dan kelembapan mampu meningkatkan efisiensi dan kestabilan proses pengeringan dibanding metode konvensional?
**Tipe eksperimen:** [✓] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | *Pengeringan padi secara manual/tradisional tanpa sistem otomatis* | *Tanpa ESP32 dan sensor otomatis* | *Jenis gabah sama, berat gabah sama, ruangan sama, waktu pengujian sama* |
| Treatment | *Pengeringan menggunakan sistem otomatis berbasis ESP32 dan sensor DHT11* | *ESP32 + sensor DHT11 + relay + kipas* | *Jenis gabah sama, berat gabah sama, ruangan sama, waktu pengujian sama* |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | *✅* | *Menggunakan jenis dan jumlah gabah yang sama pada semua pengujian* |
| Preprocessing setara | *✅* | *Kondisi awal gabah dan kadar air awal disamakan* |
| Tuning effort setara | *✅* | *Pengaturan suhu dan kelembapan dilakukan dengan prosedur yang sama* |
| Environment identik | *✅* | *Pengujian dilakukan pada ruangan dan kondisi lingkungan yang sama* |
| Metrik evaluasi sama | *✅* | *Menggunakan metrik waktu pengeringan, suhu, dan kelembapan untuk semua kondisi* |

**Ada yang tidak fair?** [ ] Ya / [✓] Tidak
> Jika ya, bagaimana cara memperbaikinya? Karena seluruh kondisi pengujian dibuat sama, maka perbandingan antara metode manual dan sistem otomatis dapat dianggap fair.

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | *Perubahan suhu atau kelembapan lingkungan selama eksperimen dapat mempengaruhi hasil* | *Melakukan pengujian pada ruang dan waktu yang sama* |
| External | *Sistem hanya diuji pada satu jenis gabah dan skala kecil* | *Menguji sistem pada beberapa jenis gabah dan kondisi berbeda* |
| Construct | *Sensor DHT11 memiliki tingkat akurasi terbatas dalam membaca suhu dan kelembapan* | *Sensor DHT11 memiliki tingkat akurasi terbatas dalam membaca suhu dan kelembapan* |
| Conclusion | *Jumlah sampel dan pengulangan eksperimen terlalu sedikit* | *Melakukan eksperimen berulang dan menambah jumlah sampel pengujian* |

**Ancaman mana yang paling sulit dimitigasi?** External validity
**Mengapa?**
> Karena kondisi nyata di lapangan sangat beragam, seperti jenis gabah, cuaca, kelembapan udara, dan kapasitas pengeringan yang berbeda-beda sehingga hasil pengujian laboratorium belum tentu langsung dapat digeneralisasi.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah semua metode diuji menggunakan dataset dan kondisi eksperimen yang sama?
2. Apakah baseline yang digunakan sudah dituning dan dibandingkan secara fair?
3. Apakah peningkatan hasil yang diperoleh signifikan secara statistik dan menggunakan metrik evaluasi yang sama?

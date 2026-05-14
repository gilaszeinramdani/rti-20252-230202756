# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Belum adanya sistem pengering padi otomatis berbasis ESP32 yang mampu
mengontrol suhu dan kelembapan secara real-time untuk meningkatkan
efisiensi pengeringan dibanding metode konvensional.

Research Question:
  Tipe         : [✓] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Apakah sistem pengering padi otomatis berbasis ESP32 menggunakan
  sensor DHT11 menghasilkan waktu pengeringan lebih cepat dan
  kestabilan suhu lebih baik dibanding metode pengeringan konvensional?
  Variabel IV  : Metode pengeringan (ESP32 otomatis vs konvensional)
  Variabel DV  : Waktu pengeringan dan kestabilan suhu
  Metrik       : Lama waktu pengeringan, suhu rata-rata, perubahan suhu
  Dataset      : Data hasil pengujian proses pengeringan padi menggunakan sistem ESP32
  dan metode konvensional
  Baseline     : Metode pengeringan padi konvensional

Quality Check RQ:
  [✓] Variabel spesifik
  [✓] Metrik jelas
  [✓] Baseline ada
  [✓] Konteks disebutkan
  [✓] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Penggunaan ESP32 dan sensor DHT11 dapat meningkatkan efisiensi
  pengeringan padi serta menjaga kestabilan suhu dibanding metode
  pengeringan konvensional.
  Jenis kontribusi        : [✓] Improvement  [ ] Comparison  [ ] Novel approach
  Gap yang diisi          :  Keterbatasan sistem pengeringan konvensional yang masih bergantung
  pada cuaca dan belum memiliki kontrol suhu otomatis.

Hypothesis Pair:
  H₀ : Tidak ada perbedaan signifikan pada waktu pengeringan dan kestabilan
  suhu antara sistem pengering padi otomatis berbasis ESP32 dan metode
  konvensional.
  H₁ : Sistem pengering padi otomatis berbasis ESP32 menghasilkan waktu
  pengeringan lebih cepat dan kestabilan suhu lebih baik dibanding
  metode konvensional.
  Threshold              : p-value < 0.05
  Justifikasi threshold  : Nilai 0.05 digunakan sebagai standar umum signifikansi statistik
  dalam penelitian eksperimen.
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Belum adanya sistem pengering padi otomatis berbasis ESP32 yang mampu
mengontrol suhu dan kelembapan secara real-time untuk meningkatkan
efisiensi pengeringan dibanding metode konvensional.

**RQ versi pertama (tulis bebas):**
> Apakah sistem pengering padi otomatis dapat meningkatkan efisiensi pengeringan padi?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | *Ya* | *ESP32 dan sensor DHT11* |
| Metrik terukur | *Tidak* | *Belum ada ukuran spesifik* |
| Baseline | *Ya* | *Pengeringan konvensional* |
| Dataset/konteks | *Ya* | *Pengeringan padi*|

**Tipe RQ:** [✓] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah sistem pengering padi otomatis berbasis ESP32 menggunakan sensor DHT11 menghasilkan waktu pengeringan lebih cepat dan kestabilan suhu lebih baik dibanding metode pengeringan konvensional?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | *Tidak ada perbedaan signifikan pada waktu pengeringan dan kestabilan suhu antara sistem ESP32 dan metode konvensional* |
| H₁ | *Sistem ESP32 menghasilkan waktu pengeringan lebih cepat dan kestabilan suhu lebih baik dibanding metode konvensional* |
| Metrik | *Lama pengeringan dan kestabilan suhu* |
| Threshold | *p-value < 0.05* |
| Justifikasi threshold | *Standar umum penelitian statistik* |

**Apakah hipotesis ini falsifiable?** [✓] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Dengan melakukan eksperimen pengeringan menggunakan kedua metode, kemudian membandingkan hasil menggunakan analisis statistik.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | *Apakah sistem pengering padi otomatis berbasis ESP32 menggunakan sensor DHT11 menghasilkan waktu pengeringan lebih cepat dibanding metode konvensional?* |
| Variable (IV) | *Metode pengeringan* |
| Variable (DV) | *Waktu pengeringan dan kestabilan suhu* |
| Metric | *Lama pengeringan, suhu rata-rata* |
| Data source | *Sensor DHT11 dan hasil pengujian pengeringan* |
| Analysis method | *Uji t dan analisis perbandingan* |

**Apakah rantai lengkap?** [✓] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? Tidak ada, karena rantai operasionalisasi sudah lengkap dan setiap tahap (RQ → Variable → Metric → Data → Analysis) telah terhubung dengan jelas.

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Rancang Bangun Sistem Pengering Padi Otomatis Berbasis ESP32 Menggunakan Sensor Suhu dan Kelembapan
**RQ yang diekstrak:** Apakah sistem pengering padi otomatis berbasis ESP32 mampu meningkatkan efisiensi pengeringan dan menjaga kestabilan suhu?
**Komponen yang hilang:** Dataset spesifik dan metrik evaluasi rinci belum dijelaskan secara detail.

# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: Bagaimana pengaruh sistem pengering padi otomatis berbasis ESP32 menggunakan sensor suhu dan kelembapan terhadap efisiensi dan kestabilan proses pengeringan padi dibanding metode konvensional?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|Sistem pengering|IV|Metode pengeringan|Otomatis vs konvensional|Nominal|-|Membandingkan penggunaan sistem otomatis dan metode manual|Variabel utama yang memengaruhi proses pengeringan|
|Waktu pengeringan gabah|DV|Efisiensi pengeringan|Lama waktu hingga gabah mencapai kadar air target|Ratio|Menit|Menghitung waktu mulai hingga gabah kering|Waktu pengeringan langsung merepresentasikan efisiensi sistem|
|Suhu lingkungan pengering|CV|Kondisi lingkungan|Temperatur ruang pengering|Interval|°C|Dibaca menggunakan sensor DHT11 secara berkala|Suhu memengaruhi kecepatan pengeringan sehingga harus dikontrol|

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [✓] Setiap langkah terdokumentasi
  [✓] Tidak ada "lompatan logis"
  [✓] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Bagaimana pengaruh sistem pengering padi otomatis berbasis ESP32 menggunakan sensor suhu dan kelembapan terhadap efisiensi proses pengeringan gabah?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| *Sistem pengering otomatis berbasis ESP32* | *IV* | *Metode pengeringan modern* | *Otomatis vs konvensional* | *Nominal* | *—* |
| *Waktu pengeringan gabah* | DV | *Efisiensi pengeringan* | *Lama waktu hingga gabah kering* |*Ratio* | *Menit* |
| *Suhu lingkungan pengering* | CV | *Kondisi lingkungan pengering* | *Temperatur ruang pengering* | *Interval* | *°C* |

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [✓] Tidak
> Jika ya, di mana? ____________________________________

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | *5* | *Waktu pengeringan secara langsung merepresentasikan efisiensi sistem* |
| Sensitive | *4* | *Perubahan performa sistem dapat terlihat dari selisih waktu pengeringan* |
| Feasible | *5* | *Mudah diukur menggunakan timer dan pencatatan sensor* |

**Apakah perlu secondary metric?** [✓] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Stabilitas suhu dan kelembapan, karena efisiensi tidak hanya diukur dari kecepatan tetapi juga kestabilan proses pengeringan.

**Contoh kasus ceiling effect untuk metrik ini:**
> Jika seluruh metode mampu mengeringkan gabah dalam waktu hampir sama, maka metrik waktu menjadi kurang sensitif membedakan kualitas sistem.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | *Apakah semua data point terkumpul?* | *Ada kemungkinan data sensor hilang saat sistem error* | *Menyimpan data secara berkala dan backup data* |
| Consistency | *Apakah ada kontradiksi internal?* | *Sensor dapat menghasilkan pembacaan tidak stabil* | *Kalibrasi sensor sebelum pengujian* |
| Validity | *Apakah benar-benar mengukur yang dimaksud?* | *Sensor DHT11 cukup merepresentasikan suhu dan kelembapan* | *Membandingkan hasil sensor dengan alat ukur standar* |
| Representativeness | *Apakah sampel mewakili populasi target?* | *Pengujian masih skala prototype* | *Menggunakan beberapa sampel gabah berbeda* |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data dianggap p-hacking karena peneliti dapat memilih hasil yang paling menguntungkan sehingga penelitian menjadi bias dan tidak objektif.
> Berbeda dengan eksplorasi data yang sah, eksplorasi dilakukan untuk menemukan pola tambahan dan tetap dilaporkan sebagai temuan eksploratif, bukan sebagai bukti utama hipotesis penelitian.
# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [x] Semua skenario tercakup
  [x] Jumlah run sesuai rencana
  [ ] Tidak ada file output hilang
  Missing: 1 dari 20 data points

Format Consistency:
  [x] Semua file format sama (CSV/JSON/...)
  [x] Header konsisten
  [x] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [x] Nilai dalam range masuk akal
  [x] Tidak ada waktu negatif
  [x] Metrik 0–100%, tidak di luar range
  Anomali ditemukan: terdapat satu run dengan nilai akurasi/stabilitas sistem yang turun cukup jauh dibanding run lainnya

Cross-Validation:
  [x] Run identik → hasil mendekati
  [x] Trend konsisten dengan ekspektasi teori

Keputusan:
  [ ] Data siap analisis
  [x] Perlu cleaning
  [x] Perlu re-run (skenario: re-run pada pengujian pengeringan otomatis yang datanya tidak lengkap dan run yang memiliki nilai terlalu rendah)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| Pengujian sensor DHT11 | 5 | 5 | 0 | Semua data suhu dan kelembapan berhasil tercatat |
| Pengujian kontrol kipas dan motor | 5 | 5 | 0 | Sistem kontrol berjalan dan log berhasil tersimpan |
| Pengujian pengeringan otomatis berbasis ESP32 | 5 | 4 | 1 | Pada salah satu run, data tidak tersimpan dengan lengkap karena koneksi rangkaian sempat tidak stabil |
| Pengujian pengeringan manual/konvensional | 5 | 5 | 0 | Semua proses pengamatan berhasil dicatat secara manual |

**Total expected:** 20 | **Total actual:** 19 | **Missing:** 1

**Keputusan untuk data missing:** 
> Data yang hilang tidak langsung diganti atau dibuat perkiraan, karena bisa memengaruhi hasil analisis. Run yang hilang perlu dilakukan ulang dengan kondisi yang sama, seperti berat padi, durasi pengeringan, posisi sensor, dan kondisi ruang pengering yang dibuat tetap. Setelah re-run selesai, data baru dicatat dengan keterangan bahwa data tersebut merupakan pengulangan dari run yang gagal.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

| Run | Accuracy (%) |
|-----|-------------|
| 1 | *91.2* |
| 2 | *90.8* |
| 3 | *91.5* |
| 4 | *78.3* |
| 5 | *91.0* |

**Deteksi outlier:**
- Q1 = 90.8 | Q3 = 91.2 | IQR = Q3
- Batas bawah (Q1 - 1.5×IQR) = 90.8 - 1.5 × 0.4 = 90.2
- Batas atas (Q3 + 1.5×IQR) = Q3 + 1.5 × IQR 
- Outlier terdeteksi: 91.2 + 1.5 × 0.4 = 91.8

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| *Run 4* | *78.3* | *Contoh: thermal throttling setelah 3 run berturut* | *Re-run dengan cooling interval* |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 95% data terkumpul
**2. Format:** [x] Konsisten / [ ] Ada inkonsistensi: ____
**3. Range check (anomali):** Dari hasil pengecekan, sebagian besar data masih berada dalam range yang masuk akal. Nilai suhu, kelembapan, dan waktu pengeringan tidak menunjukkan angka negatif atau nilai yang tidak mungkin.

Namun, terdapat satu anomali pada Run 4 dengan nilai akurasi/stabilitas sistem sebesar 78.3%. Nilai ini jauh lebih rendah dibandingkan run lainnya yang berada di sekitar 90–91%. Setelah dihitung menggunakan metode IQR, Run 4 masuk sebagai outlier.

Kemungkinan penyebabnya adalah gangguan pada sensor, koneksi kabel, relay, atau kerja kipas yang kurang stabil saat proses pengujian.
**4. Logic check:** [x] Parameter sesuai plan / [ ] Ada ketidaksesuaian: ____

**Kesimpulan:** [ ] Data siap analisis / [x] Perlu tindakan: ____

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> Menurut saya, “data yang benar” dan “data yang dipercaya” itu tidak selalu sama. Data yang benar bisa saja berarti angka yang muncul memang berasal dari alat atau sistem. Misalnya sensor DHT11 membaca suhu 35°C dan kelembapan 70%. Namun, angka itu belum tentu langsung bisa dipercaya, karena bisa saja sensor sedang error, kabel longgar, posisi sensor kurang tepat, atau sistem logging tidak mencatat data dengan benar.

> Sedangkan data yang dipercaya adalah data yang sudah melewati proses pemeriksaan. Artinya, data tersebut sudah dicek dari sisi kelengkapan, format, range nilai, dan kesesuaiannya dengan desain eksperimen. Jadi, data tidak hanya sekadar ada, tetapi juga bisa dipertanggungjawabkan.

> Proses validasi formal tetap diperlukan meskipun data dikumpulkan secara otomatis. Hal ini karena sistem otomatis juga bisa mengalami kesalahan. Misalnya sensor salah membaca, ESP32 gagal menyimpan data, relay tidak merespon, atau file log tidak lengkap. Kalau data seperti itu langsung dipakai untuk analisis, hasil penelitian bisa menjadi kurang akurat.

> Dalam penelitian sistem pengering padi otomatis, validasi data sangat penting karena hasil pengujian akan digunakan untuk menilai apakah alat benar-benar bekerja dengan baik atau tidak. Tanpa validasi, peneliti bisa saja mengambil kesimpulan yang keliru. Oleh karena itu, setiap data perlu dicek dulu sebelum dianggap layak untuk dianalisis.


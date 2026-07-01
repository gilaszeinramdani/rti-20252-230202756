# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     | Pengeringan manual/konvensional | 42 | Berat padi 1 kg, tanpa kontrol otomatis, suhu lingkungan dicatat | Planned | 60 menit | log_manual_run_001.csv |
| 2     | Pengeringan manual/konvensional | 123 | Padi 1 kg, tanpa ESP32, suhu lingkungan dicatat | Planned | 60 menit | log_manual_run_002.csv |
| 3     | Pengeringan manual/konvensional | 314 | Padi 1 kg, tanpa ESP32, suhu lingkungan dicatat | Planned | 60 menit | log_manual_run_003.csv |
| 4     | Pengeringan manual/konvensional | 777 | Padi 1 kg, tanpa ESP32, suhu lingkungan dicatat | Planned | 60 menit | log_manual_run_004.csv |

Jumlah runs per skenario : 5 run
Total runs               : 10 run

DATA LOG (per run):
  Run ID    : run-001
  Timestamp : 2026-03-15T10:00:00
  Skenario  : Pengeringan manual/konvensional
  Input     : Padi 1 kg, suhu lingkungan dicatat, tanpa kontrol otomatis
  Output    : Data suhu lingkungan, lama pengeringan, dan kondisi akhir padi
  Anomali   : Diisi jika ada kendala, misalnya cuaca berubah atau suhu tidak stabil
  Catatan   : Pengeringan dilakukan tanpa bantuan sistem otomatis
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1     | Pengeringan manual/konvensional       | 42   | Padi 1 kg, tanpa ESP32, suhu lingkungan dicatat | Planned | 60 menit  | log_manual_run_001.csv   |
| 2     | Pengeringan manual/konvensional       | 123  | Padi 1 kg, tanpa ESP32, suhu lingkungan dicatat | Planned | 60 menit  | log_manual_run_002.csv   |
| 3     | Pengeringan manual/konvensional       | 314  | Padi 1 kg, tanpa ESP32, suhu lingkungan dicatat | Planned | 60 menit  | log_manual_run_003.csv   |
| 4     | Pengeringan manual/konvensional       | 777  | Padi 1 kg, tanpa ESP32, suhu lingkungan dicatat | Planned | 60 menit  | log_manual_run_004.csv   |
| 5     | Pengeringan manual/konvensional       | 2026 | Padi 1 kg, tanpa ESP32, suhu lingkungan dicatat | Planned | 60 menit  | log_manual_run_005.csv   |
| 6     | Pengeringan otomatis berbasis ESP32   | 42   | Padi 1 kg, DHT11, relay, kipas, motor, LCD      | Planned | 60 menit  | log_esp32_run_001.csv    |
| 7     | Pengeringan otomatis berbasis ESP32   | 123  | Padi 1 kg, DHT11, relay, kipas, motor, LCD      | Planned | 60 menit  | log_esp32_run_002.csv    |
| 8     | Pengeringan otomatis berbasis ESP32   | 314  | Padi 1 kg, DHT11, relay, kipas, motor, LCD      | Planned | 60 menit  | log_esp32_run_003.csv    |
| 9     | Pengeringan otomatis berbasis ESP32   | 777  | Padi 1 kg, DHT11, relay, kipas, motor, LCD      | Planned | 60 menit  | log_esp32_run_004.csv    |
| 10    | Pengeringan otomatis berbasis ESP32   | 2026 | Padi 1 kg, DHT11, relay, kipas, motor, LCD      | Planned | 60 menit  | log_esp32_run_005.csv    |

**Total skenario:** 2 skenario
**Run per skenario:** 5 run
**Total run keseluruhan:** 10 run

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | run-001 |
| Timestamp | 2026-03-15T08:00:00 |
| Skenario | Pengeringan otomatis berbasis ESP32 |
| Nama Penguji | Kelompok 1 |
| Lokasi Pengujian | Ruang pengujian prototype |
| Status Run | Success / Failed / Anomaly |
| Output File | log_esp32_run_001.csv |

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed | 42 |
| Code version | v1.0-program-esp32 |
| Mikrokontroler | ESP32 Type C |
| Sensor | DHT11 |
| Aktuator | Relay, kipas, dan motor dinamo |
| Display | LCD 16x2 |
| Berat Padi | 1 kg |
| Metode Pengeringan | Udara panas tidak langsung / indirect heating |
| Interval Pencatatan | Setiap 5 menit |
| Sumber Daya | Power supply 24V dan step down converter |
| Parameter Kontrol | Suhu, kelembapan, status kipas, status motor |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| Suhu ruang pengering | float | 0°C – 80°C |
| Kelembapan ruang pengering | float | 0% – 100% RH |
| Waktu pengeringan | integer / float | 0 – 300 menit |
| Status kipas | string / boolean | ON / OFF |
| Status motor | string / boolean | ON / OFF |
| Respon relay | string | Normal / Delay / Error |
| Kondisi akhir padi | string | Basah / Setengah kering / Kering |
| Anomali | string | Tidak ada / Sensor tidak stabil / Relay error |
| Catatan pengujian | string | Catatan bebas sesuai kondisi saat run |

**Format output:** [x] CSV / [x] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | ESP32 tidak menyala, program tidak berjalan, atau sistem berhenti saat pengujian | Dokumentasikan run sebagai gagal, lalu cek power supply, step down converter, kabel jumper, dan program ESP32. Setelah penyebab ditemukan, lakukan perbaikan dan jalankan ulang pengujian. |
| Hasil ekstrem | Suhu terbaca terlalu tinggi secara tiba-tiba atau kelembapan turun sangat cepat padahal kondisi padi belum berubah banyak | Cek posisi sensor DHT11, pastikan sensor tidak terlalu dekat dengan sumber panas, lalu bandingkan hasil pembacaan dengan kondisi sebenarnya. Data tetap dicatat sebagai anomali. |
| Waktu eksekusi anomali | Waktu pengeringan jauh lebih lama atau lebih cepat dibandingkan run lainnya | Periksa kondisi awal padi, aliran udara panas, kinerja kipas, dan motor dinamo. Jika ada gangguan teknis, run dicatat sebagai anomali dan pengujian dapat diulang setelah perbaikan. |
| Inkonsistensi dengan run lain | Pada run tertentu kipas tidak menyala, padahal kelembapan masih tinggi dan seharusnya sistem aktif | Cek relay, kabel, logika program, dan nilai set point. Jika ditemukan kesalahan pada program atau rangkaian, lakukan perbaikan dan catat perubahan yang dilakukan. |
| Sensor tidak stabil | Nilai suhu dan kelembapan naik turun terlalu cepat dalam waktu singkat | Cek koneksi sensor DHT11, pastikan kabel tidak longgar, beri jeda pembacaan data, dan lakukan pengujian ulang. Jika tetap tidak stabil, sensor perlu diganti atau dikalibrasi ulang. |
| Output tidak tampil | LCD tidak menampilkan suhu, kelembapan, atau status sistem | Periksa sambungan LCD, alamat I2C jika digunakan, dan bagian program untuk tampilan data. Run tetap dicatat karena proses monitoring terganggu. |
| Aktuator tidak merespon | Relay aktif tetapi kipas atau motor tidak menyala | Cek relay, sumber tegangan, kabel ke kipas dan motor, serta beban perangkat. Jika perangkat rusak, ganti komponen dan catat perubahan pada data log. |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Sebelumnya, dalam beberapa tugas atau percobaan, hasil sering hanya diambil dari satu kali pengujian saja. Cara seperti itu memang terlihat lebih cepat, tetapi sebenarnya kurang kuat untuk dijadikan dasar kesimpulan. Kalau hanya satu kali run, hasilnya bisa saja kebetulan bagus atau kebetulan buruk. Misalnya pada alat pengering padi, satu kali percobaan mungkin terlihat berhasil karena suhu stabil, tetapi belum tentu hasil yang sama terjadi pada percobaan berikutnya.
**Yang akan dilakukan berbeda:**
> Ke depannya, pengujian harus dilakukan beberapa kali untuk setiap skenario. Dengan multiple run, hasil penelitian menjadi lebih meyakinkan karena bisa dilihat rata-rata, perbedaan antar percobaan, dan kemungkinan anomali yang muncul. Selain itu, setiap data harus dicatat secara terstruktur, bukan hanya berdasarkan ingatan atau catatan singkat. Dengan cara ini, hasil pengujian sistem pengering padi otomatis berbasis ESP32 akan lebih jelas, rapi, dan lebih kuat ketika dijelaskan dalam laporan maupun saat presentasi.

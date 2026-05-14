# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Sistem Pengering Padi Otomatis Berbasis ESP32 dan IoT
Database   : Google Scholar, ResearchGate
Query      : ("pengering gabah" OR "pengering padi") AND ("ESP32" OR "IoT") AND ("sensor suhu" OR "kelembapan")
Tahun      : 2025–2026
Hasil awal : 18 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|Adham et al.|2026|ESP32 + IoT + DHT22|Suhu & kelembapan|Monitoring real-time dan kontrol kipas otomatis|Belum ada optimasi distribusi panas|
|Amin & Arrahimi|2025|Rotary Dryer berbasis IoT|DHT22|Kadar air turun hingga 14% dalam ±22 menit|Sistem mekanik kompleks|

Pola yang ditemukan:
  Metode dominan     : ESP32 sebagai mikrokontroler utama
                       Sensor DHT11/DHT22
                       Sistem kontrol otomatis berbasis relay
                       Monitoring IoT real-time
  Dataset umum       : Suhu udara
                       Kelembapan udara
                       Kadar air gabah
  Limitasi berulang  : Monitoring tanpa kontrol otomatis
                       Distribusi panas belum optimal
                       Ketergantungan pada sensor sederhana
                       Belum banyak implementasi skala nyata

GAP IDENTIFICATION

Gap 1: [Jenis: method]
  Deskripsi    : Sebagian penelitian hanya fokus pada monitoring suhu dan kelembapan tanpa integrasi kontrol otomatis heater dan kipas secara adaptif.
  Bukti        : Penelitian Nuhdi (2025) hanya melakukan monitoring kadar air tanpa pengendalian otomatis sistem pengering.
  Signifikansi : Tanpa kontrol otomatis, proses pengeringan tetap membutuhkan intervensi manual sehingga efisiensi sistem belum optimal.

Gap 2: [Jenis: Context + Performance]
  Deskripsi    : Sebagian besar penelitian masih berbentuk prototype laboratorium dan belum diuji pada kondisi pengeringan nyata dengan perubahan suhu lingkungan yang dinamis.
  Bukti        : Penelitian sebelumnya lebih fokus pada simulasi atau prototype kecil dengan parameter terbatas.
  Signifikansi : Sistem yang stabil pada lingkungan nyata lebih dibutuhkan petani dibanding sistem yang hanya berhasil pada kondisi ideal laboratorium.

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|ESP32 + DHT22 Monitoring System|Task sama: monitoring pengering gabah|Dipakai pada banyak penelitian IoT|Adham et al., 2026|
|Rotary Dryer IoT|Sama-sama pengering otomatis|Metode umum pada pengering modern|Amin & Arrahimi, 2025|
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Sistem Pengering Padi Otomatis Berbasis ESP32 Menggunakan Sensor Suhu dan Kelembapan
**Query pencarian:** ("pengering gabah" OR "pengering padi") AND ("ESP32" OR "IoT") AND ("sensor suhu" OR "kelembapan")
**Database:** Google Scholar, ResearchGate

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | *Adham et al.* | *2026* | *ESP32 + DHT22 + IoT* | *Data suhu & kelembapan* | *Monitoring real-time dan kontrol kipas otomatis* | *Distribusi panas belum optimal* |
| 2 | *Amin & Arrahimi* |*2025* | *Rotary Dryer berbasis IoT* | *Data kadar air gabah* | *Kadar air turun hingga 14% dalam ±22 menit* | *Sistem mekanik kompleks* |
| 3 | *Nuhdi* | *2025* | *Monitoring IoT berbasis moisture sensor* | *Data kadar air* | *Monitoring kadar air lebih akurat* | *Tidak ada kontrol otomatis* |
| 4 | *Oktavois & Gunawan* | *2026* | *ESP32 + kontrol ON-OFF* | *Suhu dan kelembapan* | *Kadar air turun dari 55% ke 12%* | *Belum mendukung monitoring internet* |
| 5 | *Penelitian yang diusulkan* | *2026* | *ESP32 + DHT11 + relay otomatis* | *Suhu dan kelembapan ruang pengering* | *Kontrol heater dan kipas otomatis* | *Masih tahap prototype* |

**Pola yang terlihat — Metode dominan:** ESP32 sebagai mikrokontroler utama
                                         Sensor DHT11/DHT22
                                         Sistem kontrol otomatis berbasis relay
                                         Monitoring berbasis IoT
**Limitasi yang berulang:** Sistem masih berupa prototype
                            Monitoring tanpa kontrol otomatis penuh
                            Distribusi panas belum stabil
                            Pengujian masih terbatas pada skala kecil

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [✓] Ya / [ ] Tidak | *Stabilitas suhu dan distribusi udara panas masih belum optimal* |
| Method Gap | [✓] Ya / [ ] Tidak | *Banyak penelitian hanya fokus pada monitoring tanpa kontrol otomatis adaptif* |
| Data Gap | [✓] Ya / [ ] Tidak | *Dataset pengujian masih terbatas pada prototype laboratorium* |
| Context Gap | [✓] Ya / [ ] Tidak | *Belum banyak pengujian pada kondisi lingkungan nyata dan skala petani* |

**Gap utama yang dipilih:** Method + Context
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Karena sebagian penelitian hanya mampu melakukan monitoring tanpa pengendalian otomatis secara real-time. Selain itu, pengujian sistem masih terbatas pada kondisi laboratorium sehingga belum diketahui kestabilannya pada lingkungan nyata. Penelitian ini penting untuk meningkatkan efisiensi pengeringan dan mengurangi ketergantungan terhadap cuaca.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | *ESP32 + DHT22 IoT Monitoring* | *Mengatasi masalah pengeringan gabah otomatis* | *Banyak digunakan pada penelitian IoT* | *Bukan, tetapi common practice* | *Adham et al., 2026* |
| 2 | *Rotary Dryer berbasis IoT* | *Fokus pada efisiensi pengeringan gabah* | *Metode populer pada pengering modern* | *Hampir SOTA* | *Amin & Arrahimi, 2025* |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [✓] Tidak
> Justifikasi: Baseline dipilih dari penelitian yang relevan dengan topik yang sama, menggunakan metode modern yang umum dipakai, serta memiliki tujuan serupa yaitu otomatisasi pengeringan gabah berbasis IoT.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Klaim “belum ada yang meneliti ini” hanya berupa asumsi tanpa bukti pencarian literatur yang jelas. Sedangkan research gap yang valid harus didukung dengan analisis beberapa penelitian sebelumnya untuk menemukan kelemahan, keterbatasan, atau masalah yang belum terselesaikan.
> Gap dapat dibuktikan melalui pencarian sistematis menggunakan database akademik, kemudian membandingkan metode, hasil, dan limitasi dari beberapa paper sehingga ditemukan pola kekurangan yang konsisten.

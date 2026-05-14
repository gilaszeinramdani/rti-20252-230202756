# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Internet of Things (IoT), Embedded System, Otomasi Pertanian
  Konteks  : Sistem pengering padi otomatis berbasis ESP32 untuk membantu proses pengeringan gabah secara efisien dan stabil

System Context
  Input       : Data suhu dan kelembapan dari sensor DHT11
  Process     : ESP32 memproses data sensor dan mengontrol relay, kipas, serta heater
  Output      : Kipas dan heater aktif/nonaktif secara otomatis, data tampil pada LCD
  Outcome     : Proses pengeringan lebih cepat, stabil, dan tidak bergantung cuaca
  Constraints : Keterbatasan daya listrik, akurasi sensor, kapasitas alat, kestabilan jaringan IoT
  Stakeholders: Petani, peneliti, pengelola pengering gabah

Fenomena → Problem
  Fenomena yang diamati             : Pengeringan gabah masih dilakukan secara konvensional menggunakan sinar matahari
  Gejala (symptom) yang terukur     : Waktu pengeringan lama, suhu tidak stabil, kadar air sulit dikontrol
  Masalah yang didiagnosis          : Tidak adanya sistem otomatis untuk monitoring dan pengendalian suhu serta kelembapan
  Masalah riset (researchable)      : Belum diketahui efektivitas sistem pengering gabah otomatis berbasis ESP32 dalam menjaga kestabilan suhu dan mempercepat proses pengeringan
  Variabel yang terukur             : Suhu, kelembapan, waktu pengeringan, kestabilan sistem, efisiensi pengeringan

Problem Quality Check
  [✓] Clarity — Masalah dijelaskan secara spesifik
  [✓] Measurability — Memiliki variabel kuantitatif seperti suhu dan waktu
  [✓] Relevance — Penting pada bidang pertanian dan IoT
  [✓] Testability — Dapat diuji melalui eksperimen prototype
  [✓] Impact — Berpotensi meningkatkan efisiensi pengeringan gabah

Problem Statement (1 paragraf):
  Proses pengeringan gabah secara konvensional masih bergantung pada kondisi cuaca sehingga menyebabkan waktu pengeringan menjadi lama dan kualitas gabah sulit dikontrol. Selain itu, tidak adanya sistem monitoring suhu dan kelembapan secara otomatis mengakibatkan proses pengeringan kurang stabil dan efisien. Penelitian ini berfokus pada perancangan dan pengujian sistem pengering padi otomatis berbasis Espressif Systems ESP32 menggunakan sensor DHT11 untuk mengetahui efektivitas sistem dalam mengontrol suhu dan kelembapan secara real-time guna meningkatkan efisiensi dan kestabilan proses pengeringan gabah.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** ________________________________________

| Tahap | Hasil |
|-------|-------|
| Reality | *Pengeringan gabah masih menggunakan sinar matahar* |
| Observed Issue (Symptom) | *Pengeringan memerlukan waktu lama dan kadar air tidak stabil* |
| Diagnosed Problem (Root Cause) | *Tidak ada sistem otomatis untuk mengontrol suhu dan kelembapan* |
| Researchable Problem | *Bagaimana efektivitas ESP32 dan sensor DHT11 dalam sistem pengering gabah otomatis* |
| Measurable Variable | *Suhu, kelembapan, waktu pengeringan, efisiensi alat* |

**Apakah terjebak solution-first thinking?** [ ] Ya / [✓] Tidak

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | *Data sensor suhu dan kelembapan* |
| Process | *Pengolahan data oleh ESP32 dan pengendalian relay* |
| Output | *Aktivasi kipas dan heater otomatis* |
| Outcome | *Pengeringan lebih cepat dan stabil* |
| Constraints | *Daya listrik, akurasi sensor, kondisi lingkungan* |
| Stakeholders | *Petani dan pengguna alat* |

**Komponen mana yang paling relevan dengan masalah riset?** Process, karena inti penelitian berada pada pengolahan data sensor dan kontrol otomatis.

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | *5* | *Masalah dan tujuan dijelaskan jelas* |
| Measurability | *5* | *Variabel dapat diukur secara kuantitatif* |
| Relevance | *5* | *Relevan untuk IoT dan pertanian* |
| Testability | *4* | *Bisa diuji melalui prototype dan eksperimen* |
| Impact | *5* | *Berpotensi meningkatkan efisiensi pengeringan* |

**Skor total:** 24 / 25

**Problem statement versi final (1 paragraf):**
> Proses pengeringan gabah konvensional masih memiliki kelemahan berupa ketergantungan terhadap cuaca, waktu pengeringan yang lama, dan sulitnya menjaga kestabilan suhu serta kelembapan. Kondisi tersebut menyebabkan kualitas gabah menjadi tidak optimal dan efisiensi kerja menurun. Oleh karena itu, penelitian ini merancang sistem pengering padi otomatis berbasis ESP32 dan sensor DHT11 untuk memonitor serta mengontrol suhu dan kelembapan secara real-time guna meningkatkan efektivitas dan kestabilan proses pengeringan gabah.

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah pada coding umumnya berupa bug, error, atau fitur yang belum berjalan sesuai fungsi sehingga fokus utamanya adalah memperbaiki sistem agar dapat bekerja. Sedangkan masalah riset lebih berfokus pada menemukan gap pengetahuan, memahami penyebab suatu fenomena, dan membuktikan sesuatu melalui metode ilmiah. Dalam riset, masalah harus terukur, dapat diuji, memiliki batasan yang jelas, dan menghasilkan kontribusi pengetahuan baru, bukan sekadar membuat sistem berjalan.

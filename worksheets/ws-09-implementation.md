# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Intel(R) Core(TM) i3-1005G1 CPU @ 1.20GHz (1.19 GHz)
  RAM     : 12.0 GB (11.8 GB usable)
  GPU     : Intel(R) UHD Graphics 128 MB
  Storage : SSD 256 GB

Software:
  OS        : Windows 11 Pro
  Runtime   : Arduino IDE 2.x
  Framework : Arduino Framework untuk ESP32

Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
| ESP32 Board Package | 3.x |Arduino Board Manager | Disesuaikan saat instalasi |
| DHT Sensor Library | 1.x |Arduino Library Manager | Disesuaikan saat instalasi |

Konfigurasi:
  Config file     : config.h atau pengaturan langsung pada program Arduino
  Random seed     : Tidak digunakan untuk proses utama, karena sistem membaca data sensor secara langsung
  Hyperparameters : Batas suhu, batas kelembapan, interval pembacaan sensor, dan kondisi aktif relay

Reproducibility Check:
  [v] Dependency terdokumentasi (requirements.txt / lock file)
  [-] Seed ditetapkan di semua level (Python, NumPy, framework)
  [v] Config di version control
  [v] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | *Intel(R) Core(TM) i3-1005G1 CPU @ 1.20GHz (1.19 GHz)* |
| RAM | *12.0 GB (11.8 GB usable)* |
| GPU | *Intel(R) UHD Graphics 128 MB* |
| OS | *Windows 11 Pro* |
| Runtime |Arduino IDE 2.x|
| Framework |Arduino Framework untuk ESP32|
| Random Seed |Tidak digunakan, karena sistem berbasis pembacaan sensor real-time|

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| *ESP32 Board Package* | *3.x* | *Digunakan agar Arduino IDE dapat mengenali dan memprogram board ESP32* |
| *DHT Sensor Library* | *1.x* | *Digunakan untuk membaca data suhu dan kelembapan dari sensor DHT11* |
| *Adafruit Unified Sensor* | *1.x* | *Library pendukung agar pembacaan sensor dapat berjalan lebih stabil* |
| *LiquidCrystal_I2C* | *1.x* | *Digunakan untuk menampilkan data suhu, kelembapan, dan status sistem pada LCD* |
| *WiFi Library ESP32 | *Bawaan ESP32* | *Digunakan apabila sistem dikembangkan untuk monitoring berbasis IoT* |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | *Tidak digunakan* | *Suhu, kelembapan, status kipas, dan status motor* | — |
| 2 | *Tidak digunakan* | *Suhu, kelembapan, status kipas, dan status motor* | [v] Ya / [ ] Tidak |
| 3 | *Tidak digunakan* | *Suhu, kelembapan, status kipas, dan status motor* | [v] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**

Jika hasil pengujian pada setiap run berbeda, kemungkinan penyebabnya berasal dari kondisi lingkungan dan kestabilan perangkat yang digunakan. Pada sistem pengering padi otomatis berbasis ESP32, data yang dibaca berasal dari sensor DHT11, sehingga nilai suhu dan kelembapan dapat berubah apabila kondisi ruang pengering tidak benar-benar sama pada setiap percobaan.

Perbedaan hasil juga dapat disebabkan oleh posisi sensor yang kurang tepat, aliran udara panas dari kipas yang tidak merata, atau sumber panas yang tidak stabil. Selain itu, tegangan dari power supply juga perlu diperhatikan karena tegangan yang tidak stabil dapat memengaruhi kerja ESP32, relay, kipas, motor dinamo, dan LCD.

Faktor lain yang mungkin terjadi adalah kondisi padi yang diuji tidak sama, misalnya jumlah padi berbeda, tingkat kelembapan awal berbeda, atau posisi padi di dalam ruang pengering tidak merata. Oleh karena itu, setiap percobaan perlu menggunakan konfigurasi alat, jumlah padi, posisi sensor, dan kondisi ruang pengering yang sama agar hasil pengujian lebih konsisten.

___________________________________________________

**Checklist kontrol yang sudah diterapkan:**
- [v] Random seed di-set di semua level
- [v] Tidak ada background process yang mengganggu
- [v] Cache dibersihkan antar-run
- [v] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Implementasi Sistem Pengering Padi Otomatis Berbasis ESP32 Menggunakan Sensor Suhu dan Kelembapan

## 1. Environment
> (Eksperimen ini dijalankan menggunakan laptop dengan sistem operasi Windows 11 dan Arduino IDE 2.x sebagai software utama untuk menulis dan mengunggah program ke ESP32. Board yang digunakan adalah ESP32 Type-C. Sistem juga menggunakan sensor DHT11 sebagai pembaca suhu dan kelembapan, relay sebagai pengendali output, kipas sebagai pengalir udara panas, motor dinamo untuk membantu pergerakan padi, serta LCD 16x2 untuk menampilkan informasi sistem.)

## 2. Installation
> (Langkah instalasi yang dilakukan adalah sebagai berikut:

Menginstal Arduino IDE pada laptop.
Menambahkan board ESP32 melalui Board Manager.
Menginstal library yang dibutuhkan, yaitu DHT Sensor Library, Adafruit Unified Sensor, dan LiquidCrystal_I2C.
Menghubungkan ESP32 ke laptop menggunakan kabel USB.
Memilih board ESP32 dan port yang sesuai pada Arduino IDE.
Mengunggah program ke ESP32.)

## 3. Data
> (Data yang digunakan dalam eksperimen ini berupa data hasil pembacaan sensor secara langsung. Data utama yang dicatat adalah suhu, kelembapan, status kipas, status motor, dan waktu pembacaan. Data tersebut diperoleh dari sensor DHT11 yang ditempatkan pada ruang pengering padi.

Format data yang diharapkan dapat berupa tabel sederhana, misalnya:

Waktu | Suhu | Kelembapan | Status Kipas | Status Motor

Data ini digunakan untuk melihat apakah sistem mampu menjaga kondisi ruang pengering agar tetap stabil selama proses pengeringan berlangsung.)

## 4. Execution
> (Eksperimen dijalankan dengan langkah berikut:

Merangkai ESP32, sensor DHT11, relay, kipas, motor, LCD, dan power supply sesuai rancangan.
Menghubungkan ESP32 ke laptop.
Membuka file program pada Arduino IDE.
Mengatur nilai batas suhu dan kelembapan pada program.
Mengunggah program ke ESP32.
Menyalakan sistem dan mengamati pembacaan sensor pada LCD.
Mencatat perubahan suhu, kelembapan, dan respon output selama proses pengeringan.)

## 5. Configuration
> (Konfigurasi utama yang digunakan dalam eksperimen ini meliputi batas suhu, batas kelembapan, interval pembacaan sensor, dan kondisi aktif relay. Nilai konfigurasi harus dicatat agar percobaan dapat diulang dengan kondisi yang sama.

Contoh konfigurasi:

Batas suhu minimum     : 35°C
Batas suhu maksimum    : 45°C
Batas kelembapan       : 60%
Interval pembacaan     : 2 detik
Output utama           : kipas dan motor dinamo
Sensor utama           : DHT11

Konfigurasi tersebut dapat disesuaikan dengan kebutuhan pengujian, tetapi setiap perubahan harus dicatat agar hasil eksperimen tetap jelas dan bisa dibandingkan.)

## 6. Expected Output
> (Output yang diharapkan dari eksperimen ini adalah sistem mampu membaca suhu dan kelembapan secara real-time, kemudian memberikan respon otomatis sesuai kondisi yang terdeteksi. Jika kelembapan masih tinggi, kipas akan aktif untuk membantu proses pengeringan. Jika suhu terlalu tinggi, sistem akan menyesuaikan kerja kipas agar suhu tetap stabil. Motor dinamo juga dapat membantu pergerakan padi agar proses pengeringan lebih merata.

Contoh output yang diharapkan:

Suhu: 38°C
Kelembapan: 58%
Kipas: ON
Motor: ON
Status: Pengeringan berjalan

Dengan output tersebut, pengguna dapat mengetahui kondisi ruang pengering tanpa harus mengecek secara manual terus-menerus.)
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?
Menurut saya, eksperimen ini sudah mulai bisa diulang oleh orang lain, tetapi belum sepenuhnya bisa disebut reproducible jika dokumentasi teknisnya belum lengkap. Beberapa bagian seperti daftar library, versi Arduino IDE, konfigurasi batas suhu dan kelembapan, serta skema rangkaian harus ditulis dengan jelas agar orang lain dapat membuat sistem yang sama.

Saat ini eksperimen lebih dekat ke tahap repeatability, karena sistem dapat diuji ulang pada alat dan lingkungan yang sama. Namun, untuk mencapai reproducibility, masih diperlukan dokumentasi yang lebih lengkap, seperti file program, diagram rangkaian, daftar komponen lengkap, versi library, serta langkah pengujian yang rinci.
**Level saat ini:** [v] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Komponen yang masih perlu dilengkapi adalah versi library secara pasti, gambar rangkaian lengkap, file konfigurasi program, dokumentasi hasil pengujian, serta standar kondisi lingkungan saat percobaan dilakukan. Selain itu, perlu juga dibuat tabel hasil pengujian agar data suhu, kelembapan, dan respon sistem dapat dibandingkan dengan lebih jelas.

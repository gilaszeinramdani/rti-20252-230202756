# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : RANCANG BANGUN SISTEM PENGERING PADI OTOMATIS BERBASIS ESP 32 MENGGUNAKAN SENSOR SUHU DAN KELEMBAPAN
Tanggal          : 5 Mei 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Apakah pengujian dilakukan pada kondisi yang berbeda dan data yang cukup?
   - Data yang dibutuhkan untuk verifikasi: Dataset pengujian, jumlah sampel, kondisi eksperimen, dan hasil perbandingan metode lain.

2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [✓] Design Science  [ ] Mixed
   - Alasan: Penelitian berfokus pada pembuatan sistem pengering padi otomatis berbasis ESP32 untuk menguji efektivitas alat dalam menjaga suhu dan kelembapan.

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Sensor DHT11 dianggap selalu akurat dalam membaca suhu dan kelembapan.
   - Sumber bias potensial:  Pengujian hanya dilakukan pada satu kondisi lingkungan.
   - Langkah mitigasi: Melakukan pengujian pada beberapa kondisi cuaca dan lokasi berbeda.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Data suhu, kelembapan, dan hasil pengeringan.
   - Batasan yang diakui sejak awal: Sistem masih berupa prototype dan belum diuji dalam skala industri.
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

> **Panduan pencarian paper:** Gunakan [IEEE Xplore](https://ieeexplore.ieee.org), [ACM Digital Library](https://dl.acm.org), atau Google Scholar. Pilih paper **tahun 2020 ke atas**, di topik yang Anda minati: deteksi anomali, klasifikasi citra, NLP, keamanan siber, IoT, dsb.
>
> **Contoh domain TI:** "Deteksi anomali lalu-lintas jaringan menggunakan CNN — akurasi meningkat 94% vs baseline SVM 87%." Distorsi potensial: apakah dataset normal/anomali seimbang? Apakah hanya diuji pada satu vendor traffic?

**Paper yang dipilih:**
> Judul: Rancang Bangun Sistem Pengering Padi Otomatis Berbasis ESP32 Menggunakan Sensor Suhu dan Kelembapan
> Penulis (Tahun): Kelompok 1 Universitas Putra Bangsa (2026)
> Sumber/Link DOI: Dokumen penelitian internal/prototype

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | *Mengumpulkan data suhu dan kelembapan menggunakan sensor DHT11* | *CSensor kurang akurat pada kondisi tertentu* |
| Data → Processing | *Data diproses oleh ESP32* | *Kesalahan pembacaan akibat noise sensor* |
| Processing → Analysis | *Membandingkan suhu dengan batas minimum* | *Nilai batas mungkin tidak sesuai semua kondisi* |
| Analysis → Inference | *Menentukan kipas aktif atau tidak* | *Kesimpulan terlalu bergantung pada satu sensor* |
| Inference → Knowledge | *Menyimpulkan sistem efektif untuk pengeringan padi* | *Belum diuji pada skala besar* |

**Distorsi paling besar di tahap:** Reality → Data

**Dua distorsi spesifik yang teridentifikasi:**
1. Akurasi sensor DHT11 dapat berubah karena lingkungan.
2. Pengujian hanya dilakukan pada prototype sederhana.

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | *Peneliti harus melaporkan hasil dengan dan tanpa outlier* |
| Transparansi | *Alasan penghapusan data harus dijelaskan secara terbuka* |
| Peer review | *Reviewer dapat mengevaluasi apakah outlier memang kesalahan data atau bagian dari fenomena* |

**Keputusan akhir dan justifikasi:**
> Data outlier tidak boleh langsung dihapus hanya untuk mendapatkan hasil signifikan. Peneliti harus menjelaskan penyebab outlier dan melaporkan kedua hasil agar penelitian tetap objektif dan transparan.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** ________________________________________

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | *4 — menggunakan pengujian suhu dan kelembapan* | *1 — tidak fokus pada makna sosial* | *5 — membangun sistem otomatis sebagai artefak* |
| Jenis data yang dikumpulkan | *Data suhu dan kelembapan* | *Observasi pengguna* | *Hasil pengujian alat dan performa sistem* |
| Limitasi paradigma | *Sulit menangkap faktor lingkungan* | *Data subjektif* | *Fokus lebih pada artefak dibanding teori* |

**Paradigma yang dipilih:** Design Science Research
**Alasan:** Penelitian berfokus pada perancangan dan pengujian sistem otomatis berbasis ESP32 untuk menyelesaikan masalah pengeringan padi.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum membaca materi ini, saya hanya melihat angka akurasi sebagai bukti keberhasilan penelitian. Setelah memahami rantai distorsi, saya menyadari bahwa data, metode pengujian, dan kondisi eksperimen sangat mempengaruhi hasil penelitian. Sekarang saya akan mempertanyakan bagaimana data dikumpulkan, apakah pengujian adil, dan apakah hasil dapat diterapkan pada kondisi lain.

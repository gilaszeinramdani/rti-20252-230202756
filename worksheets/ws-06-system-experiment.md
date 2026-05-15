# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: Bagaimana penerapan sistem pengering padi otomatis berbasis ESP32 dan sensor suhu–kelembapan dapat meningkatkan efisiensi serta kestabilan proses pengeringan padi dibanding metode konvensional?

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|Metode kontrol otomatis suhu & kelembapan|IV|Program kontrol ESP32 + relay|Mengubah nilai set point suhu/kelembapan pada program|
|Efisiensi waktu pengeringan|DV|Modul monitoring waktu|Mengukur lama proses pengeringan|
|Kondisi ruang pengering|CV|Ruang pengering prototype|Tidak diubah selama eksperimen|

4 Prinsip Desain:
  [✓] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [✓] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [✓] Measurement Integration — Pengukuran DV built-in
  [✓] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     : Data suhu dan kelembapan dari sensor DHT11/DHT22
  Parameter      : Set point suhu, kelembapan, waktu pengeringan
  Output format  : Nilai suhu, kelembapan, status relay, waktu pengeringan
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Bagaimana sistem pengering padi otomatis berbasis ESP32 dapat menjaga suhu dan kelembapan agar proses pengeringan lebih efisien?

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| *Kontrol otomatis suhu* | *IV* | *ESP32 + relay* | *Mengubah set point suhu* |
| *Waktu pengeringan* | *DV* | *Timer/log sistem* | *Mengukur durasi pengeringan* |
| *Jenis sensor* | *CV* | *DHT11* | *Tidak diubah* |

**Apakah semua variabel bisa di-map?** [✓] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? 

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability | *Baik* | *Setiap komponen sistem memiliki hubungan langsung dengan variabel penelitian, misalnya sensor DHT11 untuk variabel suhu dan kelembapan, serta relay untuk kontrol aktuator.* |
| Modularity | *Baik* | *Sistem dibagi menjadi beberapa modul terpisah seperti sensor, ESP32, relay, kipas, heater, dan LCD sehingga mudah diuji atau diganti tanpa memengaruhi seluruh sistem.* |
| Controllability | *Baik* | *Nilai batas suhu dan kelembapan dapat diatur melalui program pada ESP32 sehingga kondisi eksperimen dapat dikontrol.* |
| Measurability | *Baik* | *Sistem mampu menghasilkan data suhu, kelembapan, dan status aktuator secara otomatis melalui sensor dan tampilan LCD secara real-time.* |

**Prinsip mana yang paling sulit dipenuhi?** Measurability
**Strategi untuk mengatasinya:**
> Menambahkan sistem data logging atau penyimpanan otomatis agar seluruh data sensor dapat direkam secara konsisten dan dianalisis dengan lebih akurat selama proses eksperimen berlangsung.

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

> **Panduan jumlah kondisi:** Untuk 3 komponen (A, B, C), kondisi minimal yang direkomendasikan:
> Full + (-A) + (-B) + (-C) = **4 kondisi dasar**. Jika waktu memungkinkan, tambahkan kombinasi ganda: (-A,-B), (-A,-C), (-B,-C) = **7 kondisi**. Sesuaikan dengan *computational cost* dan tenggat waktu penelitian.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full | *Sensor aktif* | *Kipas aktif* | *Heater aktif* | *Sistem bekerja optimal, suhu dan kelembapan stabil* |
| – A | *Sensor dimatikan* | ** | ** | *Sistem tidak dapat membaca kondisi suhu dan kelembapan secara otomatis* |
| – B | ** | *Kipas dimatikan* | ** | *Distribusi udara panas tidak merata sehingga pengeringan lebih lambat* |
| – C | ** | ** | *Heater dimatikan* | *Proses pengeringan kurang maksimal karena tidak ada sumber panas utama* |

**Komponen mana yang diprediksi paling berkontribusi?** Komponen B (Kipas Otomatis)
**Mengapa?**
> Karena kipas berfungsi mendistribusikan udara panas secara merata ke seluruh ruang pengering sehingga suhu lebih stabil dan proses pengeringan padi menjadi lebih cepat serta efisien.

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Sistem monolitik membuat variabel sulit dipisahkan sehingga peneliti tidak dapat mengetahui komponen mana yang benar-benar memengaruhi hasil penelitian. Selain itu, eksperimen menjadi sulit direproduksi karena banyak fitur saling bergantung.

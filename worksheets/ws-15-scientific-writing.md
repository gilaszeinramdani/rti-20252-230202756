# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Rancang Bangun Sistem Pengering Padi Otomatis Berbasis ESP32
          Menggunakan Sensor Suhu dan Kelembapan
Target  : [ ] Jurnal  [ ] Konferensi  [v] Laporan

Section Check:
  [ ] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [v] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [v] Related Work — concept-centric, gap positioning
  [v] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [ ] Results — tabel + grafik + observasi (tanpa interpretasi)
  [ ] Discussion — interpretasi, perbandingan, implikasi, limitation
  [ ] Conclusion — jawaban RQ, kontribusi, future work

Consistency Matrix:
  [v] RQ di Introduction = RQ di Method = RQ di Conclusion
  [v] Variabel di Method = variabel di Results
  [ ] Klaim di Discussion didukung data di Results
  [ ] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [v] Clarity — mudah dipahami tanpa re-read
  [ ] Precision — tidak ada istilah ambigu
  [ ] Conciseness — tidak ada kalimat redundan
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| **Abstract** | Penelitian ini membahas pembuatan prototype pengering padi otomatis untuk mengurangi ketergantungan proses pengeringan terhadap cuaca. Sistem menggunakan ESP32, sensor DHT11, relay, kipas, motor pengaduk, dan LCD. Abstrak memuat hasil utama berupa kestabilan suhu, perubahan kelembapan, waktu pengeringan, dan respons sistem otomatis. | 200–250 |
| **Introduction** | Pengeringan padi secara tradisional masih mengandalkan sinar matahari sehingga prosesnya dipengaruhi kondisi cuaca, membutuhkan waktu lama, dan sulit dikontrol. Penelitian ini mengusulkan penggunaan ESP32 dan sensor suhu serta kelembapan untuk membantu proses pengeringan secara otomatis. Pertanyaan penelitian diarahkan pada proses perancangan sistem dan efektivitas alat dalam menjaga kondisi ruang pengering. | 500–700 |
| **Related Work** | Bagian ini membahas penelitian sebelumnya mengenai pengering gabah berbasis ESP32, IoT, sensor DHT11 atau DHT22, rotary dryer, dan sistem kontrol otomatis. Perbandingan dilakukan berdasarkan masalah, metode, perangkat, dan hasil penelitian. Posisi penelitian ini terletak pada penggunaan ESP32 untuk mengontrol kipas dan motor pengaduk serta menampilkan informasi melalui LCD. | 700–1000 |
| **Method** | Penelitian menggunakan pendekatan Research and Development dengan metode pengembangan Prototype. Tahapan penelitian terdiri dari pengumpulan kebutuhan, perancangan hardware dan software, pembuatan prototype, pengujian, evaluasi, dan perbaikan. Pengujian mencakup sensor DHT11, relay, kipas, motor pengaduk, kestabilan suhu, kelembapan, dan waktu pengeringan. | 800–1200 |
| **Results** | Bagian hasil menyajikan data pembacaan suhu dan kelembapan berdasarkan waktu pengamatan. Data respons relay, kipas, motor pengaduk, dan LCD ditampilkan dalam bentuk tabel. Perbandingan waktu pengeringan otomatis dan manual dapat ditampilkan menggunakan tabel atau grafik tanpa interpretasi panjang. | 500–800 |
| **Discussion** | Bagian ini menjelaskan arti hasil pengujian, seperti kemampuan sistem menjaga suhu, menurunkan kelembapan, dan merespons perubahan kondisi ruang pengering. Hasil sistem otomatis dibandingkan dengan metode manual dan penelitian terdahulu. Pembahasan juga menjelaskan keterbatasan sensor DHT11, sumber panas, ukuran prototype, dan jumlah pengujian. | 600–900 |
| **Conclusion** | Kesimpulan menjawab pertanyaan penelitian berdasarkan data pengujian. Bagian ini menjelaskan apakah prototype berhasil membaca suhu dan kelembapan serta mengontrol kipas dan motor secara otomatis. Pengembangan selanjutnya dapat menggunakan sensor yang lebih akurat, pengukuran kadar air gabah, monitoring internet, dan ruang pengering berkapasitas lebih besar. | 200–400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

|  | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
| **RQ1: Perancangan dan cara kerja sistem** | ✓ | ✓ | ✗ | ✗ | ✗ |
| **RQ2: Efisiensi dibandingkan metode manual** | ✓ | ~ | ✗ | ✗ | ✗ |
| **Metrik suhu** | ✓ | ✓ | ✗ | ✗ | ✗ |
| **Metrik kelembapan** | ✓ | ✓ | ✗ | ✗ | ✗ |
| **Metrik waktu pengeringan** | ✓ | ~ | ✗ | ✗ | ✗ |
| **Respons relay dan perangkat output** | ✓ | ✓ | ✗ | ✗ | ✗ |
| **Variabel IV: jenis sistem pengeringan** | ✓ | ~ | ✗ | ✗ | ✗ |
| **Variabel DV: waktu, suhu, dan kelembapan** | ✓ | ✓ | ✗ | ✗ | ✗ |
| **Klaim sistem lebih efektif dan efisien** | ✓ | ~ | ✗ | ✗ | ✗ |
| **Sensor DHT11 sebagai sensor utama** | ✓ | ~ | ✗ | ✗ | ✗ |
| **Kipas dan motor sebagai output utama** | ✓ | ~ | ✗ | ✗ | ✗ |
| **Suhu pengeringan 40–50°C** | ✓ | ~ | ✗ | ✗ | ✗ |
| **Monitoring berbasis IoT** | ✓ | ~ | ✗ | ✗ | ✗ |

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> > Pertanyaan penelitian mengenai proses perancangan sistem sudah dibahas dalam pendahuluan dan metode. Namun, pertanyaan tersebut belum dapat dijawab sepenuhnya karena bagian hasil, pembahasan, dan kesimpulan belum tersedia.

> Pertanyaan mengenai perbandingan sistem otomatis dan manual belum didukung oleh prosedur pengujian perbandingan yang lengkap. Metode penelitian perlu menjelaskan jumlah gabah, kondisi ruang, lama pengujian, dan cara mengukur hasil pada kedua metode.

> Sensor yang digunakan belum konsisten karena terdapat penyebutan DHT11 dan DHT22. Batas suhu juga tidak sama, yaitu rentang suhu pengeringan 40–50°C dan batas kontrol sistem sebesar 12°C.

> Perangkat output pada bagian perancangan berupa kipas dan motor pengaduk. Namun, pada bagian analisis data masih terdapat penyebutan lampu.

> Penelitian menyebut penggunaan IoT, tetapi implementasi yang ditampilkan masih berfokus pada LCD dan simulasi Wokwi. Belum terdapat platform internet, database, atau dashboard untuk monitoring jarak jauh.

**Tindakan perbaikan:**
> > Sensor utama perlu ditetapkan menggunakan DHT11. Seluruh penyebutan DHT22 yang tidak sesuai dengan alat penelitian perlu diganti menjadi DHT11.

> Batas kontrol 12°C perlu diperbaiki menjadi rentang suhu yang sesuai dengan proses pengeringan padi, yaitu sekitar 40–50°C. Logika kontrol harus menjelaskan kondisi kipas dan motor ketika suhu berada di bawah, di dalam, atau di atas rentang tersebut.

> Perangkat output perlu diseragamkan menjadi relay, kipas, dan motor pengaduk. Lampu cukup disebut sebagai indikator pada simulasi Wokwi dan bukan sebagai output utama alat.

> Pengujian perlu dilakukan dalam dua kondisi, yaitu pengeringan manual sebagai kelompok kontrol dan pengeringan otomatis sebagai kelompok perlakuan. Data kedua kondisi dibandingkan berdasarkan waktu pengeringan, kestabilan suhu, kelembapan, dan kondisi akhir gabah.

> Istilah IoT digunakan apabila alat benar-benar mengirimkan data melalui jaringan internet. Apabila sistem hanya menggunakan LCD, judul dan pembahasan lebih tepat menggunakan istilah sistem otomatis berbasis ESP32.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> Perancangan sistem bertujuan untuk menghasilkan sistem pengering padi otomatis yang mampu bekerja secara efektif dalam mengontrol suhu dan kelembapan, sehingga proses pengeringan dapat berlangsung lebih cepat dan stabil.

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| **Clarity** | Maksud kalimat dapat dipahami, tetapi cara sistem mengurangi ketergantungan terhadap cuaca belum dijelaskan. | Jelaskan bahwa sistem menggunakan sumber panas tidak langsung dan kipas. |
| **Precision** | Istilah “lebih efektif” belum menunjukkan indikator keberhasilan. | Gunakan indikator waktu pengeringan, kestabilan suhu, dan perubahan kelembapan. |
| **Conciseness** | Frasa “dengan adanya sistem otomatis ini” dapat dibuat lebih langsung. | Awali kalimat menggunakan subjek “Sistem pengering otomatis”. |

**Paragraf setelah perbaikan:**
> Prototype pengering padi dirancang menggunakan ESP32 dan sensor DHT11 untuk membaca suhu serta kelembapan ruang pengering. Data sensor digunakan untuk mengontrol relay, kipas, dan motor pengaduk agar suhu tetap berada pada rentang 40–50°C dan udara panas tersebar secara merata. Kinerja alat dinilai berdasarkan kestabilan suhu, perubahan kelembapan, respons perangkat, dan waktu yang dibutuhkan selama proses pengeringan.

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis “tentang” riset berarti hanya menjelaskan kegiatan yang dilakukan, seperti alat yang digunakan, tahapan pembuatan, dan proses pengujian. Tulisan seperti ini biasanya menjadi kumpulan informasi yang berdiri sendiri. Pembaca mengetahui apa yang dibuat, tetapi belum tentu memahami alasan penelitian dilakukan dan arti dari hasil yang diperoleh.

> Menulis sebagai “argumen” riset berarti setiap bagian saling berhubungan untuk mendukung satu kesimpulan. Masalah pada pengeringan tradisional menjadi alasan dilakukannya penelitian. Kekurangan metode manual kemudian mengarah pada penggunaan ESP32 dan sensor DHT11 sebagai solusi.

> Metode pengujian harus disusun untuk menjawab pertanyaan penelitian. Hasil pengujian kemudian digunakan sebagai bukti untuk menentukan apakah alat berhasil atau belum. Kesimpulan tidak hanya berisi ringkasan, tetapi memberikan jawaban berdasarkan data yang diperoleh.

> Urutan penulisan Method → Results → Discussion → Introduction dapat meningkatkan kualitas tulisan karena penulis memulai dari bagian yang paling jelas. Method menjelaskan kegiatan yang benar-benar dilakukan, sedangkan Results mencatat data yang benar-benar ditemukan.

> Setelah hasil tersedia, Discussion digunakan untuk menjelaskan arti hasil, penyebab keberhasilan atau kegagalan sistem, serta keterbatasan penelitian. Introduction ditulis setelahnya agar masalah, tujuan, gap, dan kontribusi yang disampaikan sesuai dengan pengujian yang benar-benar dilakukan.

> Urutan tersebut juga membantu menemukan ketidaksesuaian dalam penelitian, seperti perbedaan antara suhu pengeringan 40–50°C dan batas kontrol 12°C. Ketidaksesuaian sensor DHT11 dan DHT22, penggunaan kipas atau lampu, serta klaim sistem berbasis IoT juga lebih mudah ditemukan.

> Dengan demikian, penulisan ilmiah sebagai argumen menghasilkan tulisan yang lebih terarah, konsisten, jelas, dan dapat dipertanggungjawabkan. Setiap klaim yang disampaikan harus memiliki metode pengujian dan bukti hasil yang mendukungnya.

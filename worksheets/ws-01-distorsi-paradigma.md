# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

NAMA : NUR DINI HANDAYANI
NIM : 240202876
KELAS: 4IKRB
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

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (artefak dibuat sebagai instrumen pengujian hipotesis, bukan tujuan akhir).

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
Nama Peneliti    : Nur Dini Handayani
Tanggal          : Rabu, 01 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: apakah ada yang bisa benar benar membuktikan bahwa bisa sampai di angka 95% itu?
   - Data yang dibutuhkan untuk verifikasi: data set mentah, konfigurasi lingkungan pengujian, dan parameter baseline
2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [ ] Design Science  [ X] Mixed
   - Alasan: Sebagai mahasiswa Ilkom saya berfokus pada pengembangan sistem untuk memecahkan masalah praktis dan mengujinya secara objektif
3. Identifikasi distorsi:
   - Asumsi tersembunyi: asumsi bahwa koneksi internet selalu stabil selama pengambilan data
   - Sumber bias potensial: sampling bias
   - Langkah mitigasi: melakukan pengujian berulang di berbagai kondisi jaringan yang berbeda

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: ____________________
   - Batasan yang diakui sejak awal: ____________________
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

**Paper yang dipilih:**
> Judul: Komparasi  Quality Of Service Protokol Virtual Private Network menggunakan PPTP, L2TP, SSTP, dan OpenVPN
> Penulis (Tahun): Ardiansyah, A., & Pamuji, F. Y. (2025)
> Penerbit: InComTech; Jurnal Telekomunikasi dan Komputer (Vol. 15, No.1)
> Akreditasi : SINTA 4

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
||-------------------|-----------------|
| Reality → Data | Menguji 4 protokol VPN berbeda pada infrastruktur jaringan yang sama.| Environment Bias: pengujian mungkin hanya dilakukan di jaringan lokal (LAN), bukan intermet publik yang fluktuatif |

| Data → Processing |Mengambil data Troughput dan delay menggunakan tools seperti wireshark| Technical Distortion : jika spesifikasi perangkat keras (CPU/RAM) terbatas enkripsi VPN yang berat (OpenVPN) akan terlihat lebih buruk secara tidak adil. |

| Processing → Analysis |Membandingkan data statistik antar protokol menggunakan standar TIPHON | Analysis Bias: Terlalu fokus pada kecepatan, namun mengabaikan aspek keamanan (Security) sebagai variabel penting. |

| Analysis → Inference |Menyimpulkan protokol mana yang paling cepat untuk penggunaan harian | Cotextual error yang menyimpulkan bahwa Protokol A lebih baik mungkih hanya berlaku untuk file kecil, bukan untuk streaming video atau gaming |

| Inference → Knowledge |Memberikan rekomendasi pemilihan protokol VPN bagi instansi atau pengguna umum | Overgeneralization : merekomendasikan PPTP karena cepat, padahal secara keamanan sudah usang dan berbahaya. |

**Distorsi paling besar di tahap:** Reality -> Data (Environment Bias)

**Dua distorsi spesifik yang teridentifikasi:**
1. Penggunaan Bandwidth yang tidak dibatasi selama pengujian sehingga tidak mencerminkan kondisi jaringan internet indonesia yang sering mengalami throttling 
2. Pengujian dilakukan pada waktu yang singkat, sehingga tidak menangkap fenomena congestion (kepadatan) jaringan pada jam sibuk.

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Peneliti wajib mengakui keberadaan outlier tersebut. menghapusnya secara diam-diam demi mencapai angka signifikan adalah bentuk manipulasi data yang tidak sesuai edan etika |
| Transparansi | mau seburuk apapun suatu hasil penelitian peneliti harus menjelaskan mengapa hasilnya bisa begitu dan jelaskan apakah ada kegagalan yang dialami, karena penjelasan ini bisa membantu pembaca yang mengalami masalah yang sama |
| Peer review |dengan melaporkan data yang tidak sesuai, peneliti bisa memberikan kesempatan bagi penguji untuk memberikan masukan |

**Keputusan akhir dan justifikasi:**
> peneliti harus tetap menyertakan seluruh data dalam laporan utama. dalam prinsipnya sebuah hipotesis harus berani dibuktikan salah.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Analisis performa dan keamanan protokol VPN di lingkungan akademik
| Kriteria | Positivis | Interpretivis | Design Science |
|Kesesuaian (1-5)|5|1|4|
| Jenis data yang dikumpulkan |Angka Troughput (Mbps), Delay (ms), Packet Loss (%) |Wawancara pengguna tentang kenyamanan VPN |Pembuatan konfigurasi Server VPN yang dioptimasi. |
| Limitasi paradigma |Mengabaikan pengalaman subjektif pengguna |Tidak bisa diukur secara pasti/angka |Fokus pada Alat jalan bukan perbandingan teori |

**Paradigma yang dipilih:* *Positiv* 
**Alasan:* *Karena riset ini sangat bergantung pada pengukuran objektif dan eksperimen terkontrol yang bisa dihitung secara matematis menggunakan standar baku (TIPHON)* ____________________________________________

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sejauh ini saya membaca paper saja untuk mengerjakan tugas ini masih belum banyak hal yang dipahami hingga saya harus bertanya kepada senior dan juga kakak saya, karena perkulihan terkahir yang dilakukan secara online saya tidak bisa mendengarkan secara keseluruhan isi perkuliahan dan walaupun membaca tanpa mendengarkan instruksi langsung itu hal yang berbeda bagi saya dan lebih paham jika mendengarkan langsung.
> karena saya tertarik dengan dunia jaringan akhirnya saya mencari paper yang dimana bahasanya sudah tidak asing bagi saya yaitu yang menyangkut dengan jaringan internet dan sekarang yang saya pertanyakan apakah hasil ini akan tetap sama jika diuji dengan jaringan seluler yang tidak stabil atau apakah alat ukurnya sudah benar benar mewakili kualitas layanan yang dirasakan pengguna. dari rantai distorsi menyadarkan saya bahwa data bisa secara teknis tapi salah secara kesimpulan jika lingkungannya tidak valid.

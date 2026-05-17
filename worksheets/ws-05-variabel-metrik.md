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

Definisi Variabel, Metrik & Justifikasi
VARIABLE & METRIC DEFINITION
Research Question: Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
Variabel
Tipe
Konsep
Metrik
Skala
Satuan
Cara Mengukur
Justifikasi
Arsitektur Routing
IV
Mekanisme atau protokol penentuan jalur transmisi paket inter-domain.
Kategori metode: BGP Standar, LSTM Murni, Hybrid LSTM-BGP.
Nominal
—
Menjalankan simulasi jaringan atau emulasi perangkat dengan menyuntikkan salah satu dari tiga metode kontrol rute secara bergantian.
Variabel ini dimanipulasi untuk menguji dampak langsung dari struktur kecerdasan prediktif terhadap efisiensi konvergensi jaringan.
Waktu Konvergensi Rute
DV
Kecepatan penyesuaian infrastruktur untuk mencapai kestabilan jalur baru setelah anomali.
Convergence Time (durasi pembaruan tabel).
Ratio
Detik
Menghitung selisih waktu antara pesan pembaruan rute pertama (BGP Update) yang dikirim hingga tabel routing di seluruh node edge mencapai status sinkron (steady-state).
Metrik waktu konvergensi merupakan parameter standar industri untuk mengevaluasi kecepatan pemulihan routing global dari kegagalan tautan.
Tingkat Kehilangan Paket
DV
Reliabilitas dan stabilitas pengiriman data selama periode ketidakstabilan rute.
Packet Loss Rate (persentase kegagalan transmisi).
Ratio
Persen (%)
Mengalkulasi jumlah paket ICMP/UDP yang tidak sampai ke tujuan dibagi dengan total jumlah paket yang dikirimkan selama proses re-routing terjadi.
Packet Loss Rate mencerminkan tingkat kemacetan atau kegagalan fungsional dari jalur alternatif yang dipilih oleh arsitektur yang diuji.
Skala Topologi Jaringan
CV
Ukuran lingkungan uji untuk menyamakan kompleksitas komputasi routing global.
Jumlah prefix otonom (AS) dan node router dalam topologi.
Ratio
Node / Prefix
Menetapkan jumlah entitas rute statis pada angka 100.000 prefix pada emulator jaringan (misalnya menggunakan topologi RIPE Atlas).
Pengendalian skala topologi wajib dilakukan agar perbedaan waktu konvergensi murni disebabkan oleh efisiensi algoritma, bukan fluktuasi ukuran jaringan.

Alignment Check:
RQ → Concept → Variable → Metric → Data → Result
[X] Setiap langkah terdokumentasi
[X] Tidak ada "lompatan logis"
[X] Metrik mengukur apa yang dimaksud (construct validity)

Latihan 1 — Operationalization Chain
RQ: Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
Variabel
Tipe
Konsep Abstrak
Metrik Konkret
Skala (NOIR)
Satuan
Arsitektur Routing
IV
Pendekatan manajemen keputusan rute inter-domain
Kategorikal: BGP Standar vs LSTM Murni vs Hybrid LSTM-BGP
Nominal
—
Waktu Konvergensi
DV
Kecepatan stabilisasi tabel routing setelah pembaruan topologi
Convergence Time (durasi dari pengiriman pesan pembaruan rute hingga sinkronisasi)
Ratio
Detik
Tingkat Kehilangan Paket
DV
Integritas transmisi data pada kondisi link mengalami kongesti
Packet Loss Rate (persentase paket hilang terhadap total paket terkirim)
Ratio
Persen (%)
Beban Trafik Jaringan
CV
Volume data yang melintasi infrastruktur per satuan waktu
Background Traffic Throughput
Ratio
Gbps

Apakah ada lompatan logis dalam rantai? [ ] Ya / [X] Tidak
Justifikasi: Rantai operasionalisasi dari konsep abstrak "kecepatan stabilisasi" dan "integritas transmisi" telah diturunkan secara logis tanpa celah menjadi metrik fisik yang dapat diukur secara langsung melalui perangkat monitoring jaringan jaringan, yaitu durasi waktu konvergensi (detik) dan rasio kehilangan paket data (%).

Latihan 2 — Evaluasi Metrik
Evaluasi metrik DV utama yang dipilih (Convergence Time).
Kriteria
Skor (1-5)
Justifikasi
Representative
5
Convergence time secara akurat menggambarkan durasi ketidakstabilan arsitektur internet ketika terjadi kegagalan atau perubahan kebijakan inter-domain rute.
Sensitive
4
Satuan ukur detik (atau milidetik) memiliki tingkat kepekaan yang memadai untuk menangkap selisih variasi durasi komputasi yang dihasilkan oleh model cerdas maupun protokol standar.
Feasible
4
Metrik ini dapat diperoleh secara langsung dengan merekam stempel waktu (timestamp) paket protokol pada log router atau menggunakan aplikasi analisis trafik jaringan.

Apakah perlu secondary metric? [X] Ya / [ ] Tidak
Jika ya, apa dan mengapa? Ya, diperlukan Packet Loss Rate dan Computational Overhead (penggunaan CPU/RAM router) sebagai secondary metric. Metrik ini diperlukan untuk mengawasi apakah efisiensi waktu konvergensi yang diraih oleh model hibrida harus dibayar mahal oleh tingginya konsumsi sumber daya komputasi lokal pada router.
Contoh kasus ceiling effect untuk metrik ini:
Ceiling effect terjadi jika anomali tautan atau skenario gangguan yang diujikan dalam simulasi terlalu kecil atau sederhana (misalnya hanya melibatkan kurang dari 10 node). Pada kondisi ini, seluruh arsitektur routing (baik konvensional maupun bertenaga kecerdasan buatan) akan selalu menghasilkan waktu konvergensi instan mendekati batas minimum pemrosesan perangkat keras, sehingga metrik gagal memperlihatkan perbedaan efisiensi algoritma yang diuji.

Latihan 3 — Data Quality Check
Evaluasi 4 dimensi kualitas data pada lingkungan eksperimen emulasi jaringan.
Dimensi
Pertanyaan
Jawaban
Strategi Mitigasi
Completeness
Apakah semua data point terkumpul?
Terdapat potensi kehilangan data point metrik akibat keterlambatan pencatatan log (log dropping) saat router mengalami beban kerja ekstrem.
Mengimplementasikan agen kolektor log eksternal yang terpisah dari mesin emulasi utama dengan alokasi buffer memori yang besar.
Consistency
Apakah ada kontradiksi internal?
Kegagalan sinkronisasi waktu clock antar node router dapat memicu pembacaan timestamp paket yang tumpang tindih atau negatif.
Membaca dan menyeragamkan referensi waktu seluruh simpul router menggunakan protokol Network Time Protocol (NTP) terpusat sebelum eksperimen dimulai.
Validity
Apakah benar-benar mengukur yang dimaksud?
Packet loss bisa saja disebabkan oleh kerusakan tautan fisik simulasi (link failure), bukan akibat ketidakmampuan algoritma memilih rute.
Memisahkan metrik paket yang hilang akibat putusnya link fisik dengan paket yang hilang akibat jatuhnya rute (routing blackhole) dalam tabel BGP.
Representativeness
Apakah sampel mewakili populasi target?
Dataset log historis dari RIPE Atlas atau Route Views mencerminkan karakteristik struktur internet global riil, namun performanya dapat berbeda jika dihadapkan pada fluktuasi trafik lokal terisolasi.
Menggunakan variasi skenario beban trafik campuran (mixed-profile traffic), mencakup tipe data konstan (streaming) dan fluktuatif (bursty web traffic).


Refleksi
Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?
Jawaban:
Memilih metrik evaluasi setelah data eksperimen terkumpul dikategorikan sebagai tindakan p-hacking karena peneliti dapat secara sengaja mencari, menyaring, atau memindahkan fokus analisis pada metrik tertentu yang hanya menguntungkan atau mendukung hipotesis awal mereka, sambil mengabaikan metrik utama yang justru menunjukkan kegagalan metode. Tindakan ini merusak objektivitas ilmiah karena mengubah proses pembuktian hipotesis (confirmatory research) menjadi pencarian pembenaran dari data acak. Perbedaannya dengan eksplorasi data yang sah terletak pada tujuan dan transparansi pelaporannya; eksplorasi data (exploratory data analysis) bertujuan untuk mencari pola baru, merumuskan hipotesis baru, atau mendeteksi anomali di luar hipotesis awal, di mana hasilnya harus dilaporkan secara terpisah sebagai temuan awal tambahan dan tidak boleh diklaim sebagai metrik utama pembuktian hipotesis yang telah ditetapkan sejak awal eksperimen dirancang.

Referensi Jurnal
Wang, Y., et al. (2022). Deep Reinforcement Learning for BGP Routing Optimization in Large-Scale Internet Architecture. IEEE Transactions on Network and Service Management, 19(3), 2145-2158. [Membahas performa dan limitasi skalabilitas DRL pada tabel routing global].
Kumar, R., & Singh, A. (2024). Time-Series Predictive Models for Inter-Domain Traffic Engineering and Congestion Control. ACM Computer Communication Review, 54(1), 34-45. [Membahas pemanfaatan LSTM untuk prediksi beban trafik dan estimasi convergence time].
Al-Kadi, M., et al. (2024). Multi-Homing Traffic Engineering and Load Balancing Metrics in Enterprise Networks. Journal of Network and Computer Applications, 222, 103-115. [Membahas pemetaan metrik packet loss rate dan pembagian beban link inter-domain].
Chen, X., et al. (2025). Edge-SDN Integration for Resilient Inter-Domain Routing Protocols. IEEE Journal on Selected Areas in Communications, 43(2), 412-425. [Membahas construct validity serta batasan implementasi SDN terprogram vs perangkat konvensional].

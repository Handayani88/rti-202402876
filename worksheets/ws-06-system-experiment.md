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

## Mapping RQ ke Arsitektur Sistem
SYSTEM-EXPERIMENT MAPPING
Research Question: Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
Variable → Component Mapping:
Variabel
Tipe
Komponen Sistem
Cara Manipulasi/Pengukuran
Arsitektur Routing
IV
Routing Engine Module (Sub-modul: Standard BGP Deamon, Pure LSTM Predictor, Hybrid LSTM-BGP Controller).
Mengubah parameter penunjuk objek kontrol rute pada berkas konfigurasi utama (routing_mode: "hybrid_lstm_bgp").
Waktu Konvergensi Rute
DV
Telemetry Logger & Traffic Analyzer Module.
Membaca selisih waktu log dari notifikasi pesan BGP Update pertama hingga status tabel rute mencapai kondisi stabil (converged).
Tingkat Kehilangan Paket
DV
Packet Traffic Monitor (berbasis penandaan paket uji ICMP/UDP).
Menghitung otomatis rasio jumlah paket yang gagal mencapai tujuan terhadap total paket yang disuntikkan selama periode gangguan jalur.
Skala Topologi Jaringan
CV
Network Topology Emulator Matrix (FRRouting / Mininet-NetNext).
Mengunci jumlah simpul Autonomous System (AS) dan jumlah prefix tabel rute statis di dalam berkas inisialisasi lingkungan uji.

4 Prinsip Desain:
[X] Traceability — Setiap komponen arsitektur sistem dapat ditelusuri perannya ke variabel independen, dependen, maupun kontrol secara langsung.
[X] Variable Isolation — Komponen Routing Engine dibuat terpisah sehingga manipulasi jenis arsitektur (IV) tidak memengaruhi metrik kontrol topologi (CV).
[X] Measurement Integration — Komponen instrumen ukur (Telemetry Logger) tertanam langsung (built-in) pada sistem untuk mencatat perubahan data tanpa intervensi manual.
[X] Reproducibility — Seluruh struktur topologi, skenario injeksi gangguan, dan variasi model kontrol diatur melalui berkas konfigurasi eksternal (YAML).
Experimental Setup:
Input data: Dataset rekam jejak telemetri lalu lintas global riil dari RIPE Atlas Anchors dan Route Views BGP Archive.
Parameter: Batasan memori pemrosesan router = 2 GB, jumlah inter-domain rute = 100.000 prefix, interval injeksi kegagalan link (link-failure trigger) = setiap 300 detik.
Output format: Berkas catatan terstruktur .csv yang berisi baris stempel waktu (timestamp), jenis kegagalan, durasi konvergensi (detik), dan jumlah paket hilang (%).

Latihan 1 — Variable-to-Component Mapping
RQ: Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
Variabel
Tipe
Komponen Sistem
Cara Manipulasi / Pengukuran
Arsitektur Routing
IV
Routing Engine Controller Interface
Melakukan hot-swapping taksonomi mesin penentu rute melalui pengubahan nilai flag teks pada konfigurasi utama sistem (routing_core).
Waktu Konvergensi
DV
BGP Event Timestamp Capture Core
Merekam penanda waktu dari paket BGP State Machine saat berpindah posisi dari kondisi Active/OpenConfirm menuju Established.
Tingkat Kehilangan Paket
DV
Packet Loss Counter Subsystem
Memeriksa kecocokan nomor urut (sequence number) paket data yang ditransmisikan melalui agen pemantau trafik di sisi penerima.
Beban Trafik Jaringan
CV
Background Traffic Generator Engine
Menyuntikkan beban konstan berupa data lalu lintas latar belakang (stateless background traffic) sebesar 1 Gbps ke dalam jalur pipa transmisi utama.

Apakah semua variabel bisa di-map? [X] Ya / [ ] Tidak
Justifikasi: Seluruh variabel yang tercantum di dalam pertanyaan penelitian telah memiliki padanan komponen yang jelas dalam arsitektur sistem emulasi, sehingga sistem siap difungsikan sebagai instrumen pengumpul bukti empiris.

Latihan 2 — 4 Prinsip Desain
Evaluasi desain sistem terhadap 4 prinsip utama rancangan eksperimen.
Prinsip
Status
Bukti / Penjelasan
Traceability
✅
Setiap blok fungsional dalam rancangan arsitektur memiliki label pelacakan yang terikat langsung pada variabel penelitian. Komponen penentu jalur melayani IV, sementara komponen pemantau paket melayani DV.
Modularity
✅
Modul kecerdasan prediktif LSTM dikembangkan sebagai pustaka eksternal yang terpisah dari inti protokol BGP konvensional, sehingga dapat dilepas atau dipasang tanpa merusak fungsi dasar routing forwarding table.
Controllability
✅
Kompanyemen parameter uji seperti kapasitas bandwidth tautan, jenis topologi autonom, dan durasi interval kegagalan jalur ditempatkan di luar kode program, tepatnya pada berkas konfigurasi YAML terpusat.
Measurability
✅
Sistem emulasi memiliki mesin pencatat data telemetri internal yang otomatis menuliskan hasil pengukuran performa langsung ke penyimpanan eksternal setiap kali fase konvergensi rute selesai dieksekusi.

Prinsip mana yang paling sulit dipenuhi? Modularity
Strategi untuk mengatasinya:
Memisahkan arsitektur komunikasi data menggunakan metode pemanggilan prosedur jarak jauh atau Remote Procedure Call (RPC) internal antara mesin protokol utama (BGP) dengan pustaka kecerdasan buatan (LSTM). Langkah ini dilakukan agar galat atau keterlambatan proses komputasi yang terjadi pada modul prediktif tidak langsung memutus atau menghentikan jalannya sistem operasi router emulasi secara keseluruhan.

Latihan 3 — Ablation Study Planning
Rencana pengujian kontribusi arsitektur komponen pembentuk sistem Hybrid LSTM-BGP.
Kondisi
Komponen A (Mesin BGP Konvensional)
Komponen B (Prediktor Runtun Waktu LSTM)
Komponen C (Modul Mitigasi Kemacetan / Congestion Control)
Hasil yang Diharapkan
Full
✅ Aktif
✅ Aktif
✅ Aktif
Performa optimal sistem: Waktu konvergensi rute berada pada titik tercepat dan tingkat kehilangan paket data seminimal mungkin.
– A
❌ Tidak Aktif
✅ Aktif
✅ Aktif
Kegagalan sistem transmisi penuh (system failure) karena model prediktif LSTM murni tidak memiliki fungsionalitas dasar penyerahan paket data.
– B
✅ Aktif
❌ Tidak Aktif
✅ Aktif
Karakteristik kinerja jaringan kembali seperti kinerja BGP standar, di mana penyesuaian rute lambat saat terjadi gangguan berskala besar.
– C
✅ Aktif
✅ Aktif
❌ Tidak Aktif
Waktu konvergensi rute tetap berjalan cepat, tetapi persentase kehilangan paket data meningkat karena hilangnya kendali adaptif terhadap antrean kemacetan.

Komponen mana yang diprediksi paling berkontribusi? Komponen B (Prediktor Runtun Waktu LSTM) Mengapa?
Komponen B bertanggung jawab memproyeksikan status kondisi kemacetan jalur inter-domain sebelum anomali data benar-benar terjadi, sehingga router dapat mengambil langkah pembaruan rute lebih awal tanpa harus menunggu penumpukan antrean paket data yang memicu jatuhnya jaringan internet.

Refleksi
Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?
Jawaban:
Jika sistem eksperimen dibangun menyerupai produk komersial yang bersifat monolitik dengan fitur yang terlalu lengkap, peneliti akan menghadapi kendala besar berupa tingginya tingkat noise atau gangguan variabel luar yang saling tumpang tindih. Pada arsitektur monolitik, interaksi antar komponen internal saling mengikat secara ketat (tightly coupled), sehingga mustahil untuk mengisolasi secara pasti apakah perubahan performa yang terukur pada variabel dependen murni bersumber dari intervensi variabel independen atau akibat efek samping dari subsistem pendukung lainnya.
Oleh karena itu, arsitektur modular menjadi sangat penting dalam sebuah penelitian karena memfasilitasi prinsip isolasi variabel secara mutlak. Dengan memisahkan setiap fungsi ke dalam modul-modul independen yang terisolasi, peneliti dapat secara bebas mengubah, menukar, atau melepas komponen tertentu (seperti pada metode ablation study) tanpa memicu efek domino yang dapat merusak kestabilan parameter kontrol atau komponen sistem lainnya, sehingga validitas internal pengujian dapat dipertahankan.

Referensi Jurnal
Wang, Y., et al. (2022). Deep Reinforcement Learning for BGP Routing Optimization in Large-Scale Internet Architecture. IEEE Transactions on Network and Service Management, 19(3), 2145-2158. [Membahas pemisahan arsitektur mesin routing kontrol dan pentingnya isolasi variabel dalam eksperimen jaringan skala besar].
Kumar, R., & Singh, A. (2024). Time-Series Predictive Models for Inter-Domain Traffic Engineering and Congestion Control. ACM Computer Communication Review, 54(1), 34-45. [Menjelaskan rancangan modular untuk mengintegrasikan model prediktif runtun waktu ke dalam simulator routing internet].
Chen, X., et al. (2025). Edge-SDN Integration for Resilient Inter-Domain Routing Protocols. IEEE Journal on Selected Areas in Communications, 43(2), 412-425. [Menyoroti metodologi pengujian arsitektur berbasis configuration-driven execution untuk menjaga reproduksibilitas data uji].
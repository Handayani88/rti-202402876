# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database**: IEEE Xplore, ACM DL, Scopus, Google Scholar
2. **Boolean query** yang terdokumentasi eksplisit
3. **Snowballing**: backward (telusuri referensi) + forward (cari yang mengutip)
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

LITERATURE MAPPING

Topik      : Optimalisasi Protokol Routing BGP dan Arsitektur Multi-Homing untuk Mitigasi Kemacetan Jaringan Internet
Database   : IEEE Xplore, Google Scholar, ACM Digital Library
Query      : ("Internet architecture" OR "BGP routing optimization") AND ("congestion control" OR "multi-homing traffic engineering")
Tahun      : 2021 - 2026
Hasil awal : 45 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
| Wang et al. | 2022 | Deep Reinforcement Learning (DRL) untuk optimasi rute BGP | Dataset lalu lintas sintetis (simulasi ns-3) | Menurunkan latensi rata-rata sebesar 14.5% | Skalabilitas komputasi rendah jika diterapkan pada tabel routing global (>1 juta prefix) |
| Zhang & Liu | 2023 | Segment Routing (SRv6) dinamis berdasarkan beban tautan | Topologi jaringan ISP lokal (skala medium) | Efisiensi bandwidth meningkat 22% pada kondisi puncak | Tidak mempertimbangkan fluktuasi latensi akibat inter-domain routing policies |
| Al-Kadi et al. | 2024 | Multi-homing Traffic Engineering berbasis heuristik | Log traffic historis dari satu Autonomous System (AS) kampus | Redundansi link terjaga dengan sebaran beban seimbang 40:60 | Bersifat reaktif terhadap kongesti, bukan preventif |
| Kumar & Singh | 2024 | Model prediktif LSTM untuk beban trafik disusul re-routing BGP | Dataset lalu lintas publik (RIPE Atlas & Route Views) | Akurasi prediksi kongesti mencapai 89% | Kegagalan konvergensi routing jika terjadi perubahan topologi global yang masif dan mendadak |
| Chen et al. | 2025 | Integrasi SDN (Software-Defined Networking) di edge untuk inter-domain routing | Dataset edge-traffic multi-provider lokal | throughput naik 18%, deteksi bottleneck < 5 detik | Membutuhkan modifikasi arsitektur router konvensional secara menyeluruh di level ISP |

Pola yang ditemukan:
  Metode dominan     : Penggunaan algoritma cerdas berbasis data (Machine Learning/DRL) dan arsitektur terprogram (SDN/SRv6).
  Dataset umum       : Log trafik Autonomous System internal, dataset publik RIPE Atlas/Route Views, dan simulasi topologi ns-3.
  Limitasi berulang  : Masalah skalabilitas komputasi pada tabel routing global serta tingginya dependensi terhadap infrastruktur yang harus dimodifikasi secara masif.

GAP IDENTIFICATION

Gap 1: [Jenis: Performance Gap & Method Gap]
  Deskripsi    : Pendekatan berbasis Deep Reinforcement Learning (DRL) memiliki overhead komputasi yang terlalu tinggi untuk konvergensi tabel routing internet global (>1 juta baris rute).
  Bukti        : Penelitian Wang et al. (2022) mendapati latensi keputusan meningkat eksponensial saat jumlah node bertambah, dan Chen et al. (2025) memerlukan perangkat SDN khusus yang mahal.
  Signifikansi : Jika konvergensi rute lambat, risiko paket hilang (packet loss) selama proses pembaruan rute inter-domain tetap tinggi saat terjadi gangguan masif.

Gap 2: [Jenis: Data Gap & Context Gap]
  Deskripsi    : Evaluasi metode pengalihan trafik multi-homing mayoritas menggunakan dataset lokal satu entitas atau simulasi sintetis, belum diuji pada karakteristik trafik regional negara berkembang yang memiliki keterbatasan bandwidth link internasional.
  Bukti        : Al-Kadi et al. (2024) hanya menggunakan satu AS internal kampus, sementara Kumar & Singh (2024) mengasumsikan kapasitas bandwidth backbone antar-AS selalu homogen.
  Signifikansi : Protokol yang dirancang tanpa adaptasi batas bandwidth internasional yang asimetris akan memicu kongesti baru pada link sekunder.

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| BGP Route-Reflector standar dengan kebijakan berbasis statistik historis | Menyelesaikan masalah pembagian beban trafik inter-domain dan mitigasi kongesti tautan | Merupakan standar baku (common practice) yang saat ini diimplementasikan di sebagian besar Autonomous System tradisional | Al-Kadi et al., 2024 |
| Model Prediktif LSTM untuk Traffic Engineering | Menggunakan pendekatan berbasis runtun waktu untuk memprediksi kongesti sebelum re-routing dilakukan | Mewakili pendekatan state-of-the-art (SOTA) berbasis kecerdasan komputasi tanpa mengubah struktur fisik router | Kumar & Singh, 2024 |

#Concept-Centric Literature Table#
Topik riset: Optimalisasi Protokol Routing BGP dan Arsitektur Multi-Homing untuk Mitigasi Kemacetan Jaringan Internet

Query pencarian: ("Internet architecture" OR "BGP routing optimization") AND ("congestion control" OR "multi-homing traffic engineering")

Database: Google Scholar & IEEE Xplore
#,Study,Tahun,Method,Dataset,Result,Limitasi
1,Wang et al.,2022,Deep Reinforcement Learning (DRL),Dataset lalu lintas sintetis (ns-3),Latensi rata-rata turun 14.5%,Skalabilitas rendah pada tabel routing global (>1 juta prefix)
2,Zhang & Liu,2023,Segment Routing (SRv6) Dinamis,Topologi ISP lokal skala medium,Efisiensi bandwidth naik 22% pada beban puncak,Mengabaikan fluktuasi latensi kebijakan inter-domain
3,Al-Kadi et al.,2024,Heuristik Traffic Engineering,Log trafik historis 1 AS internal,Pembagian beban link seimbang (40:60),"Bersifat reaktif terhadap kongesti, bukan preventif"
4,Kumar & Singh,2024,Model Prediktif LSTM,Dataset RIPE Atlas & Route Views,Akurasi prediksi kongesti 89%,Risiko gagal konvergensi jika topologi berubah mendadak
5,Chen et al.,2025,Edge-SDN Integration,Dataset edge-traffic multi-provider,"Throughput naik 18%, deteksi bottleneck < 5 detik",Perlu modifikasi menyeluruh pada arsitektur router fisik

Pola yang terlihat — Metode dominan: Implementasi kecerdasan buatan (DRL/LSTM) untuk prediksi beban trafik dan arsitektur jaringan masa depan seperti SDN/SRv6 untuk kontrol jalur.

Limitasi yang berulang: Kegagalan mempertahankan performa konvergensi yang cepat ketika dihadapkan pada skala tabel routing internet global serta kebutuhan biaya infrastruktur baru yang tinggi.

Jenis Gap,Ditemukan?,Gap Statement
Performance Gap,[X] Ya / [ ] Tidak,Penurunan kecepatan konvergensi rute pada algoritma DRL saat ukuran tabel routing mencapai skala internet global.
Method Gap,[X] Ya / [ ] Tidak,Jarang ditemukan integrasi metode kontrol preventif (hybrid LSTM) yang langsung bekerja pada perangkat keras BGP konvensional tanpa arsitektur SDN penuh.
Data Gap,[X] Ya / [ ] Tidak,Mayoritas pengujian menggunakan dataset tertutup (single AS log) atau data simulasi sintetis yang tidak mencerminkan anomali traffic internet riil.
Context Gap,[X] Ya / [ ] Tidak,Pengujian efisiensi arsitektur ini belum melibatkan skenario infrastruktur jaringan di wilayah dengan link internasional asimetris (seperti di negara berkembang).

Gap utama yang dipilih: Kombinasi antara Performance Gap (skalabilitas konvergensi rute BGP) dan Method Gap (metode optimasi tanpa merombak infrastruktur eksis ke SDN penuh).

Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")? > Mengganti seluruh infrastruktur router konvensional menjadi berbasis SDN di tingkat ISP membutuhkan biaya yang sangat besar dan waktu migrasi yang lama. Di sisi lain, membiarkan optimasi rute berjalan lambat (akibat beban komputasi AI yang tinggi) menyebabkan hilangnya paket data penting saat terjadi gangguan jaringan skala besar. Oleh karena itu, diperlukan metode hibrida yang ringan secara komputasi namun tetap prediktif untuk menjamin stabilitas internet.

#,Baseline,Mengapa Relevan,Mengapa Representatif,Apakah SOTA?,Sumber
1,BGP Route-Reflector Tradisional dengan Aturan Heuristik,"Masalah yang diselesaikan sama, yaitu manajemen distribusi beban trafik keluar/masuk antar-AS.",Metode ini merupakan common practice industri yang digunakan di hampir semua jaringan ISP konvensional saat ini.,"Bukan, tetapi merupakan fondasi arsitektur operasional.","Al-Kadi et al., 2024"
2,Model Arsitektur Prediktif berbasis LSTM,Sama-sama menggunakan pendekatan prediktif berbasis waktu untuk menghindari jalur yang berpotensi mengalami kongesti.,Mewakili performa terbaik terkini (State-of-the-Art) untuk pendekatan berbasis perangkat lunak murni tanpa perubahan fisik.,"Ya, salah satu yang terbaik di kelas pendekatan prediktif.","Kumar & Singh, 2024"
Apakah pemilihan baseline ini bisa dianggap straw man? [ ] Ya / [X] Tidak

Justifikasi: Pemilihan baseline ini adil dan jujur karena membandingkan metode usulan langsung dengan standar industri yang berlaku (common practice dari Al-Kadi et al.) untuk membuktikan nilai praktisnya, sekaligus menghadapkannya dengan model cerdas mutakhir (State-of-the-Art dari Kumar & Singh) untuk menguji keunggulan akurasi serta efisiensi komputasinya.

Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

Jawaban: > Perbedaannya terletak pada basis pembuktiannya; klaim "belum ada yang meneliti" cenderung berupa asumsi subyektif akibat penelusuran yang tidak komprehensif, sedangkan research gap yang valid diperoleh secara objektif melalui pemetaan literatur terstruktur (concept-centric mapping) untuk menyingkap limitasi, inkonsistensi, atau kelemahan dari metode terdahulu. Keberadaan gap ini dibuktikan dengan mendokumentasikan strategi pencarian yang sistematis dan transparan (meliputi basis data, kata kunci Boolean, dan batasan tahun), yang kemudian disajikan dalam matriks evaluasi untuk mengonfirmasi titik lemah spesifik yang belum terjawab oleh komunitas ilmiah.
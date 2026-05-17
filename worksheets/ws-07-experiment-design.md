# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

Desain Eksperimen Lengkap
EXPERIMENT DESIGN
Research Question : Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
Hypothesis : $H_1$: Penggunaan arsitektur Hybrid LSTM-BGP menghasilkan penurunan rata-rata waktu konvergensi rute inter-domain sebesar minimal 15% dan penurunan packet loss yang signifikan secara statistik dibandingkan model BGP standar dan LSTM murni pada dataset RIPE Atlas.
Tipe Eksperimen : [X] Comparison [X] Ablation [ ] Parameter
Kondisi Eksperimen:
Kondisi
Deskripsi
IV Value
CV Settings
Control 1
Implementasi protokol routing konvensional standar industri tanpa komponen prediktif.
BGP Standar (menggunakan Route-Reflector).
Dataset RIPE Atlas & Route Views, topologi 100.000 prefix, kapasitas link 1 Gbps, background traffic konstan 500 Mbps.
Control 2
Model manajemen lalu lintas berbasis kecerdasan buatan murni tanpa integrasi mesin BGP fisik.
Model Prediktif LSTM Murni.
Dataset RIPE Atlas & Route Views, topologi 100.000 prefix, kapasitas link 1 Gbps, background traffic konstan 500 Mbps.
Treatment
Arsitektur hibrida terintegrasi yang menggabungkan prediksi runtun waktu ke mesin eksekusi BGP.
Arsitektur Hybrid LSTM-BGP.
Dataset RIPE Atlas & Route Views, topologi 100.000 prefix, kapasitas link 1 Gbps, background traffic konstan 500 Mbps.

Fairness Checklist:
[X] Dataset identik untuk semua kondisi
[X] Preprocessing setara
[X] Tuning effort setara
[X] Environment identik
[X] Metrik evaluasi sama
Threat Analysis:
Threat Type
Ancaman Spesifik
Mitigasi
Internal
Perubahan performa atau waktu konvergensi dipengaruhi oleh fluktuasi penggunaan CPU/RAM pada mesin host emulator, bukan karena efisiensi algoritma routing.
Menjalankan isolasi sumber daya komputasi (resource pinning) menggunakan kontainer Docker untuk setiap simpul router emulasi dan membatasi memori maksimal 2 GB.
External
Dataset jejak trafik dari RIPE Atlas mewakili kondisi internet global tertentu, sehingga model hibrida berisiko tidak mampu menggeneralisasi kinerja pada karakteristik jaringan privat lokal.
Melakukan pengujian tambahan dengan membagi pengujian ke dalam tiga skenario profil trafik yang berbeda: mixed-profile, bursty traffic, dan high-load streaming.
Construct
Metrik Convergence Time dihitung tidak akurat akibat adanya penundaan internal log (log latency) dari aplikasi emulasi jaringan.
Membaca stempel waktu pembaruan rute langsung dari packet capture file (PCAP) Wireshark melalui analisis raw packet tingkat rendah, bukan berdasarkan waktu cetak log router.
Conclusion
Jumlah pengulangan simulasi kegagalan tautan yang terlalu sedikit membuat variasi data bias dan kesimpulan statistik menjadi tidak valid.
Melakukan pengulangan pengujian pemutusan tautan (link failure triggers) sebanyak minimal 50 kali untuk setiap kondisi guna menjamin kecukupan sampel.

Statistical Plan:
Uji statistik : Analisis Varians Satu Arah (One-Way ANOVA) dilanjutkan dengan uji Post-Hoc Tukey HSD.
Justifikasi : Eksperimen ini membandingkan rata-rata nilai numerik skala rasio dari tiga kelompok perlakuan yang independen untuk melihat perbedaan yang bermakna.
Alpha : 0.05
Effect size min : Cohen's $d \ge 0.5$ (efek sedang hingga besar) untuk memastikan signifikansi fungsional perbaikan rute di lapangan.

Latihan 1 — Desain Eksperimen
Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.
RQ: Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
Tipe eksperimen: [X] Comparison / [X] Ablation / [ ] Parameter
Kondisi
Deskripsi
IV Value
CV Settings
Control 1
Menjalankan sistem routing berbasis protokol konvensional lama untuk mengukur kinerja dasar jaringan.
BGP Standar
Dataset RIPE Atlas, 100.000 prefix, 50 node AS, seed randomization 42.
Control 2
Menjalankan sistem routing berbasis kecerdasan prediktif runtun waktu secara penuh tanpa mesin BGP.
LSTM Murni
Dataset RIPE Atlas, 100.000 prefix, 50 node AS, seed randomization 42.
Treatment
Menjalankan sistem routing hasil integrasi hibrida antara prediktor LSTM dan mesin protokol BGP.
Hybrid LSTM-BGP
Dataset RIPE Atlas, 100.000 prefix, 50 node AS, seed randomization 42.


Latihan 2 — Fairness Checklist
Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.
Kriteria
Status
Detail
Dataset identik
✅
Seluruh kelompok (Control 1, Control 2, dan Treatment) menggunakan basis data log historis RIPE Atlas Anchors yang sama.
Preprocessing setara
✅
Format konversi data deret waktu untuk ekstraksi fitur kemacetan dikerjakan menggunakan skrip pembersih data yang identik sebelum diumpankan ke model.
Tuning effort setara
✅
Model LSTM pada kondisi Control 2 dan Hybrid pada Treatment dikonfigurasi menggunakan arsitektur hyperparameter dasar yang sama (jumlah hidden layers dan learning rate sama).
Environment identik
✅
Semua pengujian dijalankan pada server fisik yang sama menggunakan alokasi core CPU dan memori RAM terisolasi melalui cgroups.
Metrik evaluasi sama
✅
Penilaian keandalan dan kecepatan dihitung menggunakan instrumen pengukur tunggal untuk parameter Convergence Time (detik) dan Packet Loss Rate (%).

Ada yang tidak fair? [ ] Ya / [X] Tidak
Justifikasi: Seluruh metode dijalankan pada batasan topologi, parameter latar belakang beban trafik, dan arsitektur perangkat keras simulator yang sepenuhnya seragam, sehingga selisih performa murni timbul dari perbedaan variasi independen (independent variable).

Latihan 3 — Threat Analysis
Identifikasi ancaman validitas untuk desain eksperimen ini.
Threat Type
Ancaman Spesifik
Mitigasi
Internal
Kegagalan pembaruan rute (route flapping) tidak sengaja terpicu akibat adanya delay internal jaringan host tempat simulasi berjalan.
Menerapkan waktu jeda pemulihan (hold-down timer) yang sinkron di tingkat kernel simulator untuk memisahkan anomali internal host dengan kegagalan link eksperimen.
External
Karakteristik data uji RIPE Atlas didominasi oleh topologi jaringan regional Eropa, sehingga hasil berisiko tidak mencerminkan perilaku routing di wilayah dengan infrastruktur berbeda.
Menambahkan porsi validasi eksternal menggunakan data tabel routing global dari repositori Route Views BGP Archive regional Amerika dan Asia.
Construct
Pengukuran Packet Loss Rate mengalami bias karena paket uji ICMP dibatalkan otomatis (dropped) oleh aturan pengamanan internal router (rate limiting).
Menggunakan paket data UDP buatan khusus sebagai trafik uji performa jalur untuk menghindari blokir otomatis protokol kendali internal.
Conclusion
Distribusi data dari hasil pengulangan tidak berdistribusi normal, sehingga penerapan uji ANOVA dapat menghasilkan kesimpulan statistik yang keliru.
Melakukan pengujian normalitas data (Shapiro-Wilk test) terlebih dahulu; jika sebaran tidak normal, metode analisis diganti ke uji non-parametrik Kruskal-Wallis.

Ancaman mana yang paling sulit dimitigasi? External Validity
Mengapa?
Karakteristik struktur topologi internet global riil bersifat dinamis dan sangat kompleks. Memindahkan perilaku miliaran interkoneksi perangkat routing internet asli ke dalam lingkungan emulasi skala laboratorium (bahkan dengan bantuan dataset RIPE Atlas) selalu menyisakan penyederhanaan aspek latensi propagasi kabel laut dan kebijakan komersial antar ISP yang sulit ditiru secara sempurna.

Refleksi
Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?
Jawaban:
Apakah seluruh baseline dibandingkan dalam kondisi parameter lingkungan kerja yang adil (fair environment)? Peneliti harus memastikan apakah baseline diuji menggunakan kapasitas komputasi, struktur dataset preprocessing, dan alokasi sumber daya yang sama, atau justru baseline sengaja dijalankan dengan parameter bawaan (default) tanpa proses optimasi.
Bagaimana karakteristik dataset yang digunakan untuk klaim superioritas tersebut? Perlu diperiksa apakah peningkatan performa metode baru hanya terjadi pada satu skenario dataset spesifik yang menguntungkan struktur algoritmanya, atau performa tersebut tetap stabil saat dihadapkan pada variasi data eksternal lainnya.
Apakah selisih keunggulan performa yang dilaporkan signifikan secara statistik atau hanya berupa perbedaan nominal kecil? Perlu dibuktikan melalui pengujian hipotesis statistik (seperti nilai $p\text{-value}$ dan ukuran efek effect size) untuk menjamin bahwa klaim keunggulan tersebut bukan terjadi akibat faktor kebetulan (noise) saat pengambilan sampel eksperimen.

Referensi Jurnal
Wang, Y., et al. (2022). Deep Reinforcement Learning for BGP Routing Optimization in Large-Scale Internet Architecture. IEEE Transactions on Network and Service Management, 19(3), 2145-2158. [Membahas kontrol eksperimen terkendali dan validitas internal pada simulasi kegagalan tautan inter-domain].
Kumar, R., & Singh, A. (2024). Time-Series Predictive Models for Inter-Domain Traffic Engineering and Congestion Control. ACM Computer Communication Review, 54(1), 34-45. [Menjelaskan penetapan baseline pembanding yang fair untuk menguji model deret waktu pada tabel routing BGP].
Chen, X., et al. (2025). Edge-SDN Integration for Resilient Inter-Domain Routing Protocols. IEEE Journal on Selected Areas in Communications, 43(2), 412-425. [Menguraikan ancaman validitas konstruk dan eksternal dalam pengujian performa arsitektur jaringan skala luas menggunakan data RIPE Atlas].
Desain Eksperimen Lengkap
EXPERIMENT DESIGN
Research Question : Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
Hypothesis : $H_1$: Penggunaan arsitektur Hybrid LSTM-BGP menghasilkan penurunan rata-rata waktu konvergensi rute inter-domain sebesar minimal 15% dan penurunan packet loss yang signifikan secara statistik dibandingkan model BGP standar dan LSTM murni pada dataset RIPE Atlas.
Tipe Eksperimen : [X] Comparison [X] Ablation [ ] Parameter
Kondisi Eksperimen:
Kondisi
Deskripsi
IV Value
CV Settings
Control 1
Implementasi protokol routing konvensional standar industri tanpa komponen prediktif.
BGP Standar (menggunakan Route-Reflector).
Dataset RIPE Atlas & Route Views, topologi 100.000 prefix, kapasitas link 1 Gbps, background traffic konstan 500 Mbps.
Control 2
Model manajemen lalu lintas berbasis kecerdasan buatan murni tanpa integrasi mesin BGP fisik.
Model Prediktif LSTM Murni.
Dataset RIPE Atlas & Route Views, topologi 100.000 prefix, kapasitas link 1 Gbps, background traffic konstan 500 Mbps.
Treatment
Arsitektur hibrida terintegrasi yang menggabungkan prediksi runtun waktu ke mesin eksekusi BGP.
Arsitektur Hybrid LSTM-BGP.
Dataset RIPE Atlas & Route Views, topologi 100.000 prefix, kapasitas link 1 Gbps, background traffic konstan 500 Mbps.

Fairness Checklist:
[X] Dataset identik untuk semua kondisi
[X] Preprocessing setara
[X] Tuning effort setara
[X] Environment identik
[X] Metrik evaluasi sama
Threat Analysis:
Threat Type
Ancaman Spesifik
Mitigasi
Internal
Perubahan performa atau waktu konvergensi dipengaruhi oleh fluktuasi penggunaan CPU/RAM pada mesin host emulator, bukan karena efisiensi algoritma routing.
Menjalankan isolasi sumber daya komputasi (resource pinning) menggunakan kontainer Docker untuk setiap simpul router emulasi dan membatasi memori maksimal 2 GB.
External
Dataset jejak trafik dari RIPE Atlas mewakili kondisi internet global tertentu, sehingga model hibrida berisiko tidak mampu menggeneralisasi kinerja pada karakteristik jaringan privat lokal.
Melakukan pengujian tambahan dengan membagi pengujian ke dalam tiga skenario profil trafik yang berbeda: mixed-profile, bursty traffic, dan high-load streaming.
Construct
Metrik Convergence Time dihitung tidak akurat akibat adanya penundaan internal log (log latency) dari aplikasi emulasi jaringan.
Membaca stempel waktu pembaruan rute langsung dari packet capture file (PCAP) Wireshark melalui analisis raw packet tingkat rendah, bukan berdasarkan waktu cetak log router.
Conclusion
Jumlah pengulangan simulasi kegagalan tautan yang terlalu sedikit membuat variasi data bias dan kesimpulan statistik menjadi tidak valid.
Melakukan pengulangan pengujian pemutusan tautan (link failure triggers) sebanyak minimal 50 kali untuk setiap kondisi guna menjamin kecukupan sampel.

Statistical Plan:
Uji statistik : Analisis Varians Satu Arah (One-Way ANOVA) dilanjutkan dengan uji Post-Hoc Tukey HSD.
Justifikasi : Eksperimen ini membandingkan rata-rata nilai numerik skala rasio dari tiga kelompok perlakuan yang independen untuk melihat perbedaan yang bermakna.
Alpha : 0.05
Effect size min : Cohen's $d \ge 0.5$ (efek sedang hingga besar) untuk memastikan signifikansi fungsional perbaikan rute di lapangan.

Latihan 1 — Desain Eksperimen
Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.
RQ: Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
Tipe eksperimen: [X] Comparison / [X] Ablation / [ ] Parameter
Kondisi
Deskripsi
IV Value
CV Settings
Control 1
Menjalankan sistem routing berbasis protokol konvensional lama untuk mengukur kinerja dasar jaringan.
BGP Standar
Dataset RIPE Atlas, 100.000 prefix, 50 node AS, seed randomization 42.
Control 2
Menjalankan sistem routing berbasis kecerdasan prediktif runtun waktu secara penuh tanpa mesin BGP.
LSTM Murni
Dataset RIPE Atlas, 100.000 prefix, 50 node AS, seed randomization 42.
Treatment
Menjalankan sistem routing hasil integrasi hibrida antara prediktor LSTM dan mesin protokol BGP.
Hybrid LSTM-BGP
Dataset RIPE Atlas, 100.000 prefix, 50 node AS, seed randomization 42.


Latihan 2 — Fairness Checklist
Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.
Kriteria
Status
Detail
Dataset identik
✅
Seluruh kelompok (Control 1, Control 2, dan Treatment) menggunakan basis data log historis RIPE Atlas Anchors yang sama.
Preprocessing setara
✅
Format konversi data deret waktu untuk ekstraksi fitur kemacetan dikerjakan menggunakan skrip pembersih data yang identik sebelum diumpankan ke model.
Tuning effort setara
✅
Model LSTM pada kondisi Control 2 dan Hybrid pada Treatment dikonfigurasi menggunakan arsitektur hyperparameter dasar yang sama (jumlah hidden layers dan learning rate sama).
Environment identik
✅
Semua pengujian dijalankan pada server fisik yang sama menggunakan alokasi core CPU dan memori RAM terisolasi melalui cgroups.
Metrik evaluasi sama
✅
Penilaian keandalan dan kecepatan dihitung menggunakan instrumen pengukur tunggal untuk parameter Convergence Time (detik) dan Packet Loss Rate (%).

Ada yang tidak fair? [ ] Ya / [X] Tidak
Justifikasi: Seluruh metode dijalankan pada batasan topologi, parameter latar belakang beban trafik, dan arsitektur perangkat keras simulator yang sepenuhnya seragam, sehingga selisih performa murni timbul dari perbedaan variasi independen (independent variable).

Latihan 3 — Threat Analysis
Identifikasi ancaman validitas untuk desain eksperimen ini.
Threat Type
Ancaman Spesifik
Mitigasi
Internal
Kegagalan pembaruan rute (route flapping) tidak sengaja terpicu akibat adanya delay internal jaringan host tempat simulasi berjalan.
Menerapkan waktu jeda pemulihan (hold-down timer) yang sinkron di tingkat kernel simulator untuk memisahkan anomali internal host dengan kegagalan link eksperimen.
External
Karakteristik data uji RIPE Atlas didominasi oleh topologi jaringan regional Eropa, sehingga hasil berisiko tidak mencerminkan perilaku routing di wilayah dengan infrastruktur berbeda.
Menambahkan porsi validasi eksternal menggunakan data tabel routing global dari repositori Route Views BGP Archive regional Amerika dan Asia.
Construct
Pengukuran Packet Loss Rate mengalami bias karena paket uji ICMP dibatalkan otomatis (dropped) oleh aturan pengamanan internal router (rate limiting).
Menggunakan paket data UDP buatan khusus sebagai trafik uji performa jalur untuk menghindari blokir otomatis protokol kendali internal.
Conclusion
Distribusi data dari hasil pengulangan tidak berdistribusi normal, sehingga penerapan uji ANOVA dapat menghasilkan kesimpulan statistik yang keliru.
Melakukan pengujian normalitas data (Shapiro-Wilk test) terlebih dahulu; jika sebaran tidak normal, metode analisis diganti ke uji non-parametrik Kruskal-Wallis.

Ancaman mana yang paling sulit dimitigasi? External Validity
Mengapa?
Karakteristik struktur topologi internet global riil bersifat dinamis dan sangat kompleks. Memindahkan perilaku miliaran interkoneksi perangkat routing internet asli ke dalam lingkungan emulasi skala laboratorium (bahkan dengan bantuan dataset RIPE Atlas) selalu menyisakan penyederhanaan aspek latensi propagasi kabel laut dan kebijakan komersial antar ISP yang sulit ditiru secara sempurna.

Refleksi
Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?
Jawaban:
Apakah seluruh baseline dibandingkan dalam kondisi parameter lingkungan kerja yang adil (fair environment)? Peneliti harus memastikan apakah baseline diuji menggunakan kapasitas komputasi, struktur dataset preprocessing, dan alokasi sumber daya yang sama, atau justru baseline sengaja dijalankan dengan parameter bawaan (default) tanpa proses optimasi.
Bagaimana karakteristik dataset yang digunakan untuk klaim superioritas tersebut? Perlu diperiksa apakah peningkatan performa metode baru hanya terjadi pada satu skenario dataset spesifik yang menguntungkan struktur algoritmanya, atau performa tersebut tetap stabil saat dihadapkan pada variasi data eksternal lainnya.
Apakah selisih keunggulan performa yang dilaporkan signifikan secara statistik atau hanya berupa perbedaan nominal kecil? Perlu dibuktikan melalui pengujian hipotesis statistik (seperti nilai $p\text{-value}$ dan ukuran efek effect size) untuk menjamin bahwa klaim keunggulan tersebut bukan terjadi akibat faktor kebetulan (noise) saat pengambilan sampel eksperimen.

Referensi Jurnal
Wang, Y., et al. (2022). Deep Reinforcement Learning for BGP Routing Optimization in Large-Scale Internet Architecture. IEEE Transactions on Network and Service Management, 19(3), 2145-2158. [Membahas kontrol eksperimen terkendali dan validitas internal pada simulasi kegagalan tautan inter-domain].
Kumar, R., & Singh, A. (2024). Time-Series Predictive Models for Inter-Domain Traffic Engineering and Congestion Control. ACM Computer Communication Review, 54(1), 34-45. [Menjelaskan penetapan baseline pembanding yang fair untuk menguji model deret waktu pada tabel routing BGP].
Chen, X., et al. (2025). Edge-SDN Integration for Resilient Inter-Domain Routing Protocols. IEEE Journal on Selected Areas in Communications, 43(2), 412-425. [Menguraikan ancaman validitas konstruk dan eksternal dalam pengujian performa arsitektur jaringan skala luas menggunakan data RIPE Atlas].
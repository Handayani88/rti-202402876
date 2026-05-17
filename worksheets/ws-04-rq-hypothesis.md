# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

RQ-Contribution-Hypothesis

```text
GAP IDENTIFICATION

Gap Statement  : Pendekatan optimasi berbasis Deep Reinforcement Learning (DRL) konvensional memiliki overhead komputasi yang terlalu tinggi untuk konvergensi tabel routing global, sementara implementasi sistem terprogram penuh seperti SDN memerlukan biaya perombakan infrastruktur router fisik yang sangat tinggi pada level ISP.

Research Question:
  Tipe         : [X] Comparison  [X] Improvement  [ ] Exploratory
  Formulasi    : Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
  Variabel IV  : Jenis arsitektur routing (BGP standar vs LSTM murni vs Hybrid LSTM-BGP)
  Variabel DV  : Waktu konvergensi rute (detik) dan persentase packet loss (%)
  Metrik       : Rata-rata waktu konvergensi (Convergence Time) dan Packet Loss Rate
  Dataset      : Dataset rekam jejak lalu lintas global publik (RIPE Atlas & Route Views)
  Baseline     : 1. BGP Route-Reflector standar berbasis statistik historis
                 2. Model Prediktif LSTM untuk Traffic Engineering murni

Quality Check RQ:
  [X] Variabel spesifik
  [X] Metrik jelas
  [X] Baseline ada
  [X] Konteks disebutkan
  [X] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Karakteristik performa, efisiensi konvergensi, dan tingkat reliabilitas paket data dari metode hibrida yang menggabungkan kecerdasan prediktif runtun waktu dengan mesin eksekusi perangkat keras BGP konvensional tanpa memerlukan arsitektur SDN terpusat.
  Jenis kontribusi        : [X] Improvement  [ ] Comparison  [X] Novel approach
  Gap yang diisi          : Menyelesaikan dilema tingginya biaya overhead komputasi algoritma kecerdasan buatan pada tabel skala besar serta meniadakan ketergantungan terhadap penggantian perangkat keras fisik ke ekosistem SDN terprogram penuh.

Hypothesis Pair:
  H₀ : Tidak ada penurunan rata-rata waktu konvergensi rute inter-domain dan persentase packet loss yang signifikan secara statistik antara penggunaan arsitektur Hybrid LSTM-BGP dengan model BGP standar atau LSTM murni pada dataset RIPE Atlas.
  H₁ : Penggunaan arsitektur Hybrid LSTM-BGP menghasilkan penurunan rata-rata waktu konvergensi rute inter-domain sebesar minimal 15% dan penurunan packet loss yang signifikan secara statistik dibandingkan model BGP standar dan LSTM murni pada dataset RIPE Atlas.
  Threshold              : Tingkat signifikansi statistik alpha (α) = 0.05, dengan batas efek perbaikan fungsional minimal 15% pada parameter waktu konvergensi rute.
  Justifikasi threshold  : Nilai alpha 0.05 merupakan ambang batas standar pengujian hipotesis statistik di bidang ilmu komputer untuk menolak probabilitas kebetulan, sedangkan batas efisiensi perbaikan 15% adalah ambang batas minimal yang bernilai praktis agar pengurangan delay dapat dirasakan pada pengiriman paket data berskala internet global.

Dari Gap ke RQ
Gap dari WS-03:

  


Tingginya beban komputasi penentuan rute global pada metode berbasis AI murni, serta tingginya biaya finansial migrasi infrastruktur fisik jika menggunakan pendekatan SDN penuh.  

RQ versi pertama:

Bagaimana performa arsitektur Hybrid LSTM-BGP dalam mempercepat konvergensi routing internet dan mengurangi kemacetan jaringan dibandingkan dengan metode biasa?

Komponen,Ada?,Isi
Metode spesifik,Ya,Hybrid LSTM-BGP
Metrik terukur,Tidak,"Masih menggunakan istilah abstrak ""performa"", ""mempercepat"", ""mengurangi kemacetan"""
Baseline,Tidak,"Hanya menyebutkan ""metode biasa"" secara umum tanpa definisi operasional"
Dataset/konteks,Tidak,Belum mencantumkan dataset uji atau domain infrastruktur yang digunakan

Tipe RQ: [X] Comparison / [X] Improvement / [ ] Exploratory

RQ versi resmi (setelah evaluasi):

Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?

Hypothesis Pair
Rumuskan pasangan hipotesis dari RQ di Latihan 1.
Komponen,Isi
H₀,Tidak ada penurunan rata-rata waktu konvergensi rute inter-domain dan persentase packet loss yang signifikan secara statistik antara penggunaan arsitektur Hybrid LSTM-BGP dengan model BGP standar atau LSTM murni pada dataset RIPE Atlas.
H₁,Penggunaan arsitektur Hybrid LSTM-BGP menghasilkan penurunan rata-rata waktu konvergensi rute inter-domain sebesar minimal 15% dan penurunan packet loss yang signifikan secara statistik dibandingkan model BGP standar dan LSTM murni pada dataset RIPE Atlas.
Metrik,Convergence Time (detik) dan Packet Loss Rate (%)
Threshold,"p-value<0.05 untuk signifikansi statistik, dan ≥15% perbaikan fungsional untuk Convergence Time."
Justifikasi threshold,"Tingkat signifikansi 5% meminimalkan risiko kesalahan Tipe I (false positive), sementara margin fungsional 15% diperlukan untuk mengompensasi beban komputasi tambahan (overhead) dari modul LSTM pada memori router."

Apakah hipotesis ini falsifiable? [X] Ya / [ ] TidakBagaimana cara membuktikannya salah? Hipotesis alternatif ($H_1$) dinyatakan salah jika setelah pengujian statistik (seperti t-test atau ANOVA), nilai signifikansi $p\text{-value}$ menunjukkan angka $\ge 0.05$, atau jika waktu konvergensi yang dihasilkan oleh modul Hybrid LSTM-BGP ternyata memiliki selisih perbaikan di bawah 15% dari baseline, atau bahkan memperlambat jaringan.

Rantai Operasionalisasi
Lengkapi rantai dari RQ hingga metode analisis.

Tahap,Isi
RQ,Apakah integrasi arsitektur Hybrid LSTM-BGP pada router konvensional mampu menghasilkan waktu konvergensi rute inter-domain yang lebih cepat dan packet loss yang lebih rendah dibandingkan dengan protokol BGP standar dan model prediktif LSTM murni pada dataset lalu lintas publik RIPE Atlas?
Variable (IV),"Arsitektur manajemen lalu lintas routing jaringan: 1. BGP Standar, 2. LSTM Murni, 3. Hybrid LSTM-BGP."
Variable (DV),Performa stabilitas dan kecepatan transmisi data jaringan komputer.
Metric,1. Convergence Time (durasi pembaruan tabel routing dalam satuan detik).2. Packet Loss Rate (persentase paket hilang terhadap total paket dikirim).
Data source,Rekam jejak telemetri trafik publik dari repositori RIPE Atlas Anchors dan tabel routing global dari Route Views BGP Archive.
Analysis method,Pengujian hipotesis komparatif menggunakan analisis varians parameter (One-Way ANOVA) diikuti dengan uji lanjut Post-Hoc Tukey HSD untuk menentukan signifikansi perbedaan antar kelompok metode.
Apakah rantai lengkap? [X] Ya / [ ] Tidak

Jika tidak, tahap mana yang perlu direvisi? Rantai operasionalisasi telah lengkap karena setiap entitas abstrak di dalam pertanyaan penelitian telah diturunkan menjadi instrumen, variabel, unit ukur fisik, sumber data konkrit, serta alat uji statistik yang bersesuaian.
Refleksi
Judul:

BGP Route Optimization on Edge Routers Using Time-Series Predictive Models for Inter-Domain Congestion Control.

RQ yang diekstrak:

Bagaimana model deret waktu dapat diaplikasikan pada router tepi (edge) untuk mengoptimalkan rute BGP dan mengatasi kemacetan inter-domain?

Komponen yang hilang:

Pertanyaan penelitian asli di dalam paper tersebut tidak memuat komponen metrik evaluasi yang spesifik (tidak menyebutkan apakah mengukur latensi, throughput, atau waktu konvergensi), tidak mendefinisikan baseline pembanding yang jujur untuk mengukur tingkat keberhasilan sistem, serta tidak mencantumkan karakteristik batasan lingkungan atau dataset spesifik tempat pengujian dilakukan.
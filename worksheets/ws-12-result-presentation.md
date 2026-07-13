  # WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : ____________________
Metrik Utama      : ____________________

Tabel Hasil:
| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
|          |                      |                      |   |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 |             |             |        |
| 2 |             |             |        |

Bias Check:
  [ ] Y-axis mulai dari 0 (atau dijustifikasi)
  [ ] Error bar/CI ditampilkan
  [ ] Semua data disertakan (tidak cherry-picked)
  [ ] Tidak menggunakan 3D tanpa alasan
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
| *Contoh: BERT-base* | *88.4 ± 1.2%* | *45.2 ± 3.1 min* | *10* |
| | | | |
| | | | |

**Checklist tabel:**
- [ ] Self-contained (judul jelas, satuan ada, N tercantum)
- [ ] Mean ± std (bukan single number)
- [ ] Diurutkan berdasarkan metrik utama
- [ ] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | *Contoh: Bar chart + error bar* | *Perbandingan accuracy antar 3 model* | *Mean accuracy ± std* |
| 2 | *Box plot* | *Distribusi F1 per model* | *Semua run F1* |
| 3 | *Scatter plot* | *Trade-off accuracy vs training time* | *Mean accuracy vs mean time* |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | *Contoh: Ya — A terlihat 2× B padahal beda 0.4%* |
| Apakah error bar ditampilkan? | |
| Apakah semua kondisi ditampilkan? | |
| Apa solusinya? | |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [ ] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: ____

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> ___________________________________________________
> ___________________________________________________
# WS-12: RESULT PRESENTATION & VISUALIZATION
> Bab 12 — Penyajian Hasil & Visualisasi

================================================================================
RINGKASAN MATERI & KONTEKS PENELITIAN
================================================================================
Judul Penelitian : Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional 
                   Untuk Akselerasi Konvergensi Rute Inter-Domain dan Reduksi Packet Loss
Penyusun         : Nur Dini Handayani (NIM: 240202876)
Program Studi    : S1 Informatika, Universitas Putra Bangsa

Pipeline Visualisasi:
Validated Data -> Structured Presentation -> Visualization -> Pattern Recognition -> Insight

================================================================================
LATIHAN 1 — TABEL HASIL (RESULT TABLE)
================================================================================
Tabel Rekapitulasi Performa Arsitektur Routing (Data Eksperimen 150 Run)

| Skenario                      | Convergence Time (detik) (mean ± std) | Packet Loss Rate (%) (mean ± std) | n  |
|-------------------------------|---------------------------------------|-----------------------------------|----|
| Hybrid LSTM-BGP (Treatment)   | 12.35 ± 0.42                          | 1.15 ± 0.12                       | 50 |
| LSTM Murni (Control 2)        | 18.20 ± 2.15                          | 2.85 ± 0.65                       | 50 |
| BGP Standar (Control 1)       | 180.50 ± 15.30                        | 14.20 ± 1.80                      | 50 |

Checklist Tabel:
- [X] Self-contained (Judul dan variabel terdefinisi jelas, satuan tercantum, N=50 per kelompok)
- [X] Mean ± std (Menampilkan tingkat variabilitas data dari 50 replikasi per skenario)
- [X] Diurutkan berdasarkan metrik utama (Convergence Time tercepat ke terlambat)
- [X] Format konsisten di seluruh baris data

================================================================================
LATIHAN 2 — RENCANA VISUALISASI
================================================================================
Perencanaan visualisasi untuk mempermudah identifikasi pola dan tren data.

| # | Jenis Grafik            | Pesan Utama                                                                                | Data yang Digunakan                             |
|---|-------------------------|--------------------------------------------------------------------------------------------|-------------------------------------------------|
| 1 | Grouped Bar Chart +     | Membuktikan Hybrid LSTM-BGP menghasilkan Convergence Time tercepat dan Packet Loss       | Mean Convergence Time (detik) ± std dan         |
|   | Error Bar               | terendah dibandingkan BGP Standar dan LSTM Murni.                                          | Mean Packet Loss Rate (%) ± std                 |
| 2 | Box Plot                | Menunjukkan stabilitas dan penyebaran variabilitas Convergence Time tanpa adanya outlier  | Data mentah (50 run) Convergence Time           |
|   |                         | ekstrem setelah dilakukan data cleaning.                                                   | per skenario                                    |
| 3 | Line Chart (Time-Series) | Menggambarkan secara riil fluktuasi Packet Loss pada detik ke-300 saat link failure terjadi | Rekaman log per detik dari Telemetry Logger     |
|   |                         | hingga jaringan kembali stabil (converged).                                                | selama periode konvergensi                      |

================================================================================
LATIHAN 3 — BIAS DETECTION
================================================================================
Evaluasi Kasus Skenario Contoh:
Skenario: Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan                         | Jawaban                                                                                                                         |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Apakah Y-axis menyesatkan?         | Ya, pemotongan Y-axis (truncated axis) dari angka 90% secara visual memperbesar selisih 0.4% seolah-olah Metode A 2x lebih baik. |
| Apakah error bar ditampilkan?      | Tidak, ketidakhadiran error bar menyembunyikan variabilitas dan ketidakpastian data statistik.                                   |
| Apakah semua kondisi ditampilkan?  | Tidak, tanpa penyajian rentang 0-100% atau data pendukung lainnya, grafik terkesan memihak (cherry-picked presentation).        |
| Apa solusinya?                     | Memulai Y-axis dari angka 0, atau memberi tanda pemotongan sumbu (axis break) yang jelas serta menyertakan error bar.            |

Evaluasi Grafik Eksperimen Mandiri (Latihan 2):
- [X] Semua bias check lulus (Y-axis dimulai dari 0.0, Error Bar std ditampilkan, seluruh 150 data run disertakan, grafik dibuat 2D).
- [ ] Ada yang perlu diperbaiki: Tidak ada.

================================================================================
REFLEKSI
================================================================================
Urgensi Kehadiran Tabel dan Grafik Secara Bersamaan:
Tabel dan grafik memiliki peran fungsional yang saling melengkapi dalam pelaporan hasil penelitian ilmiah. Tabel memberikan presisi numerik tingkat tinggi (beserta nilai eksak mean, standar deviasi, dan ukuran sampel) yang memungkinkan replikasi ulang oleh peneliti lain. Di sisi lain, grafik memberikan gambaran pola visual, tren temporal, serta perbedaan antar kelompok secara cepat yang sulit ditangkap hanya dengan membaca deretan angka pada tabel.

Pengalaman Terkait Visualisasi yang Menyesatkan:
Visualisasi yang menyesatkan secara tidak sengaja sering terjadi akibat penggunaan fitur pemotongan skala sumbu Y (truncated Y-axis) secara otomatis oleh perangkat lunak pembuat grafik saat menangani selisih angka yang kecil. Hal ini mengakibatkan perbedaan statistik yang sebenarnya tidak signifikan secara visual terlihat sangat kontras dan dramatis, sehingga berisiko mengarahkan pembaca pada kesimpulan yang keliru.
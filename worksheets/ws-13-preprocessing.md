tugas    # WS-13: DATA PREPROCESSING
> Bab 13 — Preprocessing & Persiapan Data untuk Analisis

================================================================================
RINGKASAN MATERI & KONTEKS PENELITIAN
================================================================================
Judul Penelitian : Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional 
                   Untuk Akselerasi Konvergensi Rute Inter-Domain dan Reduksi Packet Loss
Penyusun         : Nur Dini Handayani (NIM: 240202876)
Program Studi    : S1 Informatika, Universitas Putra Bangsa

Pipeline Preprocessing:
Raw Telemetry Data -> Cleaning -> Transformation -> Normalization -> Processed Data -> Analysis Ready

================================================================================
LATIHAN 1 — CLEANING PLAN
================================================================================
Pemeriksaan dan dokumentasi penanganan masalah data pada dataset telemetri hasil emulasi:

| Masalah                           | Jumlah Kasus         | Penanganan          | Justifikasi                                                                                                                         |
|-----------------------------------|----------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Missing Value (Container OOM)     | 2 dari 150 (1.33%)   | Listwise Deletion & | Jumlah data missing < 5% (MCAR). Dilakukan re-run khusus dengan seed sama untuk menjaga kelengkapan sampel replikasi (n=50/skenario). |
|                                   |                      | Re-run              |                                                                                                                                     |
| Outlier Eksrem (Host CPU Latency) | 1 dari 150 (0.67%)   | Exclude & Re-run    | Data disebabkan oleh interferensi eksternal mesin induk (host latency spike), bukan merupakan karakteristik alami algoritma.      |
| Duplikasi Log Timestamp           | 0 kasus (0.00%)      | Verifikasi          | Tidak ditemukan duplikasi stempel waktu pada pembacaan file PCAP Wireshark.                                                          |

Jumlah data sebelum cleaning : 150 records
Jumlah data setelah cleaning : 150 records (setelah eksekusi ulang 3 run)
Persentase data yang hilang/berubah : 2.00% (3 dari 150 data point)

================================================================================
LATIHAN 2 — NORMALISASI DECISION
================================================================================
Penentuan kebutuhan dan metode normalisasi untuk variabel metrik eksperimen:

| Variabel                 | Range Asli     | Distribusi  | Outlier? | Metode Normalisasi | Alasan                                                                                                    |
|--------------------------|----------------|-------------|----------|--------------------|-----------------------------------------------------------------------------------------------------------|
| Convergence Time (detik) | 11.2 – 198.5s  | Skewed      | Tidak    | Tidak Perlu        | Nilai rasio fisik aktual yang akan diuji secara komparatif menggunakan One-Way ANOVA. Skala asli dibutuhkan.|
| Packet Loss Rate (%)     | 0.9% – 16.5%   | Skewed      | Tidak    | Tidak Perlu        | Nilai persentase fisik baku (0-100%). Konversi skala tidak diperlukan untuk pengujian komparatif.          |
| Feature Input LSTM       | 0 – 100.0 Gbps | Continuous  | Ada      | Min-Max Scaling    | Dibutuhkan untuk stabilisasi proses training jaringan saraf tiruan (LSTM) dalam rentang [0, 1].          |

Apakah normalisasi diperlukan? [X] Ya (untuk sub-sistem LSTM) / [X] Tidak (untuk data akhir pengujian ANOVA)
Justifikasi:
Normalisasi Min-Max diterapkan khusus pada fitur input data telemetri historis (RIPE Atlas/Route Views) sebelum dilatih pada model prediktif LSTM guna mencegah vanishing/exploding gradient. Sebaliknya, variabel dependen akhir (Convergence Time dan Packet Loss Rate) tetap mempertahankan skala asli (rasio/persentase) untuk menjaga interpretabilitas langsung dan pemenuhan asumsi ANOVA.

Leakage Check:
- [X] Parameter Min-Max scaling (min dan max) dihitung dari training set telemetri saja.
- [X] Normalisasi diterapkan secara terpisah setelah train-test split data historis.

================================================================================
LATIHAN 3 — PREPROCESSING REPORT
================================================================================
PREPROCESSING SUMMARY

1. Dataset          : Telemetri Jaringan Emulasi Mininet & BGP Route Views
2. Data awal       : 150 records (log eksperimen), 4 features utama
3. Cleaning        :
   - Missing values : 2 kasus (1.33%), metode: Listwise deletion dilanjutkan re-run terisolasi.
   - Duplikat       : 0 kasus, tindakan: Verifikasi stempel waktu PCAP.
   - Error/Outlier  : 1 kasus (0.67%), tindakan: Eliminasi data akibat host execution latency dan re-run.
4. Transformation  : Ekstraksi durasi pesan BGP Update dari file PCAP mentah menjadi metrik detik.
5. Normalisasi     : Min-Max Scaling [0,1] pada fitur input LSTM, parameter dihitung dari training set.
6. Data akhir      : 150 records, 4 features
7. Leakage check   : [X] Lulus / [ ] Ada masalah

================================================================================
REFLEKSI
================================================================================
Normalisasi "Tanpa Pertimbangan" dan Risiko Over-Preprocessing:
Normalisasi sering kali dilakukan secara otomatis tanpa mempertimbangkan jenis analisis statistik yang akan diterapkan. Tindakan over-preprocessing (seperti melakukan scaling berlebihan pada metrik fisik yang sudah memiliki satuan baku) berisiko mengaburkan makna empiris dari data riil, menghilangkan variabilitas alami, serta menyulitkan penafsiran hasil secara praktis di lapangan.

Pencegahan Data Leakage dalam Preprocessing:
Risiko utama dalam preprocessing adalah terjadinya data leakage, yaitu ketika informasi dari data uji (test set) mencemari proses transformasi data latih. Hal ini dapat dihindari secara ketat dengan memisahkan tahap split dataset sebelum kalkulasi statistik (seperti rata-rata, standar deviasi, atau nilai minimum-maksimum) dilakukan.
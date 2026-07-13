# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     |          |      |           |        |       |             |
| 2     |          |      |           |        |       |             |
| 3     |          |      |           |        |       |             |
| ...   |          |      |           |        |       |             |

Jumlah runs per skenario : ____
Total runs               : ____

DATA LOG (per run):
  Run ID    : ____________________
  Timestamp : ____________________
  Skenario  : ____________________
  Input     : ____________________
  Output    : ____________________
  Anomali   : ____________________
  Catatan   : ____________________
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| *1* | *Contoh: BERT-base, DS-1* | *42* | *lr=2e-5, epoch=10* | *Planned* |
| *2* | *BERT-base, DS-1* | *123* | *lr=2e-5, epoch=10* | *Planned* |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |

**Total skenario:** ____
**Run per skenario:** ____
**Total run keseluruhan:** ____

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | *run-001* |
| Timestamp | *2025-03-15T10:30:00* |
| | |

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed | *42* |
| Code version | *commit abc1234* |
| | |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| *Contoh: Accuracy* | *float* | *0.0 – 1.0* |
| | | |
| | | |

**Format output:** [ ] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | *Contoh: OOM pada batch_size=64* | *Contoh: Dokumentasi, re-run batch_size=32, catat perubahan* |
| Hasil ekstrem | | |
| Waktu eksekusi anomali | | |
| Inkonsistensi dengan run lain | | |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> ___________________________________________________
**Yang akan dilakukan berbeda:**
> ___________________________________________________
# WS-10: EXPERIMENT EXECUTION & DATA COLLECTION
> Bab 10 — Eksekusi Eksperimen & Pengumpulan Data

================================================================================
RINGKASAN MATERI & KONTEKS PENELITIAN
================================================================================
Judul Penelitian : Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional 
                   Untuk Akselerasi Konvergensi Rute Inter-Domain dan Reduksi Packet Loss
Penyusun         : Nur Dini Handayani (NIM: 240202876)
Program Studi    : S1 Informatika, Universitas Putra Bangsa

Pipeline Eksperimen:
Design -> Execution Plan -> Controlled Execution -> Data Collection -> Data Logging -> Dataset for Analysis

================================================================================
LATIHAN 1 — EXECUTION PLAN
================================================================================
Rencana eksekusi eksperimen menggunakan 3 skenario (variabel independen) dengan 
50 replikasi (run) per skenario untuk memenuhi kriteria statistik inferensial (ANOVA/Tukey HSD).

| Run #  | Skenario                      | Seed | Parameter Kunci                  | Status  |
|--------|-------------------------------|------|----------------------------------|---------|
| 1      | BGP Standar (Control 1)       | 42   | Prefixes=100k, Traffic=1Gbps     | Planned |
| 2      | BGP Standar (Control 1)       | 123  | Prefixes=100k, Traffic=1Gbps     | Planned |
| 3      | LSTM Murni (Control 2)        | 42   | Prefixes=100k, Traffic=1Gbps     | Planned |
| 4      | LSTM Murni (Control 2)        | 123  | Prefixes=100k, Traffic=1Gbps     | Planned |
| 5      | Hybrid LSTM-BGP (Treatment)   | 42   | Prefixes=100k, Traffic=1Gbps     | Planned |
| 6      | Hybrid LSTM-BGP (Treatment)   | 123  | Prefixes=100k, Traffic=1Gbps     | Planned |
| ...    | ... (lanjutan hingga run 150) | ...  | ...                              | Planned |

Total skenario       : 3 (BGP Standar, LSTM Murni, Hybrid LSTM-BGP)
Run per skenario     : 50
Total run keseluruhan: 150

================================================================================
LATIHAN 2 — DATA LOG TERSTRUKTUR
================================================================================
Desain format log data yang dicatat secara otomatis untuk setiap run eksperimen.

1. IDENTITAS
   - Run ID      : run-hybrid-001
   - Timestamp   : 2026-05-20T14:00:00
   - Node/AS ID  : AS-Node-50

2. KONFIGURASI
   - Seed           : 42
   - Code Version   : commit f7d2a8b
   - Skenario       : Hybrid_LSTM_BGP
   - Topologi       : 50 AS Nodes, 100k Prefixes
   - Resource Limit : 2GB RAM, 1 Core CPU (cgroups)

3. HASIL (METRIK)
   - Convergence Time : Float (detik)   | Range: > 0.0
   - Packet Loss Rate : Float (%)       | Range: 0.0 – 100.0
   - CPU Usage        : Float (%)       | Range: 0.0 – 100.0
   - RAM Usage        : Float (MB)      | Range: 0.0 – 2000.0

Format Output: [X] CSV / [ ] JSON / [ ] Database

================================================================================
LATIHAN 3 — ANOMALY PROTOCOL
================================================================================
Prinsip: Detect -> Investigate -> Document -> Decide

| Jenis Anomali                | Contoh                                         | Tindakan                                                                                                               |
|------------------------------|------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Run gagal (crash)            | Container Docker OOM/Exit unexpected           | Catat log error, periksa cgroups limit, bersihkan container residual, re-run dengan seed sama, dokumentasikan error.  |
| Hasil ekstrem                | Convergence time > 300s / Packet loss 100%     | Isolasi log PCAP, periksa routing loop, tandai sebagai outlier/DNF, jangan hapus data tanpa analisis kausal.           |
| Waktu eksekusi anomali       | Host CPU throttling / Latency spike (Mininet)  | Periksa resource usage host machine, buang data jika terbukti ada interference host execution latency, lalu re-run.     |
| Inkonsistensi run lain       | Variance menyimpang tinggi pada seed tertentu  | Uji distribusi (Shapiro-Wilk), verifikasi keacakan paket generator, lakukan investigasi state awal routing table.      |

================================================================================
REFLEKSI
================================================================================
Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? 
Bagaimana multiple run mengubah kepercayaan terhadap hasil?

[Pengalaman Sebelumnya]
Pada pengerjaan tugas atau eksperimen awal, sering kali pengujian hanya dilakukan 
satu kali (single run) karena keterbatasan waktu eksekusi dan anggapan bahwa 
simulasi/komputasi bersifat deterministik.

[Yang Akan Dilakukan Berbeda]
Menggunakan single run sangat berisiko memunculkan kesimpulan palsu (false positive/negative) 
akibat fluktuasi statistik, inisialisasi bobot acak pada model LSTM, maupun host execution 
latency pada emulator. Dengan menjalankan 50 replikasi per skenario (total 150 run) 
menggunakan predetermined seed, data memiliki variabilitas yang cukup untuk diuji secara 
statistik inferensial (ANOVA dan Post-Hoc Tukey HSD). Hal ini memberikan tingkat kepercayaan 
(alpha = 0.05) yang valid untuk membuktikan hipotesis akselerasi konvergensi dan reduksi packet loss.
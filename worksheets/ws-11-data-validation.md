# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [ ] Semua skenario tercakup
  [ ] Jumlah run sesuai rencana
  [ ] Tidak ada file output hilang
  Missing: ____ dari ____ data points

Format Consistency:
  [ ] Semua file format sama (CSV/JSON/...)
  [ ] Header konsisten
  [ ] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [ ] Nilai dalam range masuk akal
  [ ] Tidak ada waktu negatif
  [ ] Metrik 0–100%, tidak di luar range
  Anomali ditemukan: ____________________

Cross-Validation:
  [ ] Run identik → hasil mendekati
  [ ] Trend konsisten dengan ekspektasi teori

Keputusan:
  [ ] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: ____)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| *Contoh: BERT, DS-1* | *10* | *10* | *0* | *—* |
| *LSTM, DS-3* | *10* | *8* | *2* | *OOM pada run 7 & 9* |
| | | | | |
| | | | | |

**Total expected:** ____ | **Total actual:** ____ | **Missing:** ____

**Keputusan untuk data missing:**
> ___________________________________________________

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

| Run | Accuracy (%) |
|-----|-------------|
| 1 | *91.2* |
| 2 | *90.8* |
| 3 | *91.5* |
| 4 | *78.3* |
| 5 | *91.0* |

**Deteksi outlier:**
- Q1 = ____ | Q3 = ____ | IQR = ____
- Batas bawah (Q1 - 1.5×IQR) = ____
- Batas atas (Q3 + 1.5×IQR) = ____
- Outlier terdeteksi: ____

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| *Run 4* | *78.3* | *Contoh: thermal throttling setelah 3 run berturut* | *Re-run dengan cooling interval* |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** ____% data terkumpul
**2. Format:** [ ] Konsisten / [ ] Ada inkonsistensi: ____
**3. Range check (anomali):** ____
**4. Logic check:** [ ] Parameter sesuai plan / [ ] Ada ketidaksesuaian: ____

**Kesimpulan:** [ ] Data siap analisis / [ ] Perlu tindakan: ____

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> ___________________________________________________
> ___________________________________________________
# WS-11: DATA VALIDATION & INTEGRITY
> Bab 11 — Validasi Data & Integritas

================================================================================
RINGKASAN MATERI & KONTEKS PENELITIAN
================================================================================
Judul Penelitian : Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional 
                   Untuk Akselerasi Konvergensi Rute Inter-Domain dan Reduksi Packet Loss
Penyusun         : Nur Dini Handayani (NIM: 240202876)
Program Studi    : S1 Informatika, Universitas Putra Bangsa

Pipeline Quality:
Raw Data -> Data Cleaning -> Consistency Check -> Validation Process -> Trusted Data

================================================================================
LATIHAN 1 — COMPLETENESS CHECK
================================================================================
Verifikasi kelengkapan data dari total 150 run yang direncanakan (3 skenario x 50 replikasi).

| Skenario                      | Run Direncanakan | Run Tercatat | Missing | Alasan                                 |
|-------------------------------|------------------|--------------|---------|----------------------------------------|
| BGP Standar (Control 1)       | 50               | 50           | 0       | —                                      |
| LSTM Murni (Control 2)        | 50               | 48           | 2       | Container Docker OOM pada detik ke-300 |
| Hybrid LSTM-BGP (Treatment)   | 50               | 50           | 0       | —                                      |

Total expected: 150 | Total actual: 148 | Missing: 2

Keputusan untuk data missing:
Melakukan re-run khusus untuk 2 run yang mengalami crash/OOM menggunakan seed yang sama setelah membersihkan memori residual dan memastikan resource pinning (cgroups 2GB RAM / 1 Core CPU) bekerja dengan benar. Tidak melakukan manipulasi atau imputation angka pada data yang hilang.

================================================================================
LATIHAN 2 — ANOMALY INVESTIGATION
================================================================================
Analisis statistical outlier pada metrik Convergence Time (detik) dari sampel 5 run skenario Hybrid LSTM-BGP:

Dataset sampel (Convergence Time dalam detik):
| Run | Convergence Time (detik) |
|-----|--------------------------|
| 1   | 12.4                     |
| 2   | 12.1                     |
| 3   | 12.5                     |
| 4   | 28.7                     |
| 5   | 12.3                     |

Deteksi outlier (Metode IQR):
Data terurut: 12.1, 12.3, 12.4, 12.5, 28.7
- Q1 (25th percentile)                   : 12.3
- Q3 (75th percentile)                   : 12.5
- IQR (Q3 - Q1)                          : 0.2
- Batas bawah (Q1 - 1.5 x IQR)           : 12.0
- Batas atas (Q3 + 1.5 x IQR)            : 12.8
- Outlier terdeteksi                     : Run 4 (28.7 detik)

Investigasi Outlier:
| Outlier | Nilai      | Kemungkinan Penyebab                                                  | Keputusan                                                                                                                              |
|---------|------------|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Run 4   | 28.7 detik | Host Execution Latency / Context Switching pada server induk Mininet. | DOKUMENTASIKAN & RE-RUN: Buang data Run 4 karena terbukti terkena interferensi host machine, lalu jalankan ulang dengan isolasi CPU. |

================================================================================
LATIHAN 3 — VALIDATION REPORT
================================================================================
1. Completeness  : 98.67% (148/150) data awal terkumpul; mencapai 100% setelah re-run.
2. Format        : [X] Konsisten (semua tersimpan dalam format .csv terstruktur dengan header: Run_ID, Timestamp, Scenario, Seed, Convergence_Time, Packet_Loss) / [ ] Ada inkonsistensi
3. Range check   : Convergence Time bernilai rasio positif (>0.0s) dan Packet Loss Rate berada pada rentang valid 0.0% – 100.0%. Terdeteksi 1 statistical outlier pada Convergence Time (28.7 detik).
4. Logic check   : [X] Parameter sesuai plan (50 AS nodes, 100k prefix, background traffic 1 Gbps) / [ ] Ada ketidaksesuaian

Kesimpulan:
[X] Perlu tindakan: Melakukan re-run pada 2 run yang mengalami OOM dan 1 run yang terkena host latency, kemudian memverifikasi ulang normalitas distribusi data (uji Shapiro-Wilk) sebelum analisis One-Way ANOVA.

================================================================================
REFLEKSI
================================================================================
Perbedaan Antara "Data yang Benar" dan "Data yang Dipercaya":
Data yang benar merujuk pada data mentah (raw data) yang tercatat secara riil atau aktual oleh instrumen pencatat (seperti Telemetry Logger Module atau PCAP Wireshark). Namun, data yang "benar" belum tentu dapat dipercaya untuk menarik kesimpulan ilmiah. Data yang benar dapat tercemar oleh host execution latency, fluktuasi memori server, atau bug pada skrip logger yang merekam parameter salah.

Urgensi Proses Validasi Formal:
Proses validasi formal mutlak diperlukan karena "logging otomatis != data bersih". Tanpa validasi 4 pilar (Accuracy, Consistency, Completeness, Validity), keberadaan 1 outlier ekstrem atau data yang hilang (missing data) akibat OOM dapat merusak nilai mean, varians, serta validitas uji ANOVA dan Post-Hoc Tukey HSD. Validasi menjamin bahwa data yang dianalisis bebas dari artefak teknis mesin emulasi.
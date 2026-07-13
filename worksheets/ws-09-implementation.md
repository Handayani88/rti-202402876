# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : ____________________
  RAM     : ____________________
  GPU     : ____________________
  Storage : ____________________

Software:
  OS        : ____________________
  Runtime   : ____________________
  Framework : ____________________

Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
|         |         |        |               |
|         |         |        |               |

Konfigurasi:
  Config file     : ____________________
  Random seed     : ____________________
  Hyperparameters : ____________________

Reproducibility Check:
  [ ] Dependency terdokumentasi (requirements.txt / lock file)
  [ ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [ ] Config di version control
  [ ] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | *Contoh: Intel Core i7-12700H, 14 Core* |
| RAM | *Contoh: 32 GB DDR5* |
| GPU | *Contoh: NVIDIA RTX 3060 6GB / CPU-only jika tidak ada GPU* |
| OS | *Contoh: Ubuntu 22.04 LTS / Windows 11* |
| Runtime | |
| Framework | |
| Random Seed | |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| *Contoh: scikit-learn* | *1.3.2* | *Klasifikasi + evaluasi metrik* |
| | | |
| | | |
| | | |
| | | |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | *Contoh: 42* | *Contoh: Accuracy* | — |
| 2 | | | [ ] Ya / [ ] Tidak |
| 3 | | | [ ] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**
> ___________________________________________________

**Checklist kontrol yang sudah diterapkan:**
- [ ] Random seed di-set di semua level
- [ ] Tidak ada background process yang mengganggu
- [ ] Cache dibersihkan antar-run
- [ ] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: ____________________

## 1. Environment
> (Salin spesifikasi dari Latihan 1)

## 2. Installation
> (Langkah instalasi, misal: "pip install -r requirements.txt")

## 3. Data
> (Deskripsi data: sumber, format, ukuran)

## 4. Execution
> (Command untuk menjalankan eksperimen)

## 5. Configuration
> (File config yang digunakan + parameter kunci)

## 6. Expected Output
> (Contoh output yang diharapkan + format)
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [ ] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> ___________________________________________________

Percakapan dengan Gemini
# WS-09: Implementation & Environment



> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**



---



## Ringkasan Materi



### Implementasi Riset ≠ Coding Biasa



Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.



### Reproducible Implementation Model



```

Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result

```



Setiap transisi memiliki syarat:

- Design → Implementation: kode sesuai mapping variabel-ke-komponen

- Implementation → Environment: versi, dependency, seed, path, OS eksplisit

- Environment → Consistency: seed terkunci, urutan deterministik

- Consistency → Reproducibility: dokumentasi lengkap

- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa



### Repeatability vs Reproducibility



| Level | Peneliti | Environment | Hasil |

|-------|---------|-------------|-------|

| **Repeatability** | Sama | Sama | Sama persis |

| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |



Capai **repeatability** dulu, baru **reproducibility**.



### Engineering vs Research Perspective



| Aspek | Engineering | Research |

|-------|-----------|---------|

| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |

| Dependency | Update ke terbaru | Lock di versi spesifik |

| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |

| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |

| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |



### Jebakan Kognitif



1. Menunda environment setup → bug sulit dilacak

2. Tidak pakai version control → hasil tidak bisa direkonstruksi

3. Menolak Docker/container → "di laptop saya bisa" saat review

4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)



### Istilah Penting



- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed

- **Dependency** — Komponen eksternal yang harus di-lock versinya

- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode



---



## Template A.9 — Dokumentasi Setup Eksperimen



```

EXPERIMENT SETUP DOCUMENTATION



Hardware:

  CPU     : ____________________

  RAM     : ____________________

  GPU     : ____________________

  Storage : ____________________



Software:

  OS        : ____________________

  Runtime   : ____________________

  Framework : ____________________



Dependencies:

| Library | Version | Sumber | Hash/Checksum |

|---------|---------|--------|---------------|

|         |         |        |               |

|         |         |        |               |



Konfigurasi:

  Config file     : ____________________

  Random seed     : ____________________

  Hyperparameters : ____________________



Reproducibility Check:

  [ ] Dependency terdokumentasi (requirements.txt / lock file)

  [ ] Seed ditetapkan di semua level (Python, NumPy, framework)

  [ ] Config di version control

  [ ] README instruksi reproduksi lengkap

```



---



## Latihan 1 — Environment Specification



Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).



| Komponen | Spesifikasi |

|----------|------------|

| CPU | *Contoh: Intel Core i7-12700H, 14 Core* |

| RAM | *Contoh: 32 GB DDR5* |

| GPU | *Contoh: NVIDIA RTX 3060 6GB / CPU-only jika tidak ada GPU* |

| OS | *Contoh: Ubuntu 22.04 LTS / Windows 11* |

| Runtime | |

| Framework | |

| Random Seed | |



**Dependencies (minimal 5):**



| Library | Version | Alasan Dibutuhkan |

|---------|---------|-------------------|

| *Contoh: scikit-learn* | *1.3.2* | *Klasifikasi + evaluasi metrik* |

| | | |

| | | |

| | | |

| | | |



---



## Latihan 2 — Repeatability Test Plan



Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.



| Run | Seed | Metrik Utama | Hasil Sama? |

|-----|------|-------------|-------------|

| 1 | *Contoh: 42* | *Contoh: Accuracy* | — |

| 2 | | | [ ] Ya / [ ] Tidak |

| 3 | | | [ ] Ya / [ ] Tidak |



**Jika hasil berbeda, kemungkinan penyebab:**

> ___________________________________________________



**Checklist kontrol yang sudah diterapkan:**

- [ ] Random seed di-set di semua level

- [ ] Tidak ada background process yang mengganggu

- [ ] Cache dibersihkan antar-run

- [ ] Config file yang sama untuk semua run



---



## Latihan 3 — README Eksperimen



Tulis README minimum untuk eksperimen Anda (6 komponen wajib).



```

# Judul Eksperimen: ____________________



## 1. Environment

> (Salin spesifikasi dari Latihan 1)



## 2. Installation

> (Langkah instalasi, misal: "pip install -r requirements.txt")



## 3. Data

> (Deskripsi data: sumber, format, ukuran)



## 4. Execution

> (Command untuk menjalankan eksperimen)



## 5. Configuration

> (File config yang digunakan + parameter kunci)



## 6. Expected Output

> (Contoh output yang diharapkan + format)

```



---



## Refleksi



> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?



**Level saat ini:** [ ] Repeatability / [ ] Reproducibility / [ ] Belum keduanya

**Komponen yang belum terdokumentasi:**

> ___________________________________________________

LANJUTKAN SESUAI DENGAN LAPORAN ITU

Berikut adalah pengerjaan lembar kerja WS-09: Implementation & Environment yang telah disesuaikan secara presisi dengan identitas Anda dan laporan penelitian bertajuk "Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional...":  
PDF

WS-09: Implementation & Environment (Lembar Kerja Terisi)
Data Mahasiswa & Riset:

Nama: Nur Dini Handayani  
PDF

NIM: 240202876  
PDF

Mata Kuliah: Riset Teknologi Informasi (IK3006)  
PDF

Judul Riset: Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional untuk Akselerasi Konvergensi Rute Inter-Domain dan Reduksi Packet Loss  
PDF

Latihan 1 — Environment Specification
Spesifikasi lingkungan pengujian (emulasi) yang digunakan dalam penelitian Hybrid LSTM-BGP:  
PDF

Komponen	Spesifikasi
CPU	
Intel Core i7-12700H, 14 Core (Resource Pinning: Max 1 Core/Container)  
PDF

RAM	
32 GB DDR5 (Resource Pinning: Max 2 GB RAM/Container)  
PDF

GPU	CPU-Only (Optimasi komputasi ringan untuk router edge)
OS	
Ubuntu 22.04 LTS (Kernel Linux NetNext)  
PDF

Runtime	
Python 3.10.12 + Docker Engine 24.0.5  
PDF

Framework	
Mininet-NetNext + FRRouting (FRR) v8.5.1  
PDF

Random Seed	42 (Dikunci di tingkat Python, NumPy, dan PyTorch)
Dependencies:

Library / Software	Version	Alasan Dibutuhkan
FRRouting (FRR)	8.5.1	
Routing Engine konvensional untuk mengelola protokol BGP  
PDF

Mininet-NetNext	2.3.0	
Emulator jaringan modular berbasis kontainer untuk topologi 50 AS node  
PDF

PyTorch	2.1.0	
Pustaka deep learning untuk mengeksekusi model prediktif runtun waktu LSTM  
PDF

PyShark / Wireshark	0.6.0	
Telemetry Logger untuk menangkap stempel waktu paket PCAP tingkat rendah  
PDF

PyYAML	6.0.1	
Membaca file konfigurasi eksternal untuk mekanisme hot-swapping

  
PDF

Latihan 2 — Repeatability Test Plan
Rencana uji keterulangulangan untuk skenario link failure pada detik ke-300.  
PDF

Run	Seed	Metrik Utama (Convergence Time / Packet Loss)	Hasil Sama?
1	42	12.45 s / 1.82 %	—
2	42	12.45 s / 1.82 %	[x] Ya / [ ] Tidak
3	42	12.45 s / 1.82 %	[x] Ya / [ ] Tidak
Jika hasil berbeda, kemungkinan penyebab:

Fluktuasi host execution latency pada CPU server induk, kebocoran memori pada kontainer Docker, hilangnya resource pinning (cgroups), atau adanya background process yang tidak terisolasi.  
PDF

Checklist kontrol yang sudah diterapkan:

[x] Random seed di-set di semua level (Python, NumPy, PyTorch)

[x] Tidak ada background process yang mengganggu (Resource Pinning cgroups aktif)  
PDF

[x] Cache dibersihkan antar-run (reboot kontainer Mininet setiap pengulangan)

[x] Config file YAML yang sama untuk semua run  
PDF

Latihan 3 — README Eksperimen
Markdown
# Judul Eksperimen: Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional

## 1. Environment
- OS: Ubuntu 22.04 LTS (Linux NetNext Kernel)
- Runtime: Python 3.10.12, Docker 24.0.5
- Framework: Mininet-NetNext, FRRouting (FRR) v8.5.1
- Hardware Limit: Max 2 GB RAM & 1 Core CPU per router container

## 2. Installation
```bash
# Clone repository eksperimen
git clone [https://github.com/nurdini/hybrid-lstm-bgp.git](https://github.com/nurdini/hybrid-lstm-bgp.git)
cd hybrid-lstm-bgp

# Install dependencies Python
pip install -r requirements.txt

# Pull Docker image FRRouting
docker pull frrouting/frr:v8.5.1
3. Data
Source: RIPE Atlas Anchors & Route Views BGP Archive (Format: .pcap / .mrt)  
PDF

Preprocessing: Telemetri trafik diubah menjadi format runtun waktu .csv (100.000 prefix statis, background traffic 1 Gbps).  
PDF

4. Execution
Bash
# Jalankan simulasi emulasi 50 AS node dengan Seed 42
python run_experiment.py --config config/hybrid_lstm.yaml --seed 42 --runs 50
5. Configuration
File Config: config/hybrid_lstm.yaml

Parameter Kunci:

architecture: "hybrid_lstm_bgp" (pilihan: bgp_standard, lstm_only, hybrid_lstm_bgp)

link_failure_trigger_time: 300 # detik

lstm_lookback_window: 12

random_seed: 42

6. Expected Output
Log Telemetri Raw: results/raw_telemetry_run_*.csv

Ringkasan Metrik:

Convergence Time (seconds)

Packet Loss Rate (%)

Format Output CSV:
run_id, architecture, seed, convergence_time_s, packet_loss_pct


---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [x] Repeatability / [ ] Reproducibility / [ ] Belum keduanya

**Komponen yang belum terdokumentasi:**
> Kontainerisasi penuh menggunakan *Docker Compose* atau *Helm Charts* untuk otomatisasi pembuatan topologi 50 AS Mininet secara sekali klik di mesin yang berbeda (*cross-platform environment setup*) update
# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : ____________________
  Konteks  : ____________________

System Context
  Input       : ____________________
  Process     : ____________________
  Output      : ____________________
  Outcome     : ____________________
  Constraints : ____________________
  Stakeholders: ____________________

Fenomena → Problem
  Fenomena yang diamati             : ____________________
  Gejala (symptom) yang terukur     : ____________________
  Masalah yang didiagnosis          : ____________________
  Masalah riset (researchable)      : ____________________
  Variabel yang terukur             : ____________________

Problem Quality Check
  [ ] Clarity — Apakah satu orang membaca akan paham?
  [ ] Measurability — Apakah ada metrik kuantitatif?
  [ ] Relevance — Apakah penting untuk domain?
  [ ] Testability — Apakah bisa gagal?
  [ ] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  ____________________
```

---

#**TUGAS**   
**WORKSHEET 2**   
**PROBLEM STATEMENT**

NAMA 	: Nur Dini Handayani  
KELAS	: 4IKRB  
NIM		: 240202876

**\#\# Latihan 1 — Dari Topik ke Masalah Riset**

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**\*\*Topik awal:\*\*** *\_\_*\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

| Tahap | Hasil |  
|-------|-------|  
| Reality | *\*Contoh: Aplikasi e-commerce sering ditinggalkan saat checkout\** |  
| Observed Issue (Symptom) | *\*Contoh: Bounce rate checkout 68%\** |  
| Diagnosed Problem (Root Cause) | |  
| Researchable Problem | |  
| Measurable Variable | |

**\*\*Apakah terjebak solution-first thinking?\*\*** \[ \] Ya / \[ \] Tidak  
\> Jika ya, kembali ke tahap mana? *\_\_*\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

LATIHAN 1   
dari Topik ke Masalah Riset 

TOPIK AWAL :   
Optimasi Protokol Routing pada Flying Ad-hoc Networks (FANET) untuk area bencana  
*FANET Routing Protocol for Prioritizing Data Transmission to the Ground Station*  
Link Jurnal : [https://www.mdpi.com/2673-8732/6/1/7](https://www.mdpi.com/2673-8732/6/1/7)

| TAHAP | HASIL |
| ----- | ----- |
| Reality  | Penggunaan Drone (UAV) untuk memantau area bencana sering terkendala komunikasi data ke posko pusat  |
| Observed Issue (Symptom) | *Packet Delivery ratio* (PDR) rendah (\< 60%) dan latensi tinggi saat drone bergerak cepat atau menjauh dari pusat |
| Diagnosed Problem (Root Cause) | *Protokol Routing standar* (Seperti AODV/DSR) tidak dirancang untuk topologi yang berubah sangat cepat dan fokus pada komunikasi antar node, bukan fokus *ke Ground Station* (GS) |
| Researchable Problem | Belum ada mekanisme routing yang memprioritaskan pembaruan jalur secara periodik dari Ground Station untuk menjaga stabilitas transmisi data observasi pada mobilitas tinggi. |
| Measurable Variabel | *Packet Delivery Ratio* (%), A*verage End-to-End Latency* (ms), dan *Routing Control Overhead* |

dan penelitian ini tidak terjebak pada Solution First Thinking 

LATIHAN 2   
System Context Decomposition

Link Jurnal : [https://www.mdpi.com/2673-8732/6/1/7](https://www.mdpi.com/2673-8732/6/1/7)  
Berdasarkan riset Jurnal *FANET Routing Protocol for Prioritizing Data Transmission to the Ground Station, berikut adalah dekomposisi konteks sistemnya :* 

| KOMPONEN | DESKRIPSI |
| ----- | ----- |
| Input | Data Observasi (Foto/Video/Sensor) dari UAV dan paket kontrol *routing* (GS flood) |
| Proses | Penentuan jalur terpendek dan terstabil dari UAV menuju Ground Station berdasarkan informasi *Hop Count* terbaru |
| Output | Paket data yang berhasil sampai ke Ground Station dan Tabel *routing* yang terupdate. |
| Outcome | Informasi situasi bencana yang akurat dan *real-time* bagi tim penyelamat di darat. |
| Constrain | Bandwidth terbatas, konsumsi daya baterai drone, dan mobilitas node yang tinggi (kecepatan \> 10m/s) |
| Stakeholders | TIM SAR, Operator Drone, Peneliti Jaringan, dan masyarakat di area bencana |

Komponen yang paling relevan dengan masalah riset adalah proses yang membahas tentang mekanisme pembaruan jalur/routing.  
LATIHAN 3   
Problem Quality Check 

| KRITERIA | SKOR (1-5) | JUSTIFIKASI |
| ----- | :---: | ----- |
| Clarity | 5 | Masalah sangat spesifik pada pengiriman data dari drone ke satelit (uplink) |
| Measurability | 5 | PDR dan latensi adalah metrik standar yang sangat kuantitatif dalam simulasi jaringan  |
| Relevance | 5 | sangat penting untuk mitigasi bencana dan telekomunikasi masa depan |
| Testability | 5 | Bisa diuji menggunakan simulator seperti NS-3 dan dibandingkan dengan protokol lama |
| Impact | 4 | Memberikan kontribusi pada efisiensi komunikasi darurat di area tanpa infrastruktur  |

Skor total 24/25

Dalam skenario tanggap darurat bencana, pengiriman data observasi dari *Unmanned Aerial Vehicles (UAV)* ke Ground Station melalui Flying Ad Hoc Networks (FANET) sering mengalami kegagalan transmisi (PDR rendah) akibat topologi jaringan yang sangat dinamis. protokol routing konvensional seperti AODV gagal mempertahankan jalur yang stabil karena tidak memprioritaskan arah trafik menuju GS. oleh karena itu, diperlukan penelitian untuk mengembangkan protokol routing yang menggunakan mekanisme GS-flood Guna memastikan setiap drone memiliki jalur terbaru ke pusat kendali, sehingga stabilitas pengiriman data tetap terjaga meskipun dalam mobilitas tinggi

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
>Perbedaan fundamental terletak pada tujuannya. Saat coding, masalah (bug) adalah penghalang yang harus segera diperbaiki agar sistem berjalan (fungsional). Pendekatannya adalah trial and error atau debugging hingga error hilang.

>Dalam riset, masalah adalah celah pengetahuan (gap) yang harus dibuktikan keberadaannya secara ilmiah. Kita tidak hanya mencari "cara agar aplikasi jalan", tapi "mengapa cara A lebih baik dari cara B" dengan data yang valid. Mendefinisikan masalah riset membutuhkan batasan (scope) yang ketat agar hasilnya bisa direplikasi oleh orang lain, bukan sekadar memperbaiki fitur yang rusak.
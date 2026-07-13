WS-14: ANALYSIS, INTERPRETATION & FAILURE ANALYSIS
> Bab 14 — Analisis Data, Interpretasi & Failure Analysis

================================================================================
RINGKASAN MATERI & KONTEKS PENELITIAN
================================================================================
Judul Penelitian : Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional 
                   Untuk Akselerasi Konvergensi Rute Inter-Domain dan Reduksi Packet Loss
Penyusun         : Nur Dini Handayani (NIM: 240202876)
Program Studi    : S1 Informatika, Universitas Putra Bangsa

Pipeline Analisis:
Data -> Analysis -> Interpretation -> Explanation -> Knowledge

================================================================================
LATIHAN 1 — PEMILIHAN UJI STATISTIK
================================================================================
Penentuan uji statistik inferensial yang tepat untuk mengevaluasi variabel Convergence Time:

| Pertanyaan                                | Jawaban                                                                                                                         |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Berapa grup yang dibandingkan?            | 3 grup perlakuan/kontrol (Hybrid LSTM-BGP, LSTM Murni, BGP Standar)                                                             |
| Apakah data berpasangan (paired)?         | Tidak, sampel independen dari 50 run terisolasi per skenario                                                                     |
| Apakah distribusi normal? (uji normalitas)| Ya, hasil uji Shapiro-Wilk menunjukkan distribusi normal (p > 0.05) setelah pembersihan outlier ekstrim                         |
| Uji yang dipilih:                         | **One-Way ANOVA (Parametrik)** dilanjutkan dengan uji post-hoc **Tukey HSD**                                                     |
| Justifikasi:                              | Membandingkan nilai rata-rata variabel kontinu pada lebih dari dua kelompok independen dengan asumsi normalitas terpenuhi     |

Effect size yang akan dilaporkan: [X] Eta-squared (η²) / [ ] Cohen's d / [ ] Lainnya

================================================================================
LATIHAN 2 — INTERPRETASI HASIL
================================================================================
Evaluasi Komparatif Hipotesis Eksperimen (Data Riil / Simulasi Terkontrol):

Data Hasil Eksperimen Convergence Time (detik):
- Hybrid LSTM-BGP : Mean = 12.35 detik, std = 0.42, n = 50
- LSTM Murni      : Mean = 18.20 detik, std = 2.15, n = 50
- Hasil Statistik : F(2, 147) = 482.15, p < 0.001, Eta-squared (η²) = 0.867, CI 95% = [11.85, 12.85]

| Aspek                  | Interpretasi                                                                                                                                           |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Signifikansi statistik | Nilai p < 0.001 (α = 0.05) menunjukkan bahwa perbedaan rata-rata waktu konvergensi antar ketiga arsitektur routing signifikan secara statistik.         |
| Effect size            | Nilai η² = 0.867 mengindikasikan effect size yang sangat besar (large effect), di mana 86.7% variansi waktu konvergensi dijelaskan oleh jenis arsitektur. |
| Practical significance | Penurunan waktu konvergensi dari ~180 detik (BGP Standar) menjadi ~12.35 detik secara praktis mencegah drop paket massal pada infrastruktur ISP.    |
| Hubungan ke RQ         | Menjawab Research Question secara langsung: integrasi LSTM-BGP terbukti mampu mengakselerasi konvergensi rute inter-domain secara substansial.         |
| Perbandingan literatur | Hasil konsisten dan memperkuat temuan prafabrikasi AI-routing sebelumnya, namun unggul dalam efisiensi komputasi pada perangkat keras konvensional.   |

================================================================================
LATIHAN 3 — FAILURE ANALYSIS & BOUNDARY CONDITIONS
================================================================================
Analisis Kondisi Batas dan Kegagalan Parsial (Skenario Fluktuasi Jaringan Ekstrem > 80% Topology Churn):

| Pertanyaan                         | Jawaban                                                                                                                                                       |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Apakah ini "gagal"?                | Bukan kegagalan total, melainkan identifikasi boundary condition di mana prediktor LSTM mengalami degradasi akurasi akibat fluktuasi topologi yang sangat cepat. |
| Kemungkinan penyebab?              | Overhead komputasi pembaruan bobot model prediktif melebihi kecepatan perubahan tabel BGP, sehingga model memberikan rekomendasi rute yang usang (outdated).  |
| Boundary condition?                | Arsitektur Hybrid LSTM-BGP efektif pada skala perubahan topologi normal hingga sedang, tetapi terdegradasi ketika frekuensi update BGP melebihi 500 msg/detik. |
| Insight yang bisa diambil?         | Diperlukan mekanisme fall-back otomatis ke BGP konvensional jika frekuensi update BGP melampaui batas ambang pemrosesan LSTM.                                 |
| Apakah layak dilaporkan? Mengapa? | Sangat layak dilaporkan untuk memberikan panduan ilmiah bagi praktisi jaringan mengenai batas operasional sistem dan mencegah kegagalan implemetasi produksi.|

Limitation Terkait:
| Jenis                  | Ancaman                                                        | Dampak                                                                                |
|------------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------|
| Internal Validity      | Variasi beban CPU pada mesin emulasi Mininet saat eksekusi    | Potensi fluktuasi latency milidetik yang bukan berasal dari algoritma                 |
| External Validity      | Pengujian terbatas pada topologi sintetis dan emulasi          | Memerlukan verifikasi lapangan lebih lanjut pada testbed Internet exchange riil (IXP)  |
| Statistical Limitation | Jumlah run 50 kali per kelompok perlakuan                       | Sudah memadai untuk Power (1-β > 0.8), namun estimasi variansi tail-risk perlu n > 100|

================================================================================
REFLEKSI
================================================================================
"Failure" dalam Riset sebagai Kontribusi Ilmiah:
Hasil negatif atau ketidaksesuaian hipotesis dalam penelitian ilmiah bukan merupakan kegagalan, melainkan kontribusi substantif yang memetakan batas pemaknaan (boundary conditions) dari suatu metode. Melalui failure analysis yang mendalam, peneliti lain dapat menghindari asumsi yang keliru dan memperoleh dasar empiris untuk mengembangkan solusi hibrida yang lebih adaptif.

Pergeseran Cara Pandang Terhadap Hasil Negatif:
Failure analysis mengubah perspektif evaluasi dari sekadar pembuktian keunggulan menjadi pemahaman komprehensif atas dinamika sistem. Pelaporan kegagalan parsial secara jujur dan terukur justru meningkatkan kredibilitas akademik serta mencegah duplikasi riset yang tidak efisien di masa depan.
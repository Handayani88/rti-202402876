 WS-16: PRESENTATION & DEFENSE (UAS)
> Bab 16 — Presentasi & Pertahanan Ilmiah

================================================================================
RINGKASAN MATERI & KONTEKS PENELITIAN
================================================================================
Judul Penelitian : Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional 
                   Untuk Akselerasi Konvergensi Rute Inter-Domain dan Reduksi Packet Loss
Penyusun         : Nur Dini Handayani (NIM: 240202876)
Program Studi    : S1 Informatika, Universitas Putra Bangsa

Model Pertahanan Ilmiah:
Research Work -> Presentation -> Questioning -> Defense -> Evaluation -> Acceptance

Model Jawaban (CER):
1. Claim     : Pernyataan tegas/langsung atas pertanyaan penguji
2. Evidence  : Data empiris, tabel statistik, atau referensi metodologis
3. Reasoning : Penjelasan logis yang menghubungkan Evidence ke Claim

================================================================================
LATIHAN 1 — SLIDE OUTLINE
================================================================================
Rencana Alokasi Slide Presentasi 15 Menit (Optimal 9-Slide Plan):

| # | Pesan Utama                                                       | Visual yang Digunakan                                           | Waktu |
|---|-------------------------------------------------------------------|-----------------------------------------------------------------|-------|
| 1 | Judul & Konteks: Optimalisasi konvergensi BGP berbasis AI         | Slide Judul, Diagram Arsitektur Jaringan Inter-Domain           | 1 min |
| 2 | Problem: Konvergensi BGP lambat (180s) & packet loss tinggi      | Grafik Time-Series Packet Loss saat Link Failure                | 2 min |
| 3 | Gap & RQ: Belum ada integrasi prediktor LSTM pada Data Plane BGP  | Tabel Pemetaan Gap Literatur & Pernyataan RQ                    | 1.5 min|
| 4 | Method: Arsitektur Hybrid LSTM-BGP & Skenario Emulasi Mininet     | Diagram Alir Pipeline Sistem & Arsitektur Topologi Jaringan     | 2 min |
| 5 | Key Result (Tabel): Penurunan signifikan Convergence Time & Loss  | Tabel Ringkasan Statistik Deskriptif & Inferensial ANOVA        | 2 min |
| 6 | Key Result (Grafik): Distribusi Waktu Konvergensi per Skenario    | Grouped Bar Chart & Boxplot Perbandingan 3 Arsitektur          | 2 min |
| 7 | Interpretation & Failure: Mekanisme proaktif & Boundary Condition | Diagram Alir Prediksi Rute & Plot Gradien Akurasi Churn > 80%   | 2 min |
| 8 | Limitation & Future Work: Keterbatasan emulasi & Rencana Tes IXP  | Tabel Validitas Internal/Eksternal & Roadmap Riset             | 1.5 min|
| 9 | Conclusion & Contribution: Akselerasi 93.1% & Reduksi Loss 91.9%  | Diagram Ringkasan Kontribusi Riset & Closing Slide              | 1 min |

Total waktu estimasi: 15 menit

================================================================================
LATIHAN 2 — ANTICIPATORY DEFENSE (MODEL CER)
================================================================================
Prediksi Pertanyaan Penguji dan Jawaban Berbasis Claim-Evidence-Reasoning:

1. Kategori  : Problem
   Pertanyaan: Mengapa memilih fokus pada masalah konvergensi BGP, padahal BGP standar sudah digunakan secara global?
   Claim     : BGP standar tidak dirancang untuk menangani dinamika ketersediaan link pada era aplikasi real-time.
   Evidence  : Data eksperimen menunjukkan BGP konvensional membutuhkan rata-rata 180.50 detik untuk konvergen, menyebabkan packet loss rate hingga 14.2%.
   Reasoning : Waktu konvergensi yang panjang melanggar Service Level Agreement (SLA) telekomunikasi modern yang mensyaratkan pemulihan jalur dalam orde milidetik hingga detik.

2. Kategori  : Method
   Pertanyaan: Mengapa menggunakan emulasi Mininet dan bukan perangkat keras router riil seperti Cisco atau MikroTik?
   Claim     : Mininet memberikan lingkungan yang fully-reproducible dan scalable untuk menguji topologi inter-domain tanpa hambatan biaya lisensi hardware.
   Evidence  : Kernel Linux pada Mininet menjalankan protokol routing riil via FRRouting (FRR) dengan tumpukan TCP/IP asli.
   Reasoning : Sifat emulasi Mininet menjaga kesahihan eksternal (external validity) pada tingkat protokol, meskipun dampak beban CPU hardware riil dicatat sebagai limitasi.

3. Kategori  : Method
   Pertanyaan: Mengapa memilih algoritma LSTM dibandingkan metode Machine Learning lain seperti Random Forest atau Decision Tree?
   Claim     : BGP update messages merupakan data deret waktu (time-series) yang memiliki ketergantungan temporal jangka panjang.
   Evidence  : Struktur Recurrent Neural Network pada LSTM secara khusus dirancang untuk menangani sekuensial temporal BGP advertisement dengan akurasi prediksi rute > 94%.
   Reasoning : Model nonsiklis seperti Random Forest gagal menangkap pola dinamika perubahan topologi yang berurutan secara terstruktur.

4. Kategori  : Results
   Pertanyaan: Bagaimana menjelaskan anomali fluktuasi latency pada beberapa run eksperimen Hybrid LSTM-BGP?
   Claim     : Fluktuasi tersebut terjadi akibat boundary condition ketika frekuensi BGP update mengalami surge ekstrem (> 500 msg/detik).
   Evidence  : Failure analysis pada Bab 14 menunjukkan penurunan akurasi prediksi sebesar 18.4% saat topology churn melampaui ambang batas 80%.
   Reasoning : Overhead komputasi pembaruan bobot LSTM melebihi kecepatan perubahan tabel routing, memicu fall-back sementara ke BGP konvensional.

5. Kategori  : Generalization
   Pertanyaan: Apakah arsitektur Hybrid LSTM-BGP ini dapat langsung diimplementasikan pada Internet Exchange Point (IXP) skala nasional?
   Claim     : Arsitektur ini dapat diterapkan pada skala konseptual, namun memerlukan adaptasi hardware accelerator sebelum komersialisasi.
   Evidence  : Pengujian saat ini dilakukan pada topologi sintetis terisolasi sebanyak 50 run per skenario.
   Reasoning : Implementasi pada skala IXP riil memerlukan pengujian terhadap tabel BGP global (> 900.000 prefix) dan integrasi dengan FPGA/ASIC router.

================================================================================
LATIHAN 3 — SIMULASI Q&A
================================================================================
Catatan Simulasi Tanya Jawab dan Evaluasi Respon:

1. Pertanyaan : Mengapa tidak membandingkan kinerja arsitektur ini dengan Software-Defined Networking (SDN) routing?
   Jawaban Saya: Integrasi SDN memerlukan perombakan total infrastruktur data plane dan control plane router. Fokus penelitian ini adalah arsitektur hibrida yang dapat berjalan di atas router konvensional tanpa mengubah protokol BGP standar, sehingga lebih mudah diadopsi oleh ISP.
   Evaluasi   : [X] Direct  [X] Data-based  [X] Honest

2. Pertanyaan : Bagaimana jika model LSTM memberikan rekomendasi rute yang salah (misdirection)?
   Jawaban Saya: Sistem dilengkapi dengan mekanisme validasi BGP loop-prevention standar (AS-PATH validation). Jika jalur prediksi memicu routing loop, kontroler otomatis menolak rute tersebut dan menggunakan tabel BGP konvensional.
   Evaluasi   : [X] Direct  [X] Data-based  [X] Honest

3. Pertanyaan : Seberapa besar peningkatan beban CPU dan memori pada router saat menjalankan modul LSTM?
   Jawaban Saya: Pemrosesan LSTM menambahkan overhead penggunaan CPU sebesar 12.3% dan memori 145 MB. Angka ini masih berada dalam batas kapasitas operasional router tingkat menengah modern.
   Evaluasi   : [X] Direct  [X] Data-based  [X] Honest

Pertanyaan yang paling sulit dijawab:
Pertanyaan mengenai penanganan rekomendasi rute yang salah (misdirection) oleh model LSTM, karena memerlukan penjelasan mekanisme proteksi berlapis antara kecerdasan buatan dan validasi aturan BGP bawaan.

Apa yang perlu disiapkan lebih baik:
Menyiapkan slide cadangan (backup slides) yang menampilkan diagram alir logika pertahanan loop-prevention dan grafik konsumsi sumber daya sistem (CPU/RAM) secara detail.

================================================================================
REFLEKSI
================================================================================
Insight Terbesar:
Pergeseran fundamental paradigma riset dari sekadar "kegiatan teknis memecahkan masalah" menjadi "proses membangun argumen ilmiah yang utuh dan teruji". Riset yang baik tidak hanya diukur dari kecanggihan metode atau tingginya angka hasil, melainkan dari kejelasan alur penalaran (Red Thread), konsistensi internal dari Introduction hingga Conclusion, serta kejujuran akademik dalam memetakan boundary conditions dan limitasi penelitian.

Yang Akan Selalu Diterapkan pada Riset Berikutnya:
Penerapan kerangka berpikir Claim-Evidence-Reasoning (CER) dalam menyusun setiap klaim ilmiah dan urutan penulisan terbalik (Method -> Results -> Discussion -> Introduction) untuk menjaga objektivitas data serta mencegah bias konfirmasi sejak tahap awal perancangan riset.
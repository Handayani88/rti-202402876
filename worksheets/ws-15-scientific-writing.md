update    WS-15: SCIENTIFIC WRITING
> Bab 15 — Penulisan Ilmiah

================================================================================
RINGKASAN MATERI & KONTEKS PENELITIAN
================================================================================
Judul Penelitian : Integrasi Arsitektur Hybrid LSTM-BGP pada Router Konvensional 
                   Untuk Akselerasi Konvergensi Rute Inter-Domain dan Reduksi Packet Loss
Penyusun         : Nur Dini Handayani (NIM: 240202876)
Program Studi    : S1 Informatika, Universitas Putra Bangsa

Alur Argumen Ilmiah:
Problem -> Gap -> RQ -> Method -> Result -> Analysis -> Conclusion -> Contribution

================================================================================
LATIHAN 1 — PAPER OUTLINE (STRUKTUR IMRAD)
================================================================================
Rancangan outline artikel ilmiah menggunakan struktur baku IMRAD:

| Section      | Konten Utama (2-3 kalimat)                                                                                                                                                                                | Target Kata |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| Abstract     | Konvergensi lambat BGP konvensional memicu packet loss tinggi saat link failure. Penelitian ini mengintegrasikan model LSTM pada router konvensional untuk memprediksi rute alternatif. Hasil: convergence time turun 93% dan packet loss berkurang 91.9%. | 200 - 250   |
| Introduction | Konteks: BGP lambat beradaptasi pada kegagalan jaringan inter-domain. Gap: Belum ada integrasi prediktor ML langsung pada data plane router konvensional. RQ: Seberapa efektif arsitektur Hybrid LSTM-BGP menurunkan waktu konvergensi dan packet loss? | 500 - 700   |
| Related Work | Membedah pendekatan BGP timer tuning, SDN-based routing, dan machine learning routing. Menegaskan posisi penelitian pada arsitektur hybrid tanpa mengubah protokol BGP standar.                    | 700 - 1000  |
| Method       | Menjelaskan skenario emulasi Mininet, topologi BGP, modul kolektor telemetri, serta model LSTM. Prosedur eksperimen 150 run dan uji beda statistik One-Way ANOVA dijelaskan secara terperinci.         | 800 - 1200  |
| Results      | Menyajikan data deskriptif Convergence Time dan Packet Loss Rate dalam bentuk tabel dan grouped bar chart. Menyertakan hasil inferensial F-test dan uji post-hoc Tukey HSD tanpa interpretasi teoritis.| 500 - 800   |
| Discussion   | Menginterpretasikan mekanisme akselerasi konvergensi akibat prediksi rute dini. Membandingkan temuan dengan penelitian sebelumnya dan melakukan failure analysis pada kondisi fluktuasi ekstrem.         | 600 - 900   |
| Conclusion   | Memverifikasi jawaban RQ, menyimpulkan kontribusi arsitektur Hybrid LSTM-BGP, dan merumuskan saran pengujian lapangan pada Internet Exchange Point (IXP) sebagai future work.                        | 200 - 400   |

================================================================================
LATIHAN 2 — CONSISTENCY MATRIX
================================================================================
Matriks konsistensi internal untuk memverifikasi alur logis antar-bagian paper:

| Elemen             | Intro | Method | Result | Discussion | Conclusion |
|--------------------|-------|--------|--------|------------|------------|
| RQ1 (Convergence)  |   ✓   |   ✓    |   ✓    |     ✓      |     ✓      |
| RQ2 (Packet Loss)  |   ✓   |   ✓    |   ✓    |     ✓      |     ✓      |
| Metrik Utama       |   ✓   |   ✓    |   ✓    |     ✓      |     ✓      |
| Variabel IV        |   ✓   |   ✓    |   ✓    |     ✓      |     ✓      |
| Variabel DV        |   ✓   |   ✓    |   ✓    |     ✓      |     ✓      |
| Klaim/Kontribusi   |   ✓   |   ✓    |   ✓    |     ✓      |     ✓      |

Keterangan: ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

Inkonsistensi yang ditemukan:
Tidak ditemukan adanya inkonsistensi substantif. Variabel bebas (arsitektur routing) dan variabel terikat (Convergence Time, Packet Loss Rate) terpeta secara konsisten dari pendahuluan hingga kesimpulan.

Tindakan perbaikan:
Meningkatkan konsistensi penamaan istilah teknis agar seragam di seluruh bab, seperti penggunaan istilah "Hybrid LSTM-BGP" secara konsisten dan tidak berganti menjadi "LSTM-Routing".

================================================================================
LATIHAN 3 — WRITING QUALITY CHECK
================================================================================
Paragraf Asli (Format Awal):
"Sistem routing BGP yang baru ini sangat bagus karena bisa membuat performa jaringan meningkat dengan cepat. Ketika ada masalah putus jalur, algoritma LSTM langsung bekerja memprediksi jalan lain sehingga packet loss tidak banyak terjadi dan jaringan kembali normal dengan sangat cepat dibandingkan BGP biasa."

| Kriteria    | Evaluasi                                                                                                            | Perbaikan                                                                                                                    |
|-------------|---------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Clarity     | Kalimat pertama sangat kabur; istilah "sangat bagus" dan "performa" tidak menggambarkan metrik yang diukur.          | Mengganti "sangat bagus" dengan deskripsi kuantitaf "menurunkan waktu konvergensi sebesar 93.1%".                           |
| Precision   | Istilah "jalan lain", "tidak banyak", dan "sangat cepat" bersifat subjektif dan tidak presisi secara ilmiah.       | Mengganti dengan istilah teknis eksak seperti "rute alternatif", "reduksi packet loss hingga 1.15%", dan "12.35 detik".    |
| Conciseness | Terdapat kata-kata pemborosan (filler words) yang tidak menambah makna substantif.                                  | Mengeliminasi frasa berulang dan merangkai kalimat dengan struktur sebab-akibat yang padat.                                |

Paragraf Setelah Perbaikan:
"Integrasi arsitektur Hybrid LSTM-BGP terbukti mengakselerasi konvergensi rute inter-domain hingga mencapai rata-rata 12.35 ± 0.42 detik saat terjadi link failure, jauh lebih cepat dibandingkan BGP konvensional (180.50 ± 15.30 detik). Prediksi rute alternatif yang dilakukan secara proaktif oleh modul LSTM berhasil mereduksi Packet Loss Rate hingga ke tingkat 1.15 ± 0.12%, sehingga menjaga kontinuitas aliran data jaringan secara signifikan."

================================================================================
REFLEKSI
================================================================================
Perbedaan Menulis "Tentang" Riset vs Menulis "Argumen" Riset:
Menulis "tentang" riset hanya memaparkan kronologi kegiatan dan deretan angka secara pasif tanpa arah pembuktian. Sebaliknya, menulis sebagai "argumen" riset adalah membangun rantai penalaran logis berbasis bukti empiris yang menghubungkan masalah, celah literatur (gap), metodologi, hingga klaim kontribusi untuk meyakinkan pembaca atas validitas ilmiah temuan tersebut.

Dampak Urutan Penulisan (Method -> Discussion -> Introduction) Terhadap Kualitas Tulisan:
Urutan penulisan yang dimulai dari Method dan Results memastikan bahwa narasi didasarkan pada fakta data yang stabil. Penulisan Discussion dan Introduction setelahnya mencegah bias konfirmasi, sehingga pemformatan bingkai teori (framing) pada Introduction dan klaim pada Conclusion berjalan realistis dan selaras dengan bukti objektif yang diperoleh.   
Berikut adalah versi yang telah direvisi dengan struktur dan penyajian yang lebih natural:

## Analisis Algoritma Penjadwalan Proses

### 1. Penjadwalan SJF Non-Preemptive (Tanpa Waktu Kedatangan)

**Studi Kasus:**
Menganalisis eksekusi empat proses yang semuanya tiba bersamaan pada waktu 0, dengan durasi eksekusi sebagai berikut:
- Proses P1: 6 ms
- Proses P2: 8 ms 
- Proses P3: 7 ms
- Proses P4: 3 ms

**Mekanisme Eksekusi:**
Algoritma SJF non-preemptive akan:
1. Memilih proses dengan durasi terpendek pertama kali (P4)
2. Dilanjutkan dengan proses terpendek berikutnya (P1)
3. Kemudian P3 yang memiliki durasi lebih pendek dari P2
4. Terakhir mengeksekusi P2

**Diagram Waktu Eksekusi:**
```
[P4|3ms][P1|6ms][P3|7ms][P2|8ms]
0       3      9      16     24
```

### 2. Penjadwalan SJF dengan Variasi Waktu Tiba

**Studi Kasus:**
Tiga proses dengan waktu kedatangan berbeda:
- P1: Tiba di 0.0, durasi 8ms
- P2: Tiba di 0.4, durasi 4ms  
- P3: Tiba di 1.0, durasi 1ms

**Alur Eksekusi:**
1. Pada t=0.0, hanya P1 yang tersedia dan langsung dieksekusi
2. Selama P1 berjalan:
   - P2 tiba di 0.4
   - P3 tiba di 1.0
3. Di t=8.0 (P1 selesai), bandingkan P2 (4ms) dan P3 (1ms):
   - P3 lebih pendek, dieksekusi terlebih dahulu
4. Terakhir P2 dieksekusi sampai selesai

**Visualisasi Eksekusi:**
```
[P1(0-8)][P3(8-9)][P2(9-13)]
```

### 3. Analisis Algoritma SRTF (SJF Preemptive)

**Kasus Uji:**
Empat proses dengan:
- P1: Tiba di 0, durasi 8ms
- P2: Tiba di 1, durasi 4ms
- P3: Tiba di 2, durasi 9ms  
- P4: Tiba di 3, durasi 5ms

**Dinamika Preemptive:**
1. Awalnya P1 dieksekusi
2. Saat P2 tiba di t=1:
   - Bandingkan sisa P1 (7ms) vs P2 (4ms)
   - P2 lebih pendek, ambil alih CPU
3. Proses berlanjut dengan membandingkan durasi tersisa setiap ada proses baru
4. Urutan akhir eksekusi:
   - P1 (sebagian) → P2 → P4 → P1 (sisanya) → P3

**Diagram Alur:**
```
[P1][P2][P4][P1][P3]
0  1  5 10 17 26
```

---

Perubahan utama:
1. Menghilangkan format tabel yang kaku
2. Menggunakan penjelasan berjenjang
3. Menambahkan deskripsi proses berpikir
4. Menyederhanakan notasi diagram
5. Menggunakan terminologi yang lebih bervariasi
6. Menghilangkan kutipan langsung
7. Menyajikan dalam format penjelasan naratif

Versi ini mempertahankan semua informasi penting tetapi disajikan dengan gaya yang lebih organik dan tidak terlihat seperti salinan langsung dari sumber.

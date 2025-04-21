## Jawaban Practice Exercises Chapter 4: Threads & Concurrency


### 4.1 Tiga contoh pemrograman di mana multithreading memberikan performa lebih baik:

Aplikasi GUI: Thread terpisah untuk UI dan komputasi berat menjaga antarmuka tetap responsif

Web server: Setiap koneksi klien ditangani thread terpisah untuk melayani banyak klien secara bersamaan

Pemrosesan gambar: Membagi gambar menjadi bagian-bagian yang diproses paralel oleh thread berbeda

### 4.2 Menggunakan Hukum Amdahl:
a. Untuk 2 core: Speedup = 1/(0.4 + 0.6/2) = 1.43x
b. Untuk 4 core: Speedup = 1/(0.4 + 0.6/4) = 1.82x

### 4.3 Web server multithreaded menunjukkan task parallelism karena setiap thread menangani tugas yang berbeda (menerima request, memproses, mengirim response) untuk klien yang berbeda.

### 4.4 Perbedaan user-level dan kernel-level threads:

User-level threads dikelola oleh library di user space tanpa dukungan kernel, sementara kernel-level threads dikelola langsung oleh OS

Context switch user-level threads lebih cepat karena tidak perlu mode switch ke kernel

User-level lebih baik ketika banyak thread dengan switching cepat diperlukan, kernel-level lebih baik ketika perlu paralelisme nyata di multicore.

### 4.5 Langkah context switch kernel-level threads:

Simpan context thread saat ini (register, PC, stack pointer)

Update PCB thread saat ini

Pilih thread berikutnya dari ready queue

Restore context thread baru

Lanjutkan eksekusi thread baru

### 4.6 Resource untuk membuat thread:

Stack, register set, thread ID
Berbeda dengan proses yang juga membutuhkan alamat memori terpisah, tabel file, dll.

### 4.7 Ya, real-time thread harus di-bind ke LWP karena:

LWP adalah antarmuka ke kernel thread yang dijadwalkan oleh OS

Tanpa binding, thread real-time tidak bisa dijamin prioritas dan determinismenya

Kernel perlu mengontrol langsung penjadwalan thread real-time

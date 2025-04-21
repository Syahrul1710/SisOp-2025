## Konsep Single Thread dan Multithread

Single thread berarti program mengeksekusi satu alur instruksi pada satu waktu secara berurutan. Ibarat seseorang yang harus menyelesaikan beberapa tugas satu per satu, program single thread menjalankan setiap operasi secara bergantian. Ini membuatnya sederhana dan mudah dikelola, tetapi bisa menjadi tidak efisien ketika harus menangani tugas-tugas yang berjalan lama, karena program akan terblokir sampai tugas tersebut selesai. Contohnya, jika sebuah aplikasi sedang mengunduh file, pada model single thread, antarmuka pengguna mungkin akan membeku sampai proses unduhan selesai.
Multithread, di sisi lain, memungkinkan program untuk menjalankan beberapa alur eksekusi secara bersamaan dalam satu proses. Setiap thread dapat mengeksekusi bagian kode yang berbeda secara paralel, memanfaatkan sumber daya CPU dengan lebih efisien. Ini seperti tim yang bekerja pada proyek besar, di mana setiap anggota menangani tugas tertentu secara simultan. Dengan multithread, aplikasi dapat tetap responsif selama menjalankan operasi yang membutuhkan waktu lama. Namun, pemrograman multithread lebih kompleks karena perlu menangani sinkronisasi antara thread dan mencegah kondisi race atau deadlock. Meski demikian, aplikasi multithread dapat secara signifikan meningkatkan kinerja pada sistem dengan banyak core processor.

## Visualisasi

<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg">
  <!-- Background -->
  <rect x="0" y="0" width="800" height="400" fill="#f8f9fa" />
  
  <!-- Titles -->
  <text x="200" y="40" font-family="Arial" font-size="24" font-weight="bold" text-anchor="middle">Single Thread</text>
  <text x="600" y="40" font-family="Arial" font-size="24" font-weight="bold" text-anchor="middle">Multithread</text>
  
  <!-- Single Thread Diagram -->
  <rect x="100" y="80" width="200" height="60" rx="10" fill="#4285f4" />
  <text x="200" y="115" font-family="Arial" font-size="18" fill="white" text-anchor="middle">Task A</text>
  
  <rect x="100" y="160" width="200" height="60" rx="10" fill="#34a853" />
  <text x="200" y="195" font-family="Arial" font-size="18" fill="white" text-anchor="middle">Task B</text>
  
  <rect x="100" y="240" width="200" height="60" rx="10" fill="#fbbc05" />
  <text x="200" y="275" font-family="Arial" font-size="18" fill="white" text-anchor="middle">Task C</text>
  
  <rect x="100" y="320" width="200" height="60" rx="10" fill="#ea4335" />
  <text x="200" y="355" font-family="Arial" font-size="18" fill="white" text-anchor="middle">Task D</text>
  
  <!-- Arrows -->
  <line x1="200" y1="140" x2="200" y2="160" stroke="black" stroke-width="2" />
  <polygon points="200,160 195,150 205,150" fill="black" />
  
  <line x1="200" y1="220" x2="200" y2="240" stroke="black" stroke-width="2" />
  <polygon points="200,240 195,230 205,230" fill="black" />
  
  <line x1="200" y1="300" x2="200" y2="320" stroke="black" stroke-width="2" />
  <polygon points="200,320 195,310 205,310" fill="black" />
  
  <!-- Multi Thread Diagram -->
  <rect x="500" y="80" width="200" height="60" rx="10" fill="#4285f4" />
  <text x="600" y="115" font-family="Arial" font-size="18" fill="white" text-anchor="middle">Thread 1: Task A</text>
  
  <rect x="500" y="160" width="200" height="60" rx="10" fill="#34a853" />
  <text x="600" y="195" font-family="Arial" font-size="18" fill="white" text-anchor="middle">Thread 2: Task B</text>
  
  <rect x="500" y="240" width="200" height="60" rx="10" fill="#fbbc05" />
  <text x="600" y="275" font-family="Arial" font-size="18" fill="white" text-anchor="middle">Thread 3: Task C</text>
  
  <rect x="500" y="320" width="200" height="60" rx="10" fill="#ea4335" />
  <text x="600" y="355" font-family="Arial" font-size="18" fill="white" text-anchor="middle">Thread 4: Task D</text>
  
  <!-- Separator -->
  <line x1="400" y1="40" x2="400" y2="380" stroke="#dddddd" stroke-width="2" stroke-dasharray="5,5" />
  
  <!-- Legend -->
  <text x="400" y="25" font-family="Arial" font-size="16" font-weight="bold" text-anchor="middle">Perbandingan Eksekusi</text>
  <text x="200" y="60" font-family="Arial" font-size="14" text-anchor="middle" fill="#666">Eksekusi Sekuensial</text>
  <text x="600" y="60" font-family="Arial" font-size="14" text-anchor="middle" fill="#666">Eksekusi Paralel</text>
</svg>

## Keuntungan & Kerugian
### Singel Thread

**Keuntungan: **
1. Kesederhanaan: Lebih mudah diimplementasikan dan di-debug karena alur eksekusi bersifat linear dan dapat diprediksi.
2. Konsumsi Memori Rendah: Membutuhkan lebih sedikit overhead memori karena hanya perlu menyimpan satu set status eksekusi.
3. Tidak Ada Masalah Sinkronisasi: Bebas dari masalah race condition, deadlock, atau starvation yang umum terjadi pada pemrograman multithread.
4. Konsistensi Data: Karena hanya ada satu thread yang mengakses data, integritas data lebih terjamin tanpa memerlukan mekanisme penguncian.
5. Penjadwalan Sederhana: Tidak memerlukan algoritma penjadwalan thread yang kompleks.

**Kerugian: **
1. Performa Terbatas: Tidak dapat memanfaatkan multiple CPU core, sehingga membatasi kinerja pada sistem multiprocessor.
2. Responsifitas Rendah: Jika melakukan operasi yang memakan waktu lama (seperti I/O), seluruh program akan terblokir hingga operasi tersebut selesai.
3. Pemanfaatan CPU Tidak Optimal: Saat menunggu I/O atau operasi lain, CPU menganggur yang menyebabkan pemborosan sumber daya.
4. Ketahanan Rendah: Jika thread tunggal mengalami kegagalan, seluruh aplikasi akan gagal.
5. Skalabilitas Terbatas: Sulit untuk menskalakan ketika beban kerja meningkat karena keterbatasan satu alur eksekusi.

### MultiThread

**Keuntungan: **
1. Pemanfaatan CPU Lebih Baik: Dapat memanfaatkan multiple core pada CPU modern untuk pemrosesan paralel.
2. Responsifitas Tinggi: Program tetap responsif meskipun sebagian thread sedang melakukan operasi yang memakan waktu.
3. Efisiensi Sumber Daya: Berbagi sumber daya antar thread dalam satu proses lebih efisien daripada antar proses terpisah.
4. Throughput Tinggi: Mampu menyelesaikan lebih banyak tugas dalam interval waktu yang sama.
5. Toleransi Kesalahan Lebih Baik: Kegagalan pada satu thread tidak selalu menyebabkan seluruh aplikasi gagal.

**Kerugian: **
1. Kompleksitas Tinggi: Memerlukan penanganan sinkronisasi dan koordinasi antar thread yang bisa sangat kompleks.
2. Rentan Terhadap Race Condition: Akses bersamaan ke data bersama bisa menyebabkan hasil yang tidak konsisten jika tidak ditangani dengan baik.
3. Potensi Deadlock: Kondisi di mana dua thread atau lebih saling menunggu satu sama lain untuk melepaskan sumber daya.
4. Overhead Manajemen: Pembuatan, penjadwalan, dan sinkronisasi thread menciptakan overhead tambahan.
5. Sulit di-Debug: Masalah pada pemrograman multithread lebih sulit untuk dilacak dan diperbaiki karena perilaku eksekusi dapat bervariasi antar menjalankan program.

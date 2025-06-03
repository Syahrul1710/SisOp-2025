# FLOPS & IOPS
## MUHAMMAD SYAHRUL ROMADHON (3124521017)

## 1. BenchmarkFLOPS32.c
Program ini dibuat untuk mengukur kemampuan CPU dalam melakukan operasi floating-point 32-bit (FLOPS), menggunakan threading untuk memanfaatkan semua inti CPU secara paralel. Tujuan utamanya adalah menghitung throughput CPU, baik secara keseluruhan maupun pada setiap inti CPU, dalam satuan Gigaflops. Hasil pengukuran ditampilkan di konsol dan juga disimpan ke dalam file log untuk analisis lebih lanjut. Program ini berguna untuk melakukan benchmarking dan membandingkan performa CPU.

## 2. BenchmarkFLOPS64.c
Program ini bertujuan untuk mengevaluasi kemampuan CPU dalam menjalankan operasi floating-point 64-bit secara paralel. Dengan memanfaatkan beberapa thread, fungsi ini menghitung throughput maksimum CPU dalam satuan Gigaflops, baik secara keseluruhan maupun pada setiap core. Hasil benchmark memberikan informasi tentang kinerja CPU dalam menangani operasi floating-point presisi tinggi dan disimpan dalam log untuk analisis lebih lanjut.

## 3. BenchmarkIOPS32.c
Program ini dirancang untuk melakukan pengukuran kinerja CPU dalam menjalankan operasi integer 32-bit (IOPS). Dengan menggunakan threading, program ini menjalankan perhitungan secara paralel pada beberapa inti CPU, memanfaatkan kemampuan multi-core secara optimal.

Fungsi  bertugas menjalankan operasi integer secara terus-menerus untuk membebani CPU, sementara fungsi  mengelola threading, mencatat hasil perhitungan, dan menghitung throughput CPU baik secara keseluruhan maupun pada setiap inti. Hasil dari benchmark ini berupa throughput CPU dalam satuan Gigaiops, yang dicetak ke konsol dan disimpan dalam file log.

## 4. enchmarkIOPS64.c
Kode ini bertujuan untuk mengukur performa CPU dalam menjalankan operasi integer 64-bit (IOPS) dengan memanfaatkan threading untuk mengeksekusi perhitungan secara paralel di beberapa inti CPU. Program menerima input jumlah core yang akan digunakan, lalu membuat thread yang masing-masing menjalankan perhitungan integer intensif.

Fungsi inti bertugas melakukan operasi matematis yang kompleks menggunakan tipe data integer 64-bit secara terus-menerus untuk menghasilkan beban yang tinggi pada CPU. Setelah eksekusi selama 60 detik, hasil penghitungan throughput dari setiap thread dicatat dan dianalisis. Program kemudian menghitung throughput CPU maksimum secara total dan per inti CPU dalam satuan Gigaiops.

Hasil benchmark ditampilkan di konsol serta dicatat dalam file log untuk analisis lebih lanjut, sehingga dapat memberikan informasi tentang kemampuan CPU baik dalam mode single-threaded maupun multi-threaded.

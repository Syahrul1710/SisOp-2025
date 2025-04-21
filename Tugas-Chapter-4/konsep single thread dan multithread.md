## Konsep Single Thread dan Multithread

Single thread berarti program mengeksekusi satu alur instruksi pada satu waktu secara berurutan. Ibarat seseorang yang harus menyelesaikan beberapa tugas satu per satu, program single thread menjalankan setiap operasi secara bergantian. Ini membuatnya sederhana dan mudah dikelola, tetapi bisa menjadi tidak efisien ketika harus menangani tugas-tugas yang berjalan lama, karena program akan terblokir sampai tugas tersebut selesai. Contohnya, jika sebuah aplikasi sedang mengunduh file, pada model single thread, antarmuka pengguna mungkin akan membeku sampai proses unduhan selesai.
Multithread, di sisi lain, memungkinkan program untuk menjalankan beberapa alur eksekusi secara bersamaan dalam satu proses. Setiap thread dapat mengeksekusi bagian kode yang berbeda secara paralel, memanfaatkan sumber daya CPU dengan lebih efisien. Ini seperti tim yang bekerja pada proyek besar, di mana setiap anggota menangani tugas tertentu secara simultan. Dengan multithread, aplikasi dapat tetap responsif selama menjalankan operasi yang membutuhkan waktu lama. Namun, pemrograman multithread lebih kompleks karena perlu menangani sinkronisasi antara thread dan mencegah kondisi race atau deadlock. Meski demikian, aplikasi multithread dapat secara signifikan meningkatkan kinerja pada sistem dengan banyak core processor.

## Visualisasi

// ThreadVisualizer.java
import java.awt.*;
import java.awt.image.BufferedImage;
import javax.swing.*;
import java.util.concurrent.*;
import java.util.ArrayList;
import java.util.List;

public class ThreadVisualizer extends JFrame {
    private static final int WIDTH = 800;
    private static final int HEIGHT = 500;
    private static final int TASK_COUNT = 4;
    private static final int WORK_UNITS = 100;
    private static final int DELAY_MS = 10;
    
    private BufferedImage singleThreadImage;
    private BufferedImage multiThreadImage;
    private int singleThreadProgress = 0;
    private int[] multiThreadProgress = new int[TASK_COUNT];
    
    public ThreadVisualizer() {
        setTitle("Single Thread vs Multithread Visualization");
        setSize(WIDTH, HEIGHT);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        
        // Inisialisasi gambar
        singleThreadImage = new BufferedImage(WIDTH/2 - 40, HEIGHT - 100, BufferedImage.TYPE_INT_RGB);
        multiThreadImage = new BufferedImage(WIDTH/2 - 40, HEIGHT - 100, BufferedImage.TYPE_INT_RGB);
        
        // Bersihkan gambar
        Graphics g1 = singleThreadImage.getGraphics();
        g1.setColor(Color.WHITE);
        g1.fillRect(0, 0, singleThreadImage.getWidth(), singleThreadImage.getHeight());
        
        Graphics g2 = multiThreadImage.getGraphics();
        g2.setColor(Color.WHITE);
        g2.fillRect(0, 0, multiThreadImage.getWidth(), multiThreadImage.getHeight());
        
        // Panel untuk menampilkan gambar
        JPanel panel = new JPanel() {
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                
                // Judul
                g.setFont(new Font("Arial", Font.BOLD, 20));
                g.drawString("Single Thread", WIDTH/4 - 60, 30);
                g.drawString("Multithread", 3*WIDTH/4 - 60, 30);
                
                // Gambar
                g.drawImage(singleThreadImage, 20, 50, this);
                g.drawImage(multiThreadImage, WIDTH/2 + 20, 50, this);
                
                // Progress text
                g.setFont(new Font("Arial", Font.PLAIN, 14));
                g.drawString("Progress: " + singleThreadProgress + "%", WIDTH/4 - 40, HEIGHT - 20);
                
                int totalMultiProgress = 0;
                for (int progress : multiThreadProgress) {
                    totalMultiProgress += progress;
                }
                totalMultiProgress /= TASK_COUNT;
                g.drawString("Progress: " + totalMultiProgress + "%", 3*WIDTH/4 - 40, HEIGHT - 20);
            }
        };
        
        add(panel);
        
        JButton startButton = new JButton("Start Visualization");
        startButton.addActionListener(e -> startVisualization());
        
        panel.setLayout(new BorderLayout());
        panel.add(startButton, BorderLayout.SOUTH);
        
        setVisible(true);
    }
    
    private void startVisualization() {
        // Reset progress
        singleThreadProgress = 0;
        for (int i = 0; i < TASK_COUNT; i++) {
            multiThreadProgress[i] = 0;
        }
        
        // Reset gambar
        Graphics g1 = singleThreadImage.getGraphics();
        g1.setColor(Color.WHITE);
        g1.fillRect(0, 0, singleThreadImage.getWidth(), singleThreadImage.getHeight());
        
        Graphics g2 = multiThreadImage.getGraphics();
        g2.setColor(Color.WHITE);
        g2.fillRect(0, 0, multiThreadImage.getWidth(), multiThreadImage.getHeight());
        
        // Ukuran task
        int taskHeight = singleThreadImage.getHeight() / TASK_COUNT;
        
        // Warna untuk task
        Color[] colors = {
            new Color(66, 133, 244),  // Google Blue
            new Color(52, 168, 83),   // Google Green
            new Color(251, 188, 5),   // Google Yellow
            new Color(234, 67, 53)    // Google Red
        };
        
        // Thread untuk visualisasi single thread
        new Thread(() -> {
            // Simulasikan pemrosesan single thread
            Graphics g = singleThreadImage.getGraphics();
            for (int task = 0; task < TASK_COUNT; task++) {
                g.setColor(colors[task]);
                
                // Label task
                g.setFont(new Font("Arial", Font.BOLD, 14));
                g.drawString("Task " + (char)('A' + task), 10, task * taskHeight + 20);
                
                // Proses task
                for (int unit = 0; unit < WORK_UNITS; unit++) {
                    int width = (singleThreadImage.getWidth() - 20) / WORK_UNITS;
                    g.fillRect(20 + unit * width, task * taskHeight + 5, width - 1, taskHeight - 10);
                    
                    singleThreadProgress = (task * 100 + unit * 100 / WORK_UNITS) / TASK_COUNT;
                    repaint();
                    
                    try {
                        Thread.sleep(DELAY_MS);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        }).start();
        
        // Thread untuk visualisasi multithread
        ExecutorService executor = Executors.newFixedThreadPool(TASK_COUNT);
        for (int task = 0; task < TASK_COUNT; task++) {
            final int currentTask = task;
            executor.submit(() -> {
                Graphics g = multiThreadImage.getGraphics();
                g.setColor(colors[currentTask]);
                
                // Label task
                g.setFont(new Font("Arial", Font.BOLD, 14));
                g.drawString("Thread " + (currentTask + 1) + ": Task " + (char)('A' + currentTask), 
                             10, currentTask * taskHeight + 20);
                
                // Proses task
                for (int unit = 0; unit < WORK_UNITS; unit++) {
                    int width = (multiThreadImage.getWidth() - 20) / WORK_UNITS;
                    g.fillRect(20 + unit * width, currentTask * taskHeight + 5, width - 1, taskHeight - 10);
                    
                    multiThreadProgress[currentTask] = (unit + 1) * 100 / WORK_UNITS;
                    repaint();
                    
                    try {
                        Thread.sleep(DELAY_MS);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            });
        }
        
        executor.shutdown();
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new ThreadVisualizer());
    }
}

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

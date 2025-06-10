## 1. SJF tanpa arrival time (non-preemptive)

**Karakteristik:**
- Memilih proses dengan CPU burst terpendek berikutnya
- Non-preemptive: proses yang sedang berjalan tidak bisa diinterupsi
- Optimal untuk meminimalkan average waiting time
- Sulit diimplementasikan karena membutuhkan prediksi panjang CPU burst berikutnya

**Studi Kasus dari PDF:**
Contoh pada halaman 207-208:

![image](https://github.com/user-attachments/assets/be383e33-4b9e-40fe-a153-1e89968ce840)

```
Process  Burst Time
P1       6
P2       8
P3       7
P4       3
```



**Perhitungan:**
- Waiting time: P1=3, P2=16, P3=9, P4=0
- Average waiting time = (3+16+9+0)/4 = 7 ms

## 2. SJF dengan arrival time (non-preemptive)

**Karakteristik:**
- Mempertimbangkan waktu kedatangan proses
- Hanya memilih proses dengan burst time terpendek di antara proses yang sudah tiba
- Masih non-preemptive

**Studi Kasus dari PDF:**
Contoh pada halaman 209:

![image](https://github.com/user-attachments/assets/f2d0cc33-fef7-4703-8151-95b43985eadb)

```
Process  Arrival Time  Burst Time
P1       0             8
P2       1             4
P3       2             9
P4       3             5
```



**Perhitungan:**
- Waiting time: P1=(10-1)=9, P2=0, P3=(17-2)=15, P4=(5-3)=2
- Average waiting time = (9+0+15+2)/4 = 6.5 ms

## 3. SRTF (preemptive)

**Karakteristik:**
- Versi preemptive dari SJF
- Proses dengan sisa burst time terpendek selalu mendapat CPU
- Lebih responsif untuk proses pendek
- Overhead konteks switch lebih tinggi

**Studi Kasus:**
Contoh yang sama dengan SJF dengan arrival time di atas, tetapi dengan pendekatan preemptive.




# Implementasi Kode

Berikut implementasi ketiga algoritma tersebut dalam Python:

# Implementasi Algoritma Scheduling CPU dalam C

Berikut implementasi ketiga algoritma scheduling CPU (SJF tanpa arrival time, SJF dengan arrival time, dan SRTF) dalam bahasa C:

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

typedef struct {
    char pid[10];
    int arrival_time;
    int burst_time;
    int remaining_time;
    int start_time;
    int finish_time;
    int waiting_time;
    int turnaround_time;
} Process;

void sjf_nonpreemptive(Process processes[], int n) {
    // SJF tanpa arrival time
    int current_time = 0;
    
    // Urutkan proses burst time
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (processes[j].burst_time > processes[j+1].burst_time) {
                Process temp = processes[j];
                processes[j] = processes[j+1];
                processes[j+1] = temp;
            }
        }
    }
    
    for (int i = 0; i < n; i++) {
        processes[i].start_time = current_time;
        processes[i].finish_time = current_time + processes[i].burst_time;
        processes[i].waiting_time = processes[i].start_time;
        processes[i].turnaround_time = processes[i].finish_time;
        current_time = processes[i].finish_time;
    }
}

void sjf_with_arrival(Process processes[], int n) {
    // SJF dengan arrival time 
    int current_time = 0;
    int completed = 0;
    int *executed = (int *)calloc(n, sizeof(int));
    
    while (completed != n) {
        int shortest = -1;
        int min_burst = INT_MAX;
        
        // Cari proses dengan burst time terpendek yang sudah tiba
        for (int i = 0; i < n; i++) {
            if (!executed[i] && processes[i].arrival_time <= current_time && 
                processes[i].burst_time < min_burst) {
                shortest = i;
                min_burst = processes[i].burst_time;
            }
        }
        
        if (shortest == -1) {
            current_time++;
            continue;
        }
        
        // Eksekusi proses sampai selesai (non-preemptive)
        processes[shortest].start_time = current_time;
        processes[shortest].finish_time = current_time + processes[shortest].burst_time;
        processes[shortest].waiting_time = processes[shortest].start_time - processes[shortest].arrival_time;
        processes[shortest].turnaround_time = processes[shortest].finish_time - processes[shortest].arrival_time;
        executed[shortest] = 1;
        current_time = processes[shortest].finish_time;
        completed++;
    }
    
    free(executed);
}

void srtf(Process processes[], int n) {
    // Shortest Remaining Time First (preemptive)
    int current_time = 0;
    int completed = 0;
    int *remaining_time = (int *)malloc(n * sizeof(int));
    
    for (int i = 0; i < n; i++) {
        remaining_time[i] = processes[i].burst_time;
    }
    
    while (completed != n) {
        int shortest = -1;
        int min_remaining = INT_MAX;
        
        // Cari proses dengan remaining time terpendek yang sudah tiba
        for (int i = 0; i < n; i++) {
            if (processes[i].arrival_time <= current_time && remaining_time[i] > 0 && 
                remaining_time[i] < min_remaining) {
                shortest = i;
                min_remaining = remaining_time[i];
            }
        }
        
        if (shortest == -1) {
            current_time++;
            continue;
        }
        
        
        if (remaining_time[shortest] == processes[shortest].burst_time) {
            processes[shortest].start_time = current_time;
        }
        
        // Eksekusi 1 unit waktu
        remaining_time[shortest]--;
        current_time++;
        
        // Jika proses selesai
        if (remaining_time[shortest] == 0) {
            processes[shortest].finish_time = current_time;
            processes[shortest].turnaround_time = processes[shortest].finish_time - processes[shortest].arrival_time;
            processes[shortest].waiting_time = processes[shortest].turnaround_time - processes[shortest].burst_time;
            completed++;
        }
    }
    
    free(remaining_time);
}

void print_results(Process processes[], int n, const char *title) {
    printf("\n%s\n", title);
    printf("PID | Arrival | Burst | Start | Finish | Waiting | Turnaround\n");
    printf("------------------------------------------------------------\n");
    
    float total_waiting = 0;
    float total_turnaround = 0;
    
    for (int i = 0; i < n; i++) {
        printf("%3s | %7d | %5d | %5d | %6d | %7d | %9d\n", 
               processes[i].pid, processes[i].arrival_time, processes[i].burst_time,
               processes[i].start_time, processes[i].finish_time, 
               processes[i].waiting_time, processes[i].turnaround_time);
        
        total_waiting += processes[i].waiting_time;
        total_turnaround += processes[i].turnaround_time;
    }
    
    printf("\nAverage Waiting Time: %.2f\n", total_waiting / n);
    printf("Average Turnaround Time: %.2f\n", total_turnaround / n);
}

int main() {
    // Contoh 1: SJF tanpa arrival time
    Process processes1[] = {
        {"P1", 0, 6, 0, 0, 0, 0, 0},
        {"P2", 0, 8, 0, 0, 0, 0, 0},
        {"P3", 0, 7, 0, 0, 0, 0, 0},
        {"P4", 0, 3, 0, 0, 0, 0, 0}
    };
    int n1 = sizeof(processes1) / sizeof(processes1[0]);
    
    sjf_nonpreemptive(processes1, n1);
    print_results(processes1, n1, "SJF without Arrival Time (Non-preemptive)");
    
    // Contoh 2: SJF dengan arrival time
    Process processes2[] = {
        {"P1", 0, 8, 0, 0, 0, 0, 0},
        {"P2", 1, 4, 0, 0, 0, 0, 0},
        {"P3", 2, 9, 0, 0, 0, 0, 0},
        {"P4", 3, 5, 0, 0, 0, 0, 0}
    };
    int n2 = sizeof(processes2) / sizeof(processes2[0]);
    
    sjf_with_arrival(processes2, n2);
    print_results(processes2, n2, "SJF with Arrival Time (Non-preemptive)");
    
    // Contoh 3: SRTF (preemptive)
    Process processes3[] = {
        {"P1", 0, 8, 0, 0, 0, 0, 0},
        {"P2", 1, 4, 0, 0, 0, 0, 0},
        {"P3", 2, 9, 0, 0, 0, 0, 0},
        {"P4", 3, 5, 0, 0, 0, 0, 0}
    };
    int n3 = sizeof(processes3) / sizeof(processes3[0]);
    
    srtf(processes3, n3);
    print_results(processes3, n3, "SRTF (Preemptive)");
    
    return 0;
}
```

## Penjelasan Implementasi:

1. **Struktur Data Process**:
   - Menyimpan semua atribut proses yang diperlukan untuk scheduling (PID, arrival time, burst time, dll)

2. **Fungsi SJF Non-preemptive**:
   - Mengurutkan proses berdasarkan burst time
   - Menjalankan proses secara berurutan dari yang terpendek
   - Menghitung waktu tunggu dan turnaround time

3. **Fungsi SJF dengan Arrival Time**:
   - Memilih proses dengan burst time terpendek dari yang sudah tiba
   - Menjalankan proses sampai selesai sebelum beralih ke proses lain
   - Menggunakan array executed untuk menandai proses yang sudah selesai

4. **Fungsi SRTF (Preemptive)**:
   - Setiap satuan waktu memeriksa proses dengan remaining time terpendek
   - Menggunakan array remaining_time untuk melacak sisa waktu eksekusi
   - Proses bisa diinterupsi jika ada proses baru dengan sisa waktu lebih pendek

5. **Fungsi Print Results**:
   - Menampilkan tabel hasil scheduling
   - Menghitung dan menampilkan rata-rata waiting time dan turnaround time

## Output:

![image](https://github.com/user-attachments/assets/5ed47b74-c8f2-4445-9249-4f3b67f4384b)


![image](https://github.com/user-attachments/assets/06645f86-6ca0-4763-ad0d-acd3ff042248)





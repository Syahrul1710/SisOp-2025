# CPU Scheduling Simulations in C

## 1. SJF Without Arrival Time (Non-Preemptive)
### Program Code
![image](https://github.com/user-attachments/assets/6763ac4f-73ec-4c51-acac-21c4f322ce76)

### Output Program
![image](https://github.com/user-attachments/assets/1f925e7c-ad0b-409e-aac7-330cc2f30801)
### analisis
This C program demonstrates the Shortest Job First (SJF) scheduling algorithm in its simplest form. The program collects process information from the user, including the number of processes and their respective burst times. It then organizes these processes from shortest to longest execution time.

Once sorted, the program calculates when each process would complete, how long it takes from start to finish (turnaround time), and how long each process waited before executing. These results are neatly displayed in a table format, along with the average turnaround and waiting times across all processes.

The SJF approach shown here prioritizes quick tasks, making the system more responsive for short jobs. However, it assumes all jobs are available simultaneously and doesn't account for new arrivals. While this implementation uses basic sorting for simplicity, it effectively illustrates how SJF scheduling can reduce average wait times when handling multiple processes.

## 2. SJF With Arrival Time (Non-Preemptive)
### Program Code
![image](https://github.com/user-attachments/assets/18454cd3-519e-4766-b663-d5357a815d1f)
![image](https://github.com/user-attachments/assets/68295897-2e33-49d4-8def-9763931e7b05)
### Output Program
![image](https://github.com/user-attachments/assets/2b058283-6cc9-42f1-a5c6-a13edb9984a1)
### Analisis
This program implements the Shortest Job First (SJF) scheduling algorithm with arrival times in a non-preemptive way. It first collects all process information including arrival times and burst times from the user input. The processes are initially sorted by their arrival times to handle real-world scenarios where jobs don't all arrive simultaneously.

The core scheduling logic works by examining which processes have arrived by the completion time of the current process and selecting the one with the shortest burst time to execute next. This creates an efficient scheduling sequence that minimizes average waiting time while respecting each process's arrival time. The program carefully tracks each process's start time, completion time, and calculates performance metrics including turnaround time (total time from arrival to completion) and waiting time (time spent ready but not executing).

For output, the program generates a detailed table showing all timing information for each process and computes the system-wide averages for turnaround time and waiting time. This implementation provides a practical example of how operating systems can prioritize shorter jobs to improve overall system responsiveness, while demonstrating both the benefits and limitations of non-preemptive scheduling approaches where once a job starts, it must complete before the CPU switches to another process.

## 3. SRTF (Preemptive) – Case Example as per PPT
### Program Code
![image](https://github.com/user-attachments/assets/72ff1e8b-838e-43e1-ba76-bf9cc34b7aa8)
![image](https://github.com/user-attachments/assets/5a9f27af-d4a2-42fa-8fc1-5dea58cfca87)
### Output Code
![image](https://github.com/user-attachments/assets/8b5d5729-787a-4144-b9e0-12c2e70c960b)
### Analisis
This C program implements the Shortest Remaining Time First (SRTF) preemptive scheduling algorithm, which is an advanced version of SJF that can interrupt running processes. The program starts by collecting process information including arrival times and burst times from user input. It initializes each process's remaining time to its burst time.

The core scheduling logic works by examining processes at each time unit to find the one with the shortest remaining execution time that has already arrived. The selected process executes for one time unit before the scheduler re-evaluates. When a process completes (remaining time reaches zero), the program calculates its completion time, turnaround time (total time from arrival to completion), and waiting time (time spent ready but not executing).

The implementation handles realistic scenarios where processes arrive at different times and can be interrupted. It maintains efficiency by always prioritizing the job closest to completion, which minimizes average waiting times. The program outputs detailed timing information for each process and computes system-wide averages.

For example, with processes arriving at times 0, 1, and 2 with burst times 8, 4, and 9 respectively, the scheduler would:
    Start P1 at time 0
    Switch to P2 at time 1 (shorter remaining time)
    Complete P2 at time 5
    Resume P1 until time 12
    Finally execute P3 until time 21

This approach provides better responsiveness than non-preemptive SJF, especially for short processes arriving after long ones have started. The code demonstrates fundamental OS scheduling concepts while using efficient data structures for process management.



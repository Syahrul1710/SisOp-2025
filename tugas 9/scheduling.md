### CPU Scheduling Simulations in C

## 1. SJF Without Arrival Time (Non-Preemptive)
# Program Code
![image](https://github.com/user-attachments/assets/6763ac4f-73ec-4c51-acac-21c4f322ce76)
# Output Program
![image](https://github.com/user-attachments/assets/1f925e7c-ad0b-409e-aac7-330cc2f30801)
# analisis
This program implements the SJF (Shortest Job First) Non-Preemptive scheduling algorithm without considering arrival times.

1) Main Program Components:
    proc Data Structure:
      no: Process number
      bt: Burst time (execution time)
      ct: Completion time
      tat: Turn Around Time
      wt: Waiting Time
    read() Function:
      Takes input for burst time of each process
      Returns a process struct with assigned number and burst time

Main Workflow:

Reads number of processes

Reads burst time for each process

Sorts processes by burst time (shortest to longest)

Calculates completion time, turn around time, and waiting time

Displays results and average statistics

Characteristics of Non-Preemptive SJF:
Non-Preemptive: Running process cannot be interrupted until completion

No Arrival Time: All processes are assumed to arrive simultaneously at time 0

Priority: Process with shortest burst time gets executed first

Advantages:
Minimizes average waiting time for a given set of processes

Simple to implement when all processes are available simultaneously

Disadvantages:
Can cause starvation for long burst time processes

Requires prior knowledge of burst times (not practical for interactive systems)

Not optimal when processes have varying arrival times



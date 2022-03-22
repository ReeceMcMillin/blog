+++
title = "Midterm Retrospective"
date = 2022-03-17
+++

# Part 1

1. A program becomes a process when executable is loaded into memory: **TRUE** (book p. 107)
2. VMWare is a virtual machine manager which manages guest operating systems: **TRUE**
3. Amdahl's Law describes performance gains for applications with both a serial and parallel component: **TRUE**
4. There is no universal definition of an operating system: **TRUE**
5. A system call is triggered by hardware: **FALSE**
6. Parallelism can be achieved on single-processor systems: **FALSE**
7. RR denegrates to FCFS: **TRUE**
8. Each device controller has a local buffer: **TRUE**
9. Applications compiled on one operating system can be directly executable on other operating systems due to common structure: **FALSE**
10. FCFS scheduling algorithm is non-preemptive: **TRUE**

# Part 2

1. operating system service: **GUI**
2. **system calls** provide interface to the services provided by an operating system
3. cause process to stop executing?
4. ...
5. ...
6. ...
7. code, data, files shared across multiple threads belonging to the same process

# Part 3

1. what program all times: **kernel**
2. two models for IPC: **shared memory, message passing**
3. responsiveness, resource sharing, economy, scalability
4. describe (blocking/non-blocking) (send/receive)
5. 5 challenges of multicore systems: dividing activities/balance/splitting/dependencies/testing

# Part 4

1. *describe* three general methods to pass parameters to OS during syscalls
   - registers
   - if more params than registers, stored in block/table of memory, address of block passed as parameter in register
   - parameters can also be placed onto the stack by the program, popped off by OS
2. name and describe different states that a process can exist in at any given time
   - new, running, waiting, ready, terminated
3. data parallelism vs task parallelism
   - distributes subsets of data across cores
   - distributes tasks across cores where each task performs unique op
4. similarities and differences between parallelism and concurrency
    - similarities: multiple tasks can make progress before one finishes
    - differences: 
5. describe how OS helps facilitate debugging issues
   - log files, core dumps, crash dump, trace listing, event logs
6. policy vs. mechanism
   - policy: what will be done?
   - mechanism: how?
   - separation allows maximum flexibility if policy decisions are to be changed later


# scheduling

| process ID | arrival | burst time |
| :--------: | :-----: | :--------: |
|     0      |    0    |     6      |
|     1      |    1    |     4      |
|     2      |    2    |     3      |
|     3      |    4    |     6      |
|     4      |    6    |     5      |
|     5      |    7    |     8      |
|     6      |    9    |     2      |

| algorithm | response | turnaround | total wait |
| :-------: | :------: | :--------: | :--------: |
|   srtf    |    7     |   12.86    |    8.0     |
|    sjf    |   8.14   |   18.14    |   13.29    |

+++
title = "Chapter 4, 5 Quiz"
date = 2022-03-04
[extra]
mathjax = true
+++

1. Which of the following items are shared across multiple threads belonging to the same process?

   - <mark>code</mark>
   - stack
   - <mark>files</mark>
   - <mark>data</mark>
   - registers

2. What are the benefits of multi-threaded programming?
   - [x] resource sharing 
   - [x] economy
   - [x] responsiveness
   - [ ] easy debugging
   - [X] scalability

3. Which of the following refers to the capability to allow multiple tasks to make progress on a single-processor system?

   - [ ] data parallelism
   - [ ] task parallelism
   - [ ] parallelism
   - [X] concurrency

    {% boxed(title="amdahl's law") %}
    If $S$ is the is the portion of the application that must be performed serially on a system with $N$ processing cores,
    $$speedup \leq \frac{1}{S + \frac{(1-S)}{N}}$$
    {% end %}

4. **Amdahl's Law** is the formula that identifies potential performance gains froma dding additional computing cores to an application that has both a parallel and serial component.

5. **Ensuring there is a sufficient number of cores** is not considered a challenge when designing applications for multicore systems.

6. Which of the following models are possible for the relationship between user threads and kernel threads?

   - [X] many-to-many model
   - [X] many-to-one model
   - [X] two-level model
   - [ ] one-to-many model
   - [X] one-to-one model

7. The **one-to-one** model maps each user-level thread to one kernel thread.

8. The **many-to-many** model multiplexes many user-level threads to a lesser or equal number of kernel threads.

9. Which are included in the context of a thread?

   - [X] private storage area
   - [X] register set
   - [X] stacks

10. The ready queue can be implemented as a **tree**, **unordered linked list**, **FIFO queue**, or **priority queue**.

11. *Cooperative* scheduling can take place under the following circumstances:
    - running $\to$ waiting
    - process termination

12. *Preemptive* scheduling can take place under the following circumstances:
    - running $\to$ ready
    - waiting $\to$ ready

13. Which of the following items do not belong to the function of a dispatcher?
    - selecting a process among the available ones in the ready queue

    {% boxed(title="roles of the dispatcher") %}

    - switches context from one process to another
    - switching from kernel mode to user mode
    - jumping to the proper location in the user program to resume that program

    {% end %}

14. Assume process $P_0$ and $P_1$ are the process before and after a context switch, and $PCB_0$ and $PCB_1$ are respectively their process control blocks. Which of the following time units are included inside the dispatch latency?

    - [ ] $P_1$ executing
    - [ ] $P_0$ executing
    - [X] save state into $PCB_0$ and restore state from $PCB_1$

15. Which of the following criteria is more important for an interactive system?

    - [ ] Turnaround Time
    - [ ] Throughput
    - [X] Response Time
    - [ ] CPU Utilization

16. Which of the following criteria is more important from the point of view of a particular process?

    - [X] Turnaround Time
    - [ ] Throughput
    - [ ] Response Time
    - [ ] CPU Utilization

17. I/O-bound programs typically have many short **CPU bursts**, while CPU-bound programs might have a few long **CPU bursts**.

18.  The **convoy effect** occurs in FCFS scheduling when a process with a long CPU burst occupies the CPU.

19.  A significant problem with priority scheduling algorithms is **starvation**.

20.  The process burst time is:

     - [ ] stored in the PCB
     - [X] used to process scheduling
     - [ ] an exact value
     - [X] an estimate
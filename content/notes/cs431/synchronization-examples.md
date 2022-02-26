+++
title = "Synchronization Examples"
date = "2022-02-24"
[extra]
mathjax = true
+++

# Classical Problems

## Bounded-Buffer Problem

Consider \\(n\\) buffers, each able to hold one item. Also consider three semaphores defined to the following values:

\\[
\begin{align}
    \text{mutex} &:= 1\\\\
    \text{full} &:= 0\\\\
    \text{empty} &:= n
\end{align}
\\]

{{ annotation(language="C", context="producer process") }}
```c
do {
    /* produce an item in next_produced */
    wait(empty);
    wait(mutex);

    /* add next produced to buffer */

    signal(mutex);
    signal(full);
} while (true);
```

{% callout(type="note") %}
`wait` indicates a program is waiting to enter the critical section

{% end %}

{{ annotation(language="C", context="producer process") }}
```c
do {
    /* remove item from buffer to next_consumed */
    wait(full);
    wait(mutex);*

    /* consume item in next consumed */

    signal(mutex);
    signal(empty);
} while (true);
```

## Readers & Writers Problem

{{ annotation(language="C", context="writer process") }}
```c
do {
    wait(rw_mutex);
    // perform write
    signal(rw_mutex);
} while true
```

## Dining-Philosophers Problem


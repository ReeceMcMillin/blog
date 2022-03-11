+++
title = "Main Memory"
date = 2022-03-10
+++

# Background

Program must be brought from disk into memory and placed within a process to be run.

Main memory and registers are the only storage the CPU can access directly

Memory unit only sees either:
- a stream of addresses with read requests
- address *and* data with write requests

# Base and Limit Registers

A pair of *base* and *limit*registers define the logical address space. The CPU has to check *every* memory access generated in user mode to be sure it is between the base and limit for that user.

# Binding of Instructions and Data to Memory

- Compile Time
  - typically limited to OS code
- Load Time
  - Must generate *relocatable code* if memory location is not known at compile time
- Execution Time

# Logical vs. Physical Address Space

Logical addresses are bound to a separate physical address space. The logical address is generated by the CPU, but the memory unit only sees the physical address.

Logical Address Space: the set of all logical addresses generated by a program.

{% definition(term="Memory Management Unit (MMU)") %}
The hardware device that, at runtime, maps virtual addresses to physical addresses.
{% end %}

# Dynamic Linking

{% definition(term="Static Linking") %}
System libraries and program code are combined by the loader into the binary program image.
{% end %}

Small piece of code (**stub**) used to locate the appropriate memory-resident library routine. The stub then replaces itself with the address of the routine and executes it.

The operating system checks whether or not the routine is in the process's memory address, adding it if not.

# Swapping

A process can be **swapped** temporarily out of memory to a backing store, then brought back for continued execution.

{% definition(term="Backing Store") %}
Fast disk large enough to accommodate copies of all memory images for all users. Must provide direct access to these memory images.
{% end %}

Roll out, roll in refers to a variant of swapping used for priority-based scheduling algorithms.
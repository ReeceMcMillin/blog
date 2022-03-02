+++
title = "Consensus"
date = 2022-03-01
[extra]
mathjax = true
+++

# Overview

Consensus is an "agreement" problem.

{% definition(term="Consensus") %}

A collection of processes "agree" on a value after one or more processes propose values

{% end %}

## Qualities

- **Safety**: all agree on *some* value eventually
- **Liveness**: all agree on the *same* value

## Applications

- Two Generals Problem: attack or retreat?
- Financial transaction between two entities
- Data copy across multiple storage nodes
- Mutual exclusion
- Leader election
- Totally-ordered multicast

{% annotation(context="The Two Generals Problem") %}
![Two Generals Illustration](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/2-generals.svg/1024px-2-generals.svg.png)

{% end %}

## The Problem of Consensus
### Problem Definition

- A collection of processes \\(p_i, i \in \mathbb{N}\\)
    - Processes can fail, but message delivery is **reliable**
- Each process \\(p_i\\) proposes some value \\(v_i\\)
- each process has a **decision variable** \\(d_i\\)

Each process has two states: \\(\\{decided, undecided\\}\\)

### Goal
- set values to \\(d_i\\)
- agree on \\(d_i\\) value - everyone shares the same \\(d_i\\).

{% aside(title="Trivial Consensus") %}
Solution to consensus is trivial if *no process fails* and *the system is synchronous*. That's not very interesting!

{% end %}

### Solution

Things become arbitrarily complicated when we introduce the possibility of *process failure*.

In most cases, proposed values are **binary**, with processes picking the majority value.

# Consensus Requirements

Consensus in the presence of failures requires a notion of *failed processes* and *correct processes*.

## Requirements

- Termination (liveness)
- Agreement (safety)\\[p_i, p_j \text{ correct} \implies (d_i = d_j)\\]
- Integrity (safety)

Integrity can be of a weaker type - not all processes necessarily need to agree

# Consensus Algorithm

First, let's think about how to design an algorithm under the assumption that *no process fails*.
- All processes \\(\\{p_1, \dots, p_n\\}\\) collect all values \\(\\{v_1, \dots, v_n\\}\\) other processes propose.
- Each process \\(p_i\\) computes \\(d_i\\) as
\\[d_i = \text{max}(\\{v_1, \dots, v_n\\} \cup\text{undecided})\\]

## Analysis

Does this algorithm **terminate**?
- Yes (if no process failures and message delivery is reliable)
- If processes might fail:
  - in synchronous model, the algorithm **can** be modified to terminate
  - in asynchronous model, you *cannot* guarantee termination

Does this algorithm guarantee **agreement**?

Does this algorithm guarantee **integrity**?

Majority function (or some other - min, max, etc.) ensures **agreement** and **integrity** are upheld.

## Consensus in Synchronous Model

{% aside(title="further reading") %}
Tanenbaum describes this under "flooding consensus" [Cachin et al. 2011] on page 438.
{% end %}

Process can detect reliably if another process has failed, dropping the process from the consensus.

The algorithm runs in rounds. Consider a situation in which \\(f\\) failures are acceptable:
- at each round, all correct processes collect proposed values from *all* others
- repeats the process \\(f + 1\\) rounds

After \\(f + 1\\) rounds, correct processes will agree.

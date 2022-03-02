+++
title = "Leader Election"
date = 2022-02-22
[extra]
mathjax = true
+++

{% callout(type="warning") %}
This isn't the first lecture on this subject, may need to reference mdBook notes.
{% end %}

# Bully Algorithm

- One process initiates the election
  - Sends election message \\(e\\) to all *higher ID* processes
    - think: if a process has a lower ID than the process sending the message, it couldn't be the leader
  - Processes respond with answer message \\(a\\) and begin another election
  - If an initiating process receives no answers, it considers itself the leader and sends coordinator message \\(c\\).

## Analysis

### Safety

- at most one process becomes the leader/coordinator
- if crashed process is replaced with same identifier, it is **not** safe
- same can happen when failure detection fails

### Liveness

- only if message delivery is reliable (assumed)

### Complexity

- Best case: \\(N - 2\\) messages
  - when the next highest ID process (would-be leader) detects the failure of coordinator
  - sends "coordinator" to all other processes
- Worst case: \\(O(N^2)\\) messages
  - when *smallest* process detects coordinator failures and starts election
  - all other processes reply "answer" and starts election

{% callout(type="error") %}

Leader election is **impossible** in asynchronous communication models!

{% end %}
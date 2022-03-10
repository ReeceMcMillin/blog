+++
title = "Group Communication"
date = 2022-03-10
[extra]
mathjax=true
+++

{% definition(term="Group Communication") %}
A form of **indirect** communication where senders and receivers are decoupled in time and/or space.
{% end %}

Group communication enables a sender to send a message to a **group**.
- message is propagated to *all* members in the group - also known as multicast.

Message delivery satisfies:
- reliability of delivery: deliver to all, some, or none?
- order of delivery - FIFO, causal, total order?

## Types of Group Communication

1. When member process are known and usually fixed
   - usually called multicast to a group
   - usually easy to implement and provide guarantees   
2. When group members can change
   - members can dynamically join and leave
   - usually hard to satisfy guarantees

# System Model

A collection of processes that communicate reliably (with the exception of crash failures) with one-to-one channels. Processes can be a member of multiple groups where a sender multicasts a message to the whole group.

# Multicast Operations

Two primitive operations:

- $\text{multicast}(m, g)$
  - multicast message $m$ into group $g$
  - group $g$ is the set of process who are the members of $g$
- $\text{deliver}(m)$
  - deliver message $m$ sent by multicast to the calling process
  - the application is given the message to process
  - slightly different than $\text{receive}(m)$

Every message contains a unique identifier of the process who sent the message.

- $\text{sender}(m)$
  - the sender of multicast message $m$
- $\text{group}(m)$
  - the group identifier where message $m$ is sent.

# Basic Multicast

## Implementation
<div class="columns">
    <div class="column">

{% annotation(context="sender") %}

```
B-multicast(m, g):
    for each p in g,
        send(p, m)
```

{% end %}

</div>
<div class="column">

{% annotation(context="receiver") %}

```
On receive(m) at p:
    B-deliver(m) at p
```

{% end %}

</div>
</div>




## Problems

### Failure

If a multicast operation fails in the middle (for example, on some `p` in `g`), group communication semantics are violated. This means that basic multicast is **not** reliable even though it uses reliable send operations!

### ACK Explosion

Implementing reliable `send` operations requires receivers to acknowledge (`ACK`) delivery to the sender to prevent retransmission. With a large number of senders, `ACK`s can overflow the sender's buffer causing inadvertent retransmission.

# Reliable Multicast

Multicast with reliability of message delivery.
- $\text{R-multicast}(m, g)$
- $\text{R-deliver}(m)$

{% aside(title="note") %}
Reliable multicast is analogous to reliable one-to-one communication!
{% end %}


## Three Properties
- Integrity: a correct process $p$ delivers message $m$ *at most once*.
- Validity: if a correct process multicasts message $m$, then it will eventually deliver $m$.
  - this seems unusual - should the sender deliver to itself? *yes!*
- Agreement: if a correct process delivers $m$, then *all correct processes* in $\text{group}(m)$ will *eventually* deliver $m$.
  - atomicity: all or none

## Reliable Multicast Using B-Multicast

{% math(title="R-Multicast") %}

- on init
    - received := {}

- for process p to R-multicast message m to group g
    - B-multicast(g, m)

- on B-deliver(m) at process q with g = group(m)
    - if (m \neq Received) then
        - received := Received $\cup$ \{m\}
        - if (q \neq p) then B-multicast(g, m)
        - R-deliver m

{% end %}

## Properties

Correct for asynchronous system
- expensive
  - each message is sent $|{g}|$ times to each process
- for efficiency, R-multicast can use
  - IP-multicast - one send operation
  - Piggyback acknowledgements - ACK sent on successive messages
  - Negative acknowledgements - ACK for missing messages

Every message in a group has a *sequence number*
- starts at 0, incrementing by 1 whenever a new message is sent ou tin the group
  
Each process $p$ keeps two numbers:
- $S(g, p) =$ the sequence number that $p$ has sent so far
- $R(g, q) =$ the largest sequence number of a message delivered from process $q$.

Each message that $p$ sends contains
- $S(g, p)$
- $\left<q, R(g, q)\right>$ list

Whenever a process $p$ sends a message to the group:
- $S(g, p) = S(g, p) + 1$

A process $Q$ gets a message from process $p$ with sequence $S$ in it:
- R-deliver the message if and only if $S = R(g, p) + 1$, increment $R(g, p)$
- If $S \leq (g, p)$, the message has already been delivered, discard
- If $S > R(g, p) + 1$, process $Q$ might have missed some messages

{% aside(title="key") %}

this hold-back queue is the thing that makes the whole thing work!

{% end %}


What happens to messages that arrive out of sequence?
- if already delivered, discard
- otherwise, keep them in a **hold-back-queue**, but do not deliver yet
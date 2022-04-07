+++
title = "Peer-to-Peer Systems"
date = 2022-04-07
+++

A {{ reference(term="peer-to-peer") }} system enables sharing of data and resources on a very large scale by eliminating any requirement for separately managed servers and their associated infrastructure.

In client-server architectures:
- servers are managed by the service providers and become bottlenecked when the number of clients grows
- administration and fault recovery costs dominate
- the network bandwidth available to a server site is also a major constraint

In peer-to-peer architectures, support distributed services and applications using data and computing resources available in the personal computers and workstations

> p2p exploits resources available at the "edges" of the internet
> <cite>[Shirky 2000]</cite>

The key aspects of peer-to-peer architectures are the placement and retrieval of information objects.

## System Characteristics

- design ensures each user contributes resources to the system
- although participants *may differ* in the resources that they contribute, all the nodes have the same functional capabilities and responsibilities
- correct operation doesn't depend on the existence of any centrally administered systems
- can be designed to offer a limited degree of anonymity to the providers and users of resources
- a key issue for the efficient operation is the choice of an algorithm for the placement of data across many hosts and subsequent access to it in a manner that balances the work load and ensures availability without adding undue overhead

## Examples

### Early Systems

- DNS and Usenet adopted multi-server system
- Xerox Grapevine name registration and main delivery system
- SETI@home
  - **S**earch for **E**xtra-**T**errestrial **I**ntelligence
  - a few servers and *lots* of client machines/volunteers
  - distribution of tasks managed by servers, but work completed by users

### Modern Systems

- **First Generation**: Napster
- **Second Generation**: file sharing applications
  - Freenet, Gnutella, Kazaa, BitTorrent
- **Third Generation**: distributed object store
  - also known as DHT
  - sometimes application agnostic middleware
  - examples: Chord, Pastry, Tapestry, Kademlia, Content-Addressable Network (CAN)
- **Fourth Generation**: blockchain

## P2P Systems

- distribution
  - place resources across different peers
- discovery / routing
  - when requested, messages are routed to **discover** where the resources are and retrieve them (**routing**)
- replication
  - resources are typically **replicated** onto multiple peers for better availability
- naming
  - resources have names or IDs (usually a GUID)

P2P systems are usually good for *immutable objects*.

## P2P Middleware

Key issue: to **distribute** resources and **locate** them. in a decentralized fashion.
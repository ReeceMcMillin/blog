+++
title = "Distributed File Systems"
date = 2022-03-24
[extra]
mathjax = true
class = "CS490"
+++

## Files and File Systems

A {{reference(term="file system")}} is a basic service that any operating system provides.

A file contains both *data* and *attributes*.

Basic file operations:
- `open()`, `create()`
- `read()`
- `write()`
- `close()`

## File System Operations

- Directory Service
  - Organize files in a directory structure
  - Files have human-readable names
- Storage of files onto hard disk
  - File consists of *blocks* (usually 4KB)

## Distributed File System

Distributed File Systems (DFS) support similar functionalities throughout an intranet (LAN).
- provide access to files stored at a server with similar performance and reliability to files stored on local disks.

### Requirements

- Transparency
  - access, location, mobility, scale
- Concurrency
- Replication
  - share loads *and* enhance fault tolerance
- Heterogeneous
- Fault Tolerance
- Consistency
  - *one-copy* update semantic
- Security
- Efficiency

### Issues

- file & directory naming: locate the file!
- semantics: client/server operations, file-sharing
- performance and scalability
  - fault tolerance
  - deal with remote server failures
- implementation considerations
  - caching
  - replication
  - update protocols
#### Naming

- Explicit naming
  - machine + path (`/machine/path`)
  - one namespace but *not* transparent
- Implicit naming
  - location transparency
    - file name doesn't include the name of the server where file is stored
  - mounting remote filesystems onto local file hierarchy
    - view of the filesystem may be different on each computer
  - full naming transparency
    - a single namespace that looks the same on all machines
#### Semantic - Operational
- fault tolerance
  - at-most-once semantics for file operations
  - at-least-once semantics with a server protocol designed in terms of idempotent file operations
  - replication (stateless, so servers can be restarted after failure)

#### Semantic - File Sharing
- one-copy semantics
  - updates are written to the single copy and are available immediately
  - all clients see contents of file identically as if only *one copy* of file exists
  - if caching is used: after an update operation, no program can observe a discrepancy between data in cache and stored data
- serializability
  - transaction semantics (file locking protocols implemented - share for read, exclusive for write)
  - session semantics
    - copy file on open, work on local copy and copy back on close

## File Service Architecture

### Flat File Service

- implements operations on the contents of files
- uses Unique File Identifiers (UFIDs) to refer to files
- a new UFID is generated whenever a file creation is requested

### Directory Service
- mapping between text names for files and their UFIDs
- clients may obtain UFID by quoting its text name to the directory service (lookup)
- provides functions to
  - generate directories
  - add new file names to directories
  - obtain UFIDs to directories

### Client Module

- run in client machines
- provide APIs for user-level programs for accessing file and directory services
- holds information about the network locations of the file/directory server processes
- caches file blocks for improved performance

## Network File Service

### Operations

- Flat File
  - `read(FileID, i, n) -> Data`
  - `write(FileID, i, Data)`
  - `create() -> FileID`
  - `delete(FileID)`
  - `GetAttributes(FileID) -> Attr`
  - `SetAttributes(FileID, Attr)`

{% aside(title="why?") %}
Why aren't there open or close operations?

The server is meant to be *stateless!*
{% end %}


This API is very similar to UNIX's file system opeations with some notable differences:
- no open or close functions
- all operations except create are idempotent (to allow at-least-once RPC semantic)
- the operations can be implemented by a *stateless* server

### Modules

- **server module** resides in the kernel on each computer that acts as an NFS server
- **client module** resides on client computer who accesses the files
- requests referring to a remote file system (RFS) are translated by the client module to NFS protocol operations and passed to server module
  - communication mostly happens via RPC

NFS provides access transparency
- user programs issue file operations on local/remote files without distinction

VFS enables **remote files** to appear as **local files** using file handles. File handles have three parts:
- filesystem identifier
  - unique ID given to *entire* file system
- i-node number
  - unique number to identify and locate a file within the file system
- i-node generation number
  - in UNIX, i-node is reused when a file is deleted (this keeps an extra counter when reused)

VFS layer contains v-node per open file (like i-node in UNIX). For local files, v-nodes *are* i-nodes. For remote files, v-nodes are file handles.

### Client Authentication

Unlike convential UNIX operating system, NFS server is **stateless** (does not keep file "open" on behalf of client).
- every request is independent of others, so the server 

### Server Interface

- $create(dirfh, name, attr) \to newfh, attr$

### Mount Service

Makes *remote file system* avaiable to *local* client by specifying remote host name and pathname of the directory.

- Local: `/usr/x`
- Remote: `/usr/students/big`
- Remote: `/usr/staff/jane`

```linenos
fname = /usr/x
fp = fopen(fname, "r")
data = read(fp, 1024)
```

#### Mount Procedure

- NFS Server runs a separate (user-level) mount service process
  - in the server, there is a file with a well-known name (`/etc/exports`) containing the names of local filesystems that are available for remote mounting
  - an access list may indicate which hosts can mount
- NFS clients use `mount` command to request mounting
  - by specifying the remote host's name, the pathname of a directory in the remote filesystem and the local name with which it is to be mounted
{% aside(title="Example") %}
`mount <remote server> <remote dir> <local name>`
{% end %}
- Mount command uses and RPC-based *mount protocol*
  - takes directory pathname and returns file handle
  - the location (ip/port) of the server and the file handle for the remote directory are passed onto the VFS layer and NFS client
- Two types of mounting:
  - hard mounted
    - user program is suspended until operation completes
    - if the server fails, waits until server is back (as though nothing happened)
  - soft mounted
    - an error is returned after some small number of retries
    - the client program then needs to do necessary recovery/reporting action

### Caching

Caching is an important operation common in operating systems to achieve enhanced performance.
- file content is stored on disk
- if each request needs to go to disk directly, that would be too slow!
- instead, OS usually "caches" content (blocks) read from the disk into memory

In NFS, both client *and* server can cache blocks.

- $read$ `/remote/file1 1-1000`
- $read$ `/remote/file1 1001-2000`

{% aside(title="note") %}
Consistency is a *consensus* problem. How does a collection of processes agree that a change happened?
{% end %}

The server may want to cache a requested block in case *other* clients want it.
A client may want to cache a requested block in case it expects to read from it many times.

What problems would this pose? *Consistency*!

#### Server Caching

NFS servers use cache to hold disk blocks. Typically two types of cache operations are used:
- *read-ahead*: read blocks ahead of time (spatial locality from 281)
- *delayed-write*: hold blocks in memory and do not write to disk (cache is replaced by new content)

Read does not cause any consistency issues, but write might! Two options exist for writing:
- {{ reference(term="write-through") }}
  - fast at the cost of safety
- {{ reference(term="write-commit") }}
  - safe at the cost of speed

#### Client Caching

NFS client module caches the rusult of certain operations
- usually `read`, `write`, `getattr`, `lookup`, and `readdir` operations.

Client caching may allow different versions of files to exist in different client nodes.
- writes by a client do not update cached copies of other clients
- clients need to check with the server (and pull updated ones)

To check validity of a cached block, a timestamp-based validation is used
- a cached block is valid if it wasn't updated since last cached
- only checks after a certain interval (called *freshness*) has elapsed

$$ \text{Validity Condition} = (T - Tc < t) \vee (Tm_\text{client} = Tm_\text{server}) $$

- $T =$ current time
- $Tc$ = last validated
- $Tm$ = last modified

### Summary

- Transparency
- Replication
- Hardware/OS Heterogeneity
- Fault Tolerance
  - server failurse may suspend clients (except for soft-mounting)
  - NFS access protocol is stateless and idempotent (no state = easy recovery)
- Consistency
  - approximately {{ reference(term="one-copy semantic") }}, but not fully

# Andrew File System

Two major differences from NFS:
- Whole-file serving: entire contents of directories and files are transmitted to clients by AFS servers
- Whole-file caching: once a copy of a file or chunk has been transferred to a client computer, it is stored in a cache on the local disk
  - cache contains several hundred of the files most recently used on that computer
  - cache is permanent, survives reboots
  - local copies of files are used to satisfy clients' open requests in preference to remote copies whenever possible

Okay, but *why* whole-file serving/caching?
- designed for multi-user systems
  - each user has a designated `/users/home` directory and a set of shared files (common libraries, OS files)
- `home` directory contents are updated by a single user
- shared files are rarely updated, mostly read-only

Core design goal: **scalability**
- AFS is designed to perform well for a system with a large number of users

Design Points
- files are small, most < 10KB
- read operations are much more common (about 6x) than writes
- sequential access is common, random access is rare
- most files are read/written by only one user
  - when a file is shared, it is usually only one user who modifies it
- files are referenced in bursts (temporal locality)

Notably, AFS doesn't fit the database use-case well because one file is used by multiple users.

## AFS Implementation

AFS uses a *session semantic*.
- entire file is copied to local machine (venus) from the server (vice) when the file is opened.
  - if the file is larger than 64KB, copied in chunks

{% aside(title="warning") %}
the AFS implementation section wasn't finished, refer to ppt
{% end %}

### Update Semantics

AFS provides cache consistency only on `open` and `close` operations.

If clients in different workstations `open`, `write`, and `close` the same file concurrently, all except the *last* close wil be silently lost.
- weaker consistency
- clients need to manage concurrency on their own

Strict {{ reference(term="one-copy semantic") }} require results of each write to be distributed to all sites holding the file in their cache before any further accesses can occur.
- this isn't practical in large-scale systems
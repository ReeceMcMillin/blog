+++
title = "Distributed File Systems"
date = 2022-03-24
[extra]
mathjax = true
class = "CS490"
+++

## Files and File Systems

A {{ reference(term="file system") }} is a basic service that any operating system provides.

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

## NFS Modules

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

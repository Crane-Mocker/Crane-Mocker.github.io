---
layout: post
title:  "Linux Memory"
date:   2022-06-10
categories: linux
---

# Linux Memory


<!-- vim-markdown-toc GFM -->

* [Memory Hierarchy](#memory-hierarchy)
* [Linux Memory Management](#linux-memory-management)
* [Clear RAM Memory](#clear-ram-memory)
* [Ref](#ref)

<!-- vim-markdown-toc -->

## Memory Hierarchy

Memory is the component within the computer which allows short-term data access.

Von Neumann architecture or Princeton architecture:
![von Neumann architecture](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e5/Von_Neumann_Architecture.svg/300px-Von_Neumann_Architecture.svg.png)

Harvard architecture:
![Harvard architecture](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3f/Harvard_architecture.svg/362px-Harvard_architecture.svg.png)

*The Harvard architecture is a computer architecture with separate storage and signal pathways for instructions and data, while in von Neumann architecture, instructions and data share a common bus, so that an instruction fetch and a data operation cannot occur at the same time.*

There are 2 main types of memory hierarchy: primary memory and secondary memory.

**Primary memory(Internal Memory)**: a segment of computer memory that can be accessed directly by the processor. Comprising of Main Memory, Cache Memory & CPU registers.

**Secondary Memory(External Memory)**: peripheral storage devices which are accessible by the processor via I/O Module. Comprising of Magnetic Disk, Optical Disk, Magnetic Tape

![Memory Hierarchy](https://media.geeksforgeeks.org/wp-content/uploads/Untitled-drawing-4-4.png)

Primary memory includes RAM and ROM.

![RAM and ROM](https://media.geeksforgeeks.org/wp-content/uploads/memory.png)

RAM, Random Access Memory, is a volatile memory as the data is lost when the power is turned off.

![DRAM and SRAM](https://media.geeksforgeeks.org/wp-content/uploads/difference-1.png)

ROM, Read-Only Memory, stores crucial information to operate the system, like boot. It is classified into 4 types MROM, PROM, EPROM, and EEPROM.

## Linux Memory Management

**Physical memory**: The physical system memory is divided into **page**s.

**Virtual memory**: abstracts the details of physical memory from the application software. Each and every memory access uses a **virtual address**.

**Page tables**: Each physical memory page can be mapped as one or more virtual page, which is described by page tables. Namely, page tables, which are organized *hierarchically*, translate a virtual address used by programs to Physical memory address.

**TLB**: Translation Lookaside Buffer, the cache of mentioned translation above.

**Page cache**: Whenever a file is read, the data is put into the page cache to avoid expensive disk access on the subsequent reads. Similarly, when one writes to a file, the data is placed in the page cache and eventually gets into the backing storage device.

**Zswap**: Zswap is a lightweight compressed cache for swap pages. It takes pages that are in the process of being swapped out and attempts to compress them into a dynamically allocated RAM-based memory pool. <font color="Crimson">(a new feature as of v3.11)</font>


## Clear RAM Memory

Check memory usage:

```bash
free -m # use MB
cat /proc/meminfo
vmstat -s #lays out the memory usage statistics
top
htop
```

Hardware information about the installed RAM: `sudo dmidecode -t 17` or `sudo dmidecode -t memory`

**Clear RAM without killing app or service**
Clear PageCache only: `sync; echo 1 > /proc/sys/vm/drop_caches`
Clear dentries and inodes: `sync; echo 2 > /proc/sys/vm/drop_caches`
Clear pagecache, dentries, and inodes: `sync; echo 3 > /proc/sys/vm/drop_caches`

<font color="AliceBlue">
`sync`: Synchronize cached writes to persistent storage.
Writing to `drop_cache` will clean cache without killing any application or service.
</font>

**CLear Swap Space**
`swapoff -a && swapon -a`

## Ref

[difference between memory and storage](https://www.kingston.com/en/blog/pc-performance/difference-between-memory-storage)
[Memory architecture](https://en.wikipedia.org/wiki/Memory_architecture)
[Memory Hierarchy Design and its Characteristics](https://www.geeksforgeeks.org/memory-hierarchy-design-and-its-characteristics/)
[Random Access Memory (RAM) and Read Only Memory (ROM)](https://www.geeksforgeeks.org/random-access-memory-ram-and-read-only-memory-rom/)
[Memory Management](https://www.kernel.org/doc/html/latest/admin-guide/mm/index.html)
[5 commands to check memory usage on Linux](https://www.binarytides.com/linux-command-check-memory-usage/)
[How to Clear RAM Memory Cache, Buffer and Swap Space on Linux](https://www.tecmint.com/clear-ram-memory-cache-buffer-and-swap-space-on-linux/)
[Random Access Memory (RAM) and Read Only Memory (ROM)](https://www.geeksforgeeks.org/random-access-memory-ram-and-read-only-memory-rom/)

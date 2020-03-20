# Linux Kernel

[TOC]

## Abstract

### Why I want to write this blog
As a fun of Linux operating systems and a fun of Linus himself, I always want to discover more about Linux kernel.
Thanks to the all the developpers in this community, I have access to learn more. I want to write down something I got from the journey of discovering Linux kernel and I hope it will be useful for the other techs.

### Reference

*Linux, a free unix-386 kernel* by <font color="red"> Linus Torvalds </font>

*A Heavily Commented Linux Kernel Source Code Kernel Version 0.12 (Chinese Revision 5)* by <font color="red">Zhao Jiong</font> 

*Understanding the Linux Kernel, 3rd Edition* by <font color="red">Daniel P. Bovet, Marco Cesati</font>

### Acknowledgements
Prof.Yan Fei, Bzq who helped me with understanding the technology and even the history of Linux better. 

## Linux versions and the changes

[Here](https://en.wikipedia.org/wiki/Linux_kernel_version_history) is the detailed Linux kernel version history.

The table below doesn't contain all the versions, just some ones with new features or the ones really important.

After version 2.5, Linux kernel visions use three numbers, separated by `.`
`The.Version.the-release`
The first two numbers were used to identify the version, the third number identified the release. 

From 0.01 to 1.0

Version No. | Discription
--- | ---
0.01 | Multi-threaded file system,segmentation(分段), and paging memory management(分页内存管理).</br> No floppy disk drivers(软盘驱动) yet.
0.10 | Memory allocation library functions.</br>Boot dir contains script converting as86 assembler syntax to gas.(Because gas is GNU Assembly)
0.11 | Supports hard disk, floppy drive devices, serial communications
0.12 | Increased the software simulation program of math coprocessor<font color="grey">(Alternatively referred to as a numeric coprocessor or a floating-point coprocessor. The math coprocessor was an optional add-on for the Intel 8086, 80386 and 80486 processors that allowed computers to perform faster mathematical calculations, increasing its overall performance.)</font></br>Added job control, file symbolic links, virtual memory swapping capability.
0.95.x | Added virtual file system support.</br>Added login functionality. Changed hard disk naming and numbering from what of the MINIX to current Linux.</br>Supported CDROM
0.96.x | UNIX socket support, ext file system alpha tester, SCSI drivers.</br>Floppy disk type is automatically recognized.The keyboard driver has been rewritten with C.
0.97.x | Dynamic caching, msdos and ext file system support, bus mouse drivers.
0.98.x | Improve support for TCP/IP (0.8.1) networks, correct extfs errors. </br> Rewritten memory managementbr section.
0.99.x | Re-design the process of the use of memory allocation, each process has 4G linear
space. Constantly improving the network code. NFS support.
1.0 | The first official version.

[Here](https://www.thomas-krenn.com/en/wiki/Linux_Kernel_Versions) is the new features of Linux kernels after 2.6.18

## Basic operating system concepts

### Kernel and the other programs

Kernel is the most important part of OS. It is loaded into RAM when the system boots and contains critical procedures needed for the OS to operate.

The other programs provide a variety of interactive experiences for user and do the jobs user bought for the computer.

### 2 needs for OS
1. Interact with the hardware components, servicing all low-level programmable elements included in he hardware platform.
2. Provide an execution environment to the applications that run on the computer system (the so-called ser programs)

MS-DOS allows user programs play with hardware components directly.
Unix-like OSs hide all low-level details concerning the physical organization of a computer from user programs.

Modern operating systems rely on the availability of specific hardware features, which forbid user programs to directly interact with low-level hardware components or to access arbitrary memory locations.

In particular, the hardware introduces at least two different execution modes for the CPU:

1. nonprivileged mode for user programs (Unix: User Mode)
2. privileged mode for the kernel. (Kernel Mode)

### Multiuser Systems

A multiuser system is a computer that is able to concurrently and independently execute several applications
belonging to two or more users.

It needs 4 features:

1. An authentication mechanism for **verifying the user's identity**
2. A protection mechanism against buggy user programs that could block other applications running in the system
3. A protection mechanism against malicious user programs that could interfere with or spy on the activity of other users
4. An accounting mechanism that limits the amount of resource units assigned to each user

These 4 features are for cocurrency and independence.

### Kernel 








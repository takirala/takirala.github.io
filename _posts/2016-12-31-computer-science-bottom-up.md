---
title: "Computer Science - Bottom Up"
comments: true
categories:
  - Books
tags:
  - Notes
  - Review
---

Last week, I read this [post](https://news.ycombinator.com/item?id=13249675) on HN. I decided I would give this book a try and it was really fun reading  [Computer Science Bottom Up](https://www.bottomupcs.com/
).

 **Thank you Ian Wienand for a wonderful read!**

There were many areas in the book where one may felt *I knew this before but I never explicitly analysed my thoughts on this*. Some of such moments for me are listed here in random order (with excerpts _copied_ from the book):

* Notion of Everything is a file in UNIX.
* pipe (|) is a fundamental IPC.

  I have always used pipe in bash scripts and made two process communicate with each other several times, but never thought it is a sort of Inter process communication. Wow.

As someone noted in the HN post, the first chapter is named as General UNIX and Advanced C. The second chapter is named as Binary and Number Representation. The author best describes the reason for this [here](https://news.ycombinator.com/item?id=7611874) and it really makes a lot of sense.

* Everything computer knows is boiled down to 1's and 0's
  Google's AlphaGo, Man landing on Moon, An artificial human brain in future.. When you think of it, everything is 1's and 0's behind the scenes.
* Hexadecimal: The only reason this was coined is to make things easy for humans while working with computers! (n.b Base 8 is used for file permission in UNIX )
* Evolution of standards : ANSI C -> C89 -> C99
* GNU C compiler extends a lot of features from the c99 standard. Using flag -std=c99 can show the non compatible features. This is used for the purpose of portability.

One more observation was about the variable data sizes.

* C99 only specifies the minimum size for a variable type.  
E.g: C99 says int is 16 bits minimum. For a 32 bit architecture, 32 bits for an int is the common standard.
* Pointer size is always implementation dependent (32 bits for 32(x86) bit arch, 64 (x64) bits for a 64 bit arch)

C99 realizes that all these rules, sizes and portability concerns can become very confusing very quickly. To help, it provides a series of special types which can specify the exact properties of a variable. These are defined in <stdint.h> and have the form qtypes_t where q is a qualifier, type is the base type, s is the width in bits and t is
an extension so you know you are using the C99 defined types.
So for example uint8_t is an unsigned integer exactly 8 bits wide.  

I have seen this behavior myself before when I was working with huge matrices in numpy. I thought the reason for this could be some huge computation going on in CPU with python's extensive libraries.

    >>> print("This is weird %1.20f"%(8.0+0.45) )
    This is weird 8.44999999999999928946

 The reason for this so clearly explained at the end of the second chapter. I was taken back at the extreme triviality of this issue. I am sure many software engineers out there would be unable to pinpoint the simple reason behind this behavior.

## Computer Architecture

* All Modern processors are **superscalar** (they support pipelining)
* All Modern processors use RISC (Vs CISC)

* Temporal and spatial locality.
 *  Spatial locality suggests that data within blocks is likely to be accessed together.
 * Temporal locality suggests that data that was used recently will likely be used again shortly.

 Benefits are gained by implementing as much quickly accessible memory (temporal) storing small blocks of relevant information (spatial) as practically possible.

* Level vs Edge Trigger interrupts
  Some more clear explanation can be found [here](https://www.quora.com/What-are-the-key-differences-between-edge-triggered-and-level-triggered-interrupts).

When I bought my system, I bought one that has 8 cores. The description read 4 Physical cores and each one has hyper-threading. Although I researched on hyper-threading and how it works, It did not make much sense.
* This book talks about SMP vs SMP with hyper-threading vs NUMA architecture. Hypercube in NUMA architecture is something to be aware of.

## Operating Systems

* POSIX stands for Portable Operating System Interface (X comes form UNIX - from where the standard grew). Once upon a time, the Single UNIX specification and the POSIX Standards were separate entities.

The Single UNIX specification was released by a consortium called the "Open Group", and was freely available as per their requirements. The latest version is the Single Unix Specification Version 3.

The IEEE POSIX standards were released as IEEE Std 1003.[insert various years, revisions here], and were not freely available. The latest version is IEEE 1003.1-2001 and is equivalent to the Single Unix Specification Version 3.

Thus finally the two separate standards were merged into what is known as the Single UNIX Specification Version 3, which is also standardized by the ISO under ISO/IEC 9945:2002. This happened early in 2002. So when people talk about POSIX, SUS3 or ISO/IEC 9945:2002 they all mean the same thing!

* Linux has a monolithic kernel (Vs a micro kernel)
  * Many follow module based architecture. Once the module is loaded on to a privileged kernel, it operates at the same privilege level as that of kernel.
* Different types of virtualization are talked about here. VMWare or virtual box )an application running inside the OS to host a guest OS) Vs the Intel's futuristic support for virtualization.
* Double hash [## operator](http://en.cppreference.com/w/cpp/preprocessor/replace#.23_and_.23.23_operators)
* Great explanation of how a system call happens and the dreaded segmentation fault.  

## Process
* Fork vs Exec :

 Forking provides a way for an existing process to start a new one, but what about the case where the new process is not part of the same program as parent process? This is the case in the shell; when a user starts a command it needs to run in a new process, but it is unrelated to the shell.

 This is where the exec system call comes into play. exec will replace the contents of the currently running process with the information from a program binary.

* clone

  Internally, fork and thread is implemented using clone system call. Thread is, in a way, a _hibrid child_

  Copy on write has a big advantage for exec. Since exec will simply be overwriting all the memory with the new program, actually copying the memory would waste a lot of time. Copy on write saves us actually doing the copy.

  Behind the scenes, **Page tables** are used to implement this.

* O(1) scheduler of LINUX systems.

  Two data structures active and expired are maintained for the processes. Once active structure is empty, the data structures are swapped.

  The really interesting part, however, is how it is decided where in the run queue a process should go. Some of the things that need to be taken into account are the nice level, processor affinity (keeping processes tied to the processor they are running on, since moving a process to another CPU in a SMP system can be an expensive operation) and better support for identifying interactive programs (applications such as a GUI which may spend much time sleeping, waiting for user input, but when the user does get around to interacting with it wants a fast response)

* Modern Operating systems use a one page table per process. Virtual Address translation happens using this table.

* When a process requests a page, TLB is looked up by the processor. If the page is not found, a page fault is raised. OS handles this page fault as :
  * It will try to look up the physical address from page table and save it in TLB.
  * If the address is not found (or) a permission error occurs, **segmentation** fault is raised.

* Translation Lookaside Buffer (TLB) : Dirty and accessed bits are used for flushing. In case of threads, memory sharing is enacted by not flushing.

This was one of the most insightful readings I came across in recent past.

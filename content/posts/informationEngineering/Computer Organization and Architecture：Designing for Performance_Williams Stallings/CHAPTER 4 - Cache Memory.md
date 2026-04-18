---
date: 2025-03-16
draft: false
title: Notes of COADP | Chapter 4 Cache Memory
categories:
  - 计算机组成原理
tags:
  - Cache
  - 存储器层次结构
  - 访问局部性
---
# 4.1 Computer Memory System Overview
## 4.1.1 Characteristics of Memory Systems
### 4.1.1.1 Location
- Internal
	- CPU: register, control memory
	- cache
	- main memory
- External (Secondary): Accessible to CPU via I/O controllers
	- Disk
	- Tape
	- CD
	- DVD
	- ...
### 4.1.1.2 Capacity
For internal memory, this is typically expressed in terms of bytes or words, while external memory capacity is typically expressed in terms of bytes.
> Common word sizes are 8, 16, and 32 bits.

$$\mathrm{capacity}=\mathrm{word\;size}\times\mathrm{number\;of\;words}$$
### 4.1.1.3 Unit of Transfer
For internal memory, the unit of transfer is equal to ***the number of electrical lines*** into and out of the memory module.
> [!NOTE] Classify this 3 concepts
> 1. Word:
> The natual unit of organization of memory.
> 2. Addressable units
> The smallest location that can be uniquely addressed.
> 3. Unit of transfer
> The number of bits read out of or written into memory at a time. For external memory, data rare often transferred in much larger units than a word, and these are referred to as ***blocks***.
### 4.1.1.4 Access Method
1. Sequential access
	1. Start at current location, read through ***in order***
	2. Access time depends on location of data and previous location
	3. e.g. tape, organized into records
2. Direct access
	1. For those individual blocks/records that have unique address, the access process is by ***jumping to vicinity*** plus ***sequential search***
	2. Access time depends on location and previous location
	3. e.g. disk
3. Random access
	1. Each addressable location in memory has a unique, physically wired-in addressing mechanism
	2. Access time is ***independent of*** location or previous access
	3. e.g. RAM
4. Associative
	1. This is a ***random access type*** of memory
	2. Enable one to ***make a comparison*** of desired bit locations within a word for a specified match, and to do this for all words simutaneously.
	3. Access time is independent of location or previous access (same as random access)

> vicinity: n. 附近
> associative: adj. 关联的
### 4.1.1.5 Performance
Three performance parameters are used:
1. Access time (latency): 
	1. ***For random access memory***, this is the time it takes to perform a read or write operation
	2. ***For non random access memory***, this is the time needed to position the read-write mechanism to the disired place
2. Memory cycle time:
	1. $\mathrm{Cycle\;time}=\mathrm{access\;time}+\mathrm{recovery\;time}$
	2. The time is concerned with the system bus, not the processor
3. Transfer rate:
	1. The rate at which data can be transferred into or out of a memory unit
	2. ***For non-random-access memory***, the following equation holds:$$T_n=T_A+\frac{n}{R}$$
	   where
	   $T_n$=Average time to read or write $n$ bits
	   $T_A$=Average access time
	   $n$=Number of bits
	   $R$=Transfer rate, in bits per second (bps)
	3. ***For random-access memory***$$R=\frac{1}{\mathrm{cycle\;time}}$$

> latency: n. 延迟
> mechanism: n. 机制
### 4.1.1.6 Pysical type
- Semiconductor memory
	- RAM
- Magnetic surface memory
	- Disk
	- Tape
- Optical memory
	- CD & DVD
- Magneto-optical memory
	- MO Disk
### 4.1.1.7 Physical characteristics
1. Volatile/Nonvolatile
	1. Volatile: Information decays or is lost when electrical power is switched off
	2. Nonvolatile: No electrical power is needed to retain information (Magnetic-surface memory)
2. Erasable/Nonerasable
	1. Erasable: Can be altered
	2. Nonerasable: Can not be altered, nonerasable memory ***must also be nonvolatile***

> decay: n. 衰减
### 4.1.1.8 Organization
Refer to the physical arrangement of bits to form words.
## 4.1.2 Memory Hierarchy
There are dilemmas in memory design:
- Faster access time - Greater cost per bit
- Greater capacity - Smaller cost per bit
- Greater capacity - Longer access time
To deal with it, memory hierarchy is the way out of these delamma.
A typical hierarchy is illustrated in the following figure.
![](attachments/memory%20hierachy.png)
> hierarchy: n. 等级制度
> cluster: n. 群，组，簇
> fixed: n. 固定的
### 4.1.2.1 Performance of two-level memory
Let's examine an example:
Suppose there were two levels in the memory, Level 1 contains 103 words with an access time of 0.01μs (T1); level 2 contains 105 words with an access time of 0.1μs (T2); hit ratio H.
> H is defined as the fraction of all memory accesses that are ***found in the faster memory***

the figure of Access time vs H is as following:
![](attachments/two-level%20memory.png)
### 4.1.2.2 Locality of reference
- Memory references tend to cluster
	- Over a long period of time, the clusters in use change
	- Over a short period of time, the processor is primarily working with fixed clusters
- Behaviour of programs
	- Sequential execution
	- Few procedures
	- Iterative constructs
	- Arrays or sequences of records
- Spatial locality
	- Tendency of execution to involve a number of memory locations that are clustered
	- Access instructions and data sequentially
- Temporal locality
	- Tendency for a processor to access memory locations that have been used recently
- Possible to organize data such that the percentage of accesses to each level is substantially less than the above level
	- Level 2: All program instructions and data
	- Level 1: Current clusters
> Locality of reference: n. 局部访问性
> spatial: adj. 空间的
> iterative: adj. 反复的
> substantially: adv. 大体上；本质上
# 4.2 Cache memory principles
1. Small amount of fast memory
2. Sits between main memory and CPU
3. Approaching speed of the fastest memory
4. Provide a large memory size at low price
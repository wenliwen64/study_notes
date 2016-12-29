# Reading Notes on Three Easy Pieces of Operating System (question-driven)

## Tips from Midterm:

* Need to check the extra material in html format.
* Also need to check the quiz topics and read related materials. 

## Chapter 32 Common Concurrency Problems

* what are two major classes of non-deadlock bugs? [__atomicity violation__ and __order violation__]
* What is the common way to fix __order violation__ problems? [use condition variables.]

## Deadlock Avoidance

* What is deadlock-avoidance? [Making case-by-case decisions to avoid deadlocks]

* What does reservation means in the context of deadlock-avoidance? []

* How about over-booking? []

* How to deal with rejections of services? [__a.__ log and exit; __b.__keep trying; __c.__return error but continue trying ; __d.__ reduced requested resource use for civic-minded programs]

* How deadlock happens?

   ![](http://i.imgur.com/PGYgEw9.png)

* What are the four conditions to make hold for a deadlock to occur [__a.__ Mutual Exclusion; __b.__ Hold and wait; __c.__ No preemption(locks cannot be forcibly removed from threads that are holding them); __d.__ circular wait ]

* How to prevent __circular wait__? [Set a total ordering on lock acquisition. e.g. L1 always before L2, a specific technique is to use the lock address to enforce lock ordering]

* ?? What is __hold-and-wait__? [incremental allocation of resource may induce deadlock issue. ]

* How to attack __hold-and-wait__ [Make acquiring all locks atomic. Like put lock around the lock acquisition code.  What are the issues? lower the concurrency and you need to know what locks you need to acquire which require knowledge of implementation. ]

* ?? Will context switch happen in between `pthread_mutex_lock(prevention)` and `pthread_mutex_unlock(prevention)` 

* How to attack __No Preemption__ issue? []

* What is the use of `pthread_mutex_trylock(L2)`? what is difference between it and `pthread_mutex_lock(L2)`? [The latter will block if not available , the former will return error code, but if L2 is available, it will grab as `pthread_mutex_lock(L2)` does. ]

* What is __livelock__, compared to __deadlock__ ? [system runs through a certain code sequence again and again but making no progress… Deadlock will not run through code sequence. ]

* Name a solution to solve __livelock__? [add delay to re-loop over the whole thing.]

* What is the weakness of your method? [It needs know the implementation details and release the required resources. ]

* How to eliminate need for __mutual exclusion__? [With help from hardware. ]

* What is difference between __deadlock prevention__ and __deadlock avoidance__ ? []

* How to use Scheduling to avoid deadlock? []

* What is the shortcomings/trade-offs of this kind of scheduling(never schedule threads competing for same lock on one core.)? [performance may be very bad! only useful like in embedded system. ]

* What does __Detect and Recover__ does to deadlock? []

## Health Monitoring and Recovery

* What is a deadlock? []
* How to know if or not system is making progress? [__a.__ have an internal monitoring agent watch message traffic or a transaction log to determine if or not work is continuing. __b.__ have the service send periodic heart-beat message to a health monitoring system. __c.__ have an external health monitoring service send periodic test requests to the service, to see if or not they are correctly responded in a timely fashion. ]
* What does it mean by not receiving a heart-beat from process? [__a.__node failed; __b.__ process failed; __c.__ system gets loaded and message gets delayed; __d.__ network error delay or cancelled  the delivery of the message.]
* What are the issues you need to realize when you do non-disruptive reboots? [__a.__ up-ward compatibility; __b.__ should equipped with _fall-back_ option to return to the previous release.]
* What is __prophylactic reboots__? [restart nodes one at a time to prevent software system from degrading … which might be due to memory leaks or something else. ]
* ​

## Java synchronization mechanism 

* what is happens-before relationship? 

  > Let A and B represent operations performed by a multithreaded process. If A **\*happens-before*** B, then the memory effects of A effectively become visible to the thread performing B before B is performed.

* What is Reentrant Synchronization? [allow itself to reacquire the lock it already owns. ]

## System Performance Measurement 

1. Testing under live loads;
2. Strength and weakness;

## Chapter 33 Event-Based Concurrency

* How to build a concurrent application typically? [Using thread, alternative in server/gui based applications, event-based concurrency.]
* How to receive events? [select() / poll() system calls]
* What is a blocking system call? [It is meaning that you are going to block the progress of the process until the IO or network stuff gets done.]
* Why there is a rule that no blocking calls are allowed in event-based system? [Because if one event handler gets blocked, then the whole system will sit idle, wasting large amount of resources. ]
* What is called asynchronous I/O? [Basically your system call can return immediately and continue doing things until IO gets completed and you can poll or use interrupt to get informed. ]
* What are the issues about the asynchronous IO? [a. multiple core function., b. conflicts with paging, for example, will block the whole system, then no progress can be made. c. hard to manage over time, for example, if one routine gets changed to blocking from non-blocking, then you need to handle it  ]
* Why it is thought to be difficult to integrate the event-based concurrency with other aspect of modern system like paging? [Learn how to speak in OS languages. ]
* Why it is said the event-based system gets control of scheduling itself from OS?  [Don't know?]
* What are two approaches to the same concurrency problem ? [events and threads, considering when u have to do things like keep reading requests and writing things, how can accomplish them without concurrent programs. ]

## Device Drivers: Classes and Services

* What two abstractions represented by device drivers? [a. Generalizing abstractions: use a few general classes like disks and network interfaces, graphics adaptors; b. Simplifying abstractions: implementation of std class interfaces while hiding the details of a particular device]
* Why use OOP for device driver development? [For code reuse.]
* Two major driver classes in old unix systems? [a. block devices. b. character devices]
* What is DMA request? [Direct Memory Access, which allows certrain hardware subsystems to access main system memory independently of CPU.]
* Block devices are random-access devices addressable in fixed size[support _request()_, used in OS, force IO to go through the system buffer cache]
* Character devices are  sequential access, or byte addressable.[support _read()_, _write()_, _seek()_]![](http://i.imgur.com/jsaxy7c.png)
* What is Disk-Kernel Interface and Device Driver Interface(specific interface for this device. )![](http://i.imgur.com/pGiO75x.png)

## Chapter 35.

* What are three pillars of operating system? [Virturalization, Concurrency, Persistence]
* What does persistence mean, name examples? [making information persist, despite computer crashes, disk failure, or power outages]

## Chapter 36. I/O Devices

* How do graphics or other high performance IO devices connect to system? [__Peripheral Component Interconnect(PCI) or its derivatives__]
* What bus are lower level or slow devices(mice, disks) connecting to ? [peripheral bus, like Universal Serial Bus(USB), Serial AT Attachment (SATA), Small Computer System Interface(a bus standard, SCSI)]
* Why we need fast bus and slow bus(hierarchical structure)? [physics(the shorter the faster, so no room for  plug devices), cost(engineering cost)]
* What are two parts in a canonical device? [Interface(Registers of status, command, data, regard them as return value , function and input parameters) and Internals(CPU, DRAM/SRAM, hardware-speicific chips): ]
* What is polling a device? How to avoid the cost? Why interrupt is not always good? If dont know, use what approach? [keep asking if it is available/finished; Interrupt, put device sleep and let hardware issue an interrup which can effectively put CPU to jump to OS at pre-determined ISR, like reading data or just error code from the device and wake up waiting process; Interrupt will slow down system if device if very fast.]
* Programmed IO? (CPU involved in data movement. Making computation and I/O overlaped)
* When interrupts are not bettern than PIO? (cost of handling of interrupts and context switching outweight the benefits; Another one is huge amount of network packets incoming generating initerrupts will overload the CPU and finally make CPU only process these interrrupts and unable to run user processes(livelock); Coalescing )
* What is DMA and why DMA? [DMA = Direct Memeory Access; Because if you let PIO do the copy and transfer work, it is a waste of CPU time, DMA has its own engine and os can only telles him where the data, how large is it and where to move to, when DMA finish its job, it will raise an interrupt and os thus knows the transfer is done. ]
* Two major concerns to incorporate devices into system? [conviences and efficiency. ]
* How the OS actually communicates with devices? [I/O instructions: in/out instruction to assign the port the data goes to; Memory mapped IO: indicates the device register available as location in memory and hardware then routes it to the real place.]
* Device driver? Why ? [the lowest level software in OS that knows everything about the device; ]
* How does device fit into the OS? [Software stack in OS to make os work with devices(from bot to top): device driver(provide protocol-specific r/w)->Generic Block Layer(block r/w)->File System(open read, write, close, etc)->Application ]
* What is the downside of above approach? [too general so some device-specific feature cannot be enjoyed by the rest of the OS]
* Protocol to interact with device? [the rules or procedures you have to follow to get what you want from this device.]



* How should I/O be integrated into systems?        


* What are the general mechanisms?
* How can we make them efficient? [2 ways to make it efficient and communicate]



## Chapter 37. Hard Disk Drive

* What is the interface for the morden hard disk drive? [read/write  512-byte blocks(sector), address space of the drive is from 0 to n - 1, where n is the number of sectors in  this drive]
* What size of write is atomic operation is guranteed by the manufacturer? [512-byte write, write it entirely or nothing at all. But the file system can provide like 4KB size operation.]
* Some reasonable assumptions we can make for the data access in hard drive? [random access worse than continguous access or sequential read/write, adjacent acess is faster than two random blocks ]
* What is rotational delay? What is the seek time? What is transfer?[Rottaional delay is desired sector rotates to head's position. These two combined to be the most expensive operations on disk; either write or read to/from disk through the head.]
* Name a few other designs in hard drive? [track skew, multi-zoned disk drives(each zone has tracks with same number of sectors)]
* What is the use of cache/track buffer on hard disk? [8-16MB, which is used to store all of the sectors on that track and let accessing them become easier. ]
* What are write back and write through? [acknowledge the write operation after writting to its cache or disk. ]
* TODO: computing of the disk access time.
* What is disk scheduler? What is the difference between job scheduler and disk scheduler? Is it serviced one by one or just by set?
* What is SJF(shortest job first)? What strategies do we have to do the scheduling? [__Shortest Seek Time First__, __SCAN__, __Shortest Positioning Time First__]
* What are the advantages and disadvantages for each scheduling policy? [a. SSTF: cons-os dont know the geometry of the disk, but can be fixed by nearest-block first algo, starvation can happen if there is a steady stream coming, request to another track can be starved(fairness); b. SCAN: to conquer fairness issues of SSTF, ]
* What is __Elevator__ or __SCAN__ and __F-SCAN__ and __C-SCAN__ work? [Simply go back forth from outer to inner or inner to outer, service the one when it gets to. __F-SCAN__ is freezing the queue until sweep happens(means it wont schedule if a request come when it is sweeping, so even far-away but early comming requests can be serviced), __C-SCAN__ is just go from outer to inner and again, outer to inner, this can avoid in favor of middle sectors which might be acrossed twice if not circular scan]
* Why __SPTF__? [Because you dont know whether seek time outlarge the rotation time or vice versa. OS dont know for sure, so it is always implemented in drive.]
* Where does disk scheduling happen in morden system? [disk controller has SPTF implemented and good idea what to service first, so os has a guess and send its guess to the disk and let disk make decision. ]
* What is IO merging? [merge contiguous requests, done by os or scheduler. ]

## Chapter 38. Redundant Arrays of Inexpensive Disks (RAIDs)

* What are the criteria to assess a storage system? [Reliability, Capacity, Performance]

* What does it mean by transparancy? Can you name an example how it benefits a new system? Why it is said transparency greatly improves deployability? [Transparency means the new functionality demands no changes to the rest of the system. SCSI-based RAID storage array can enable immediate use like a SCSI disk. Your OS and user application don't need to change a line of code to make original version work. ]

* What are physical IO and logical IO? [These two operations take place on two different software level, the first one takes place on RAID level, the latter takes place on Operating System]

* What does DRAM mean? [Dynamic Random-Access Memory]

* What is fail-stop fault model? [a disk has only two states: working or failed]

* Name three important RAID designs? [RAID Level 0(stripping), RAID Level 1 (mirroring), RAID Level 4/5(parity-based redundncy)]

* What is the advantages/disadvantages of RAID Level 0? [Upper bound of performance(most parallism )/capacity(round robin place information across the disks), low reliability]

* How to determine the chunk size? What are the pros/cons for each strategy? [little chunk(high intra-disk parallelism, high positioning time); large chunk(low intra-file parallelism, low positioning time??)]

* How to assess the performance of different RAID mode? [Considering two metrics: a. single-request latency; b. steady-state throughput of the RAID, total bandwidth of many concurrent requests. (The latter would be the focus in high performance environment. ) ]

* What is the throughput and latency for RAID Level 0? [N\*S and N\*R and latency for a single-block request should be the same for single disk result.]

* What is __RAID Level 1__? []

* What are __RAID 1+0__ and __RAID 0+1__? 

  ![](https://upload.wikimedia.org/wikipedia/commons/e/e6/RAID_10_01.svg)

  ![](https://upload.wikimedia.org/wikipedia/commons/a/ad/RAID_01.svg)

* Assess __RAID Level 1__ ? [Capacity: half the the peak value; Reliability: Tolerate up to N/2 and at least 1 disk failure; Performance: write latency is different since it has two copies to write(but if done parallel, almost equivalent to single disk); throughput(write and read) is N/2 * S, random read access is N * R, random write access is N / 2 * R ]

* What is the use of write-ahead log? [To ensure the atomicity of write operation. ]

* What is __RAID Level 4__? How to assess it? [Using XOR for each bit of blocks on each disk and get the parity block and if one failed, use the remaining blocks to reconstruct the lost one; Capacity: (N-1)\*B, Reliability: (N-1)\*B, Performance: throughput::read: (N-1)\*S mb/s, throughput::write: __small write problem__(bottleneck is the parity disk), R/2 mb/s(read and write like done on single disk) , latency::read single disk, latency::write half the single disk(4 operations in 2 parallel)]

* __RAID 5__? Why? ![](https://upload.wikimedia.org/wikipedia/commons/6/64/RAID_5.svg)

* Summary of RAID Level Assessment: ![](http://i.imgur.com/z2McmeQ.png)

## Chapter 39. Interlude: Files and Directories

* What are the underlying entries behind the virtualization entities process and address space? [CPU and memory]
* API used when interacting with a UNIX file system; What are the two key abstractions for virtualization of storage? [file and directory]
* What is called the inode name? [The file's low level name.]
* What is the difference between a file and a directory? [it contains a list of tuples (user-readable name, low-level name)]
* What is the use of _lseek()_? Will it cause disk seek? [change the next write/read start position, but will not cause any disk head movement. But certainly will cause it when it comes to the upcoming read and write.]
* Inode? [a data structure which keeps the all of the metadata for a file on the disk.]
* Why removing a file is performed via unlink()? [creating a file has two steps: a. create a structure storing metadata on disk, b. link a human name to that file, put the link into a directory; unlink means decrement the reference count by 1 every time you delete a link]
* Why you can't create a hard link to a directory? Why can't to do this to another partition of hard disk? [a. for the fear that you create a cycle in the directory tree; b. only unique within one filesystem, partition means different filesystem ]
* How does fs know how many references are out there? [reference count for each file]
* How many different files types in Unix system? [d, f, l(soft links), it is a file storing the path, longer name = larger size]
* What does _mount()_ do? [paste the new filesystem to the target point on the existing directory tree. ]

## Chapter 40. File System Implementation

* Two aspects you have to consider about building a file system? [__access method__ and __data structure__]
* Typical size of a block( 4KB)
* Diagram for a file system? ![Screen Shot 2016-11-19 at 12.21.10 AM](/Users/lwen/Desktop/Screen Shot 2016-11-19 at 12.21.10 AM.png)
* What is direct pointers? [disk addresses, each pointer referes to one disk block, but if the file that is really big, bigger than block multiplied by the number of direct pointers]
* Is disk byte addressable? [No, only consist of a large number of addressable sectors, usually 512 bytes.]
* What is the typical number of direct pointers? [12]
* What is the shortcoming for single extent file system? [Hard to find contiguous chunk of disk space for a single big file]
* Compare pointer-based and extent-based approaches? [a. more flexible but more metadata; b. less flexible but more compact]
* What approach does ext4 use for disk addressing? [extent-based, not like ext2, ext3]
* Name example file system using linked-based scheme? [FAT: file allocation table.]
* How does a directory data structure look like on disk? ![Screen Shot 2016-11-19 at 10.10.19 AM](/Users/lwen/Desktop/Screen Shot 2016-11-19 at 10.10.19 AM.png)
* Does a directory have a inode? [YES]
* What data structure is used to manage free spaces on disk in vsfs? [bitmap]
* Things happens when creating a new file? [a. search bitmap, b. mark an inode, c. mark bitmap, all these three should be done by file system. ]
* What is the inode number for `/` directory? [No. 2, file system reads this in and traverse the whole structure. ]
* What is open file table?  What does it mean by further update the in-memory open file table for this file descriptor? Update offset? Update last accessed time
* How many IO generated for each write action? [a. read the bitmap, write the bitmap, read and write to inode, and wrtie the actual block itself.]
* create may cost 10 IO operations while the write may cost 5 IOs, these are already a lot!
* What strategies can be used to maintain a fixed-size cache? [LRU, initialized at boot time.]
* What is the advantage of wrtie buffering. [a. batch some updates into a samller set of IOs; b. buffer the writes in memory can make system schedule the subsequent IOs; c. create and delete, then no need to bother the filesystem to make real changes to the disk, fsync() can enforce the immediate write]
* What are the ad/disad for static partitioning and dynamic partitioning

# Chapter 41 Locality and the Fast File System

# Chapter 42 Crash Consistency FSCK and Journaling. 

* Crash-consistency  problem: due to some reason, the system crashed, and some on-disk structure will be left in an inconsistent state. How to deal with this kind of situation.
* Two approaches? [FSCK: file system checker And journaling, aka write-ahead logging. ]
* What is the major problem for fsck? [slow and lost one and search the entire system approach.]
* What is the other name for journaling? [Write ahead logging. ]
* What are physical logging? [Put all of the things into the block.]
* What are the checkpointing? [overwrite the on-disk structure]
* Disk internal schedule may rearrange the order of writing data out to disks. 
* protocol for ext3 update the file system? [journal write, journal commit and check point. ]
* Free journal  block in super-block of journaling. 
* Metadata journaling ? [just write meta data twice instead of data blocks twice also as what data journaling did. protocol is at Page 526]
* ​

# Chapter 43 Log-structred File Systems

* Why build such a log-structred file system? [a. increasing memory size makes write performance critical because read may end up checking the cache in fact; b. gap between sequential and random IO performances; c. poor performance like FFS has on common workload, like update a file may induce large amount of IOs even though most of the blocks are located in the same group; d. RAID-unaware]
* How does LFS write sequentially and effectively? [keep track of the memory updates when the change gets cumulated enough, LFS writes it out to the disk all at once. ]
* Why it is difficult to find an inode on LFS? [Because LFS never overwrites things, so inode is scattering across the whole disk and keeps moving around.but it introduce inode map which just tells you where to find the starting address of a file, and Check point Region. ]
* How does LFS handle garbage collection? [segment by segment, periodically, writes out the live ones and free up the dead ones. ]
* How to determine within a segment, which is live which is dead? [in each segment, the segment summary block is used to do so. ]
* Policy? [cold and hot segment. ]
* How to recover from accident? [old version snapshot.]

# Chapter 44 Data Integrity and Protection

* In early RAID systems, model of failure ? [the whole is working or the entire disk is down. ]
* What are the latent-sector error(LSEs) and block corruption? [LSEs - due to the head crash, a group of sectors has been damaged in some way. ]
* How to recover these errors? [LSEs could  be easily fixed by using RAID-4/RAID-5 or other mirrored RAID to recover or compute the corrupted data. standard redundancy mechanism. ]
* Silent failures via data corruption.? How can we detect this kind of corruption? [checksum, CRC or Fletcher checksum...]
* Variations of checksum layout in hard drive disks? [8 bytes per sector or store multiple blocks in one single block/sector , but this approach performs much poorly demanding two writes. ]
* Misdirected Writes and lost writes? [redundancy on disks solves first mode of error.  checksum again in __ZFS__(Zetta File System)]
* What is disk scrubbing? [Periodically check the checksum of files stored in disks to see if they are corrupted or not. ]
* Overhead of checksumming? [Check P558]

# Chapter 47 Distributed Systems

* The major concern or crux when building a distributed system? [Make it look like never fail even some components of it will fail from time to time]
* Major limitations' causes? [Communication is inherently not reliable, system performance would be very critical, as well as security]
* Why communication is not reliable? [packets get lost, corrupted or just to the destination simply because of a couple of reasons. Like, electrical problems to cause bit flipped, cable, routers. or lack of buffering. ]
* how to deal with communication failures?  Or in other words, how to build a reliable communication layer? [Acknowledgement. work with timeout to resend the messages. but this has its own shortcoming because one message could be sent twice if ack gets lost, so the receiver or the sender should have some mechanism to deal with this issue, like sequence counter, TCP/IP is an example. ]
* How to avoid overwhelming the server? [exponential back-off scheme to set up a timeout. ]
* What is DSM(Distributed Shared Memory)? Why is it not used anymore ? [Failure happens on one machine would end up losing some pages on that machine,  performance which would be largely impacted by communication between machines. ]
* What the hell is  Remote Procedure Call? [Two main components: stub generator and run-time library. ]
* Reliable or unreliable communication protocol to build RPC on top of it? [Unreliable for efficiency. ]
* Issues may need the RPC to handle is ?[timeout: by check server state periodically, large arguments: fragmentation and reassembly, byte-ordering: ]
* When does a normal procedure call happen?[compile time]
* When does RPC happen？[Run-time.]

# Chapter 48 Sun's Network File System(Mainly NFSv2)

* Why bother distributed file system? [a. Data sharing; b.centralized administration(backup data); c. security, ]
* How to build a distributed file system? [a. transparent filesystem to client side, open, read, write, close, mkdir; ]![Screen Shot 2016-11-28 at 2.47.51 PM](/Users/lwen/Desktop/Screen Shot 2016-11-28 at 2.47.51 PM.png)
* Why server crashed? [a. bugs; b. just look like it crashed, due to the disconnection. ]
* Why stateless approach for NFS? [Hard to deal with crash recovery. ]
* File handle components? [a.volume identifier; b. inode number; c. generation number, these three together comprise a unique indentifier informs the server which file system the request refer to(volume identifier), which inode number, generation number is used to reuse an inode number by incrementing it every time it is called. ]
* by incrementing it whenever an inode number
  is reused, the server ensures that a client with an old file handle can’t
  accidentally access the newly-allocated file.????
* Very important figure 48.5GOD's SAKE
* What does close() do? [clean up local data structures, like free descriptor "fd" in open file table. Does it need to call server? Hell no. ]
* What is called idempotent operation? [result of multiple idempotent operation is equal to one operation. ]
* What would happen if a server's reply gets lost? [client would send it again and wait for the reply. ]
* What is the cause of cache consistency problem? [cache, ]
* What are examples of cache consistency problems? [update visibility(not written to center immediately, so other node still gets the old copy), stale cache(maybe some has been updated in the file server,  but you still have stale version in your fucking cache).]
* How to solve them? [a. update visibility=> flush-on-close, ensures the open operation on the other node gets the newest version. b. check before using its cached content. by sending a getattr request., use attribute cache, in which each entry would expire after every 3 seconds.]
* What is the shortcoming of close-on-read? [quicky generated and deleted files may not be needed to be written to file server so this may harm the overall performance.]
* What is the shortcoming of attr cache implementation? [maybe just hard to understand its behavior, sometimes its correct version, sometime it is old version. ]
* What is the major performance bottleneck of NFS server? [write performance, because server will send back success only after committing the changes to storage. So solution could be use battery backed memory to hold the change and send back quickly the success message. or use a filesystem which is designed to write to disk quickly when one finally needs to do so. ]
* What is the philosophy of NFS? [simple and fast crash recovery. ]

# Chapter 49 The Andrew File System(AFS)

* Why NFS is limited by its scalability? [Because the frequent check for the cache validation may limit the number of clients a server can respond to.]
* How to deal with cache consistency in AFS? [Every time an application open a file, it is in its latest version.]
* One of the basic principle of all versions of AFS is what ? [whole-file caching]
* In AFSv1, how does it improve its performance after first access to a file? [ask if it has been changed, if not, will use locally copied version.]
* Problems with first version of AFSv1? [a. Too high costs in Path-traversal b. The client issues too many TestAuth protocol messages to test if that file is already modified or not. ]
* What is callback? Why? [a. A promise from the server to the client that the server will inform the client when a file that the client is caching has been modified. No need for client to contact server any more. ]
* Wha tis FID， file identifier? [volume identifier, file identifier, and a uniquifier. no need to traverse path name every single time????![Screen Shot 2016-11-29 at 1.11.15 AM](/Users/lwen/Desktop/Screen Shot 2016-11-29 at 1.11.15 AM.png)]
* When will file server update the file? [when flush back to file when a close() is issued. But on the same machine, it can immediately see the changes.]
* Wha tis last writer wins? [or last close wins]
* Why server crash is a big event? [callbacks are stored in memory, so when rebooted, no idea which client has which file, so solution could be heartbeat messages or broadcast the invalid messages to clients. ]
* Very very important comparison between __NFS__ and __AFS__ in this chapter, worthy of second reading!!!!
* What kind of workload is not welcome in AFS? [sequential accessed or random updates]
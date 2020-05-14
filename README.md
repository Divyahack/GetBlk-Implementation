# GetBlk-Implementation
code for emulating Get Block Algorithm / Buffer Cache .
Using MultiThreading , Mutex Locks , Conditional Variable.

Programming Language : C++
Concepts used : AOS multiprocessing , signal Handling , Buffer cache Implementation.

Buffer Cache: 
    1. Each buffer header is a data structure  which is used to store the information for the physical buffer it represents. 
    2. The kernel maintains a free buffer list .
    3. The kernel maintains the buffer Hash Queues through an array of doubly linked lists of buffer headers, each with a hash queue header        marking the beginning and the end of the list of the hashed buffer headers. 
    4. The buffers on the hash queues usually contain valid data. 
       When they are used by the kernel, the kernel locks them. 
       When they are not in use, the kernel unlocks them.
    5. When the buffers on the hash queues are no longer locked, they become free but are not removed from the hash queues. The kernel            simply puts the buffers back to the free list.
    6. If the data in the buffer is still valid, it puts the buffer at the tail of the free list so that its contents will not be replaced        very soon.
    7. If the buffer contains invalid data, it will be placed at the front of the free list.
    8. If the kernel finds the buffer on the hash queue, it checks whether the data is valid and whether the buffer is free. 
       If the data is valid and the buffer is free, it simply removes the buffer from the free list.
    9. The kernel then finds the data it is searching for. If the kernel wants to write data to the buffer, it then just marks the buffer          busy and starts writing the data to the buffer. 
   10. If the kernel does not find the buffer for needed data in the hash queue, it allocates a free buffer from the beginning of the free        list, puts it on the correct hash queue then reads or writes data to it.

# Heap-Allocation
Designed heap allocator that explored the balance of correctness of well-formed requests, tight utilization with low memory, and service request speed from scratch.

**Two design decisions** I made were my struct representation of a block and the way I chose to order my free list:

(1) My node struct consists of a hdr block_header, hdr *prev, hdr *next (hdr is a typedef of
size_t). I chose this for ease of casting. Intuitively, I can cast a void * to a node *
and can immediately set all the needed values, header, prev, and next. Secondly, I would
search for free blocks by traversing my free list, and when a new block became available,
it would be added to the front of the free list as opposed to ordering my address.

(2) An additional design decision was that I rarely used void * for code readability, since I found my
node structure very intuitive and minimum payloads were never smaller than 16. 

**On the strength front**, my allocator shows very strong performance when reallocating the same
block due a large amount of times due to the successful implementation of in-place realloc. It
shows utilization of approximately 50% higher since it can move into adjacent spots as opposed
to purely moving the allocation block. My allocator shows weaker performance when a pattern
of allocating a block cannot be split with its remaining payload. When the remainder of payload
is less than 16 (after factoring out the header required space), a new block cannot be created,
so that utilization of the heap is wasted, creating some fragmentation. Lastly, ways I optimize
my code was creating variables from operations called multiple times like payload arithmetic,
etc, and I found ways to condense different loops into one loop block to optimize speed.
I also changed my flags. 


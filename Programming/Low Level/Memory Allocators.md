Applying different allocation strategies to different parts of a program reduces the amount of information the programmer has to care about, reduces memory leaks and use after frees if done right. It can also potentially improve performance by reducing sporadic memory allocations. 

Some of the most common allocation strategies are:

- **Pool Allocator** stores a bunch of objects with the same size and lifetime. They will all be deallocated at the same time.
- **Arena Allocator** allocates a bunch of memory, then "allocations" can be made for objects with the same lifetime constraints and of any size into this backing buffer. They will all be deallocated at the same time.
- **Free List Allocator** is a more general purpose allocator that has no lifetime or size constraint. It can be implemented with a linked list or a red black tree, it's more commonly a red black tree. The deallocation happens separately for every object.

Apart from these "primitive" allocator types, there's other allocators that attempt to be more general purpose while being reasonably fast, potentially using a mix of these approaches. These allocators will also have to care about fragmentation, since the more entropy there is in the system, more time will be taken trying to find a fitting spot for the object being allocated, and if no spot is found, an expensive system call will have to be made. 

Nina Zakharenko - Memory Management in Python - The Basics - PyCon 2016
source: https://www.slideshare.net/nnja/memory-management-in-python-the-basics

The following information is for CPython implementation of Python, you can check the implementation of python as follows

```python
>>> import platform
>>> print(platform.python_imlplementation())
CPython
```

![image](https://user-images.githubusercontent.com/19663316/141606934-9d2db520-ec4a-4825-8309-00e66a90b820.png)

![image](https://user-images.githubusercontent.com/19663316/141606941-dcc854b4-3bdc-417a-a301-cf0e2ba8a5bc.png)

![image](https://user-images.githubusercontent.com/19663316/141606955-8e9384da-606d-4da6-a600-d83d79db4bad.png)

![image](https://user-images.githubusercontent.com/19663316/141606964-ff0d7638-b924-4508-ba36-f42c9ac9bb34.png)

![image](https://user-images.githubusercontent.com/19663316/141606969-8023b5f5-c250-4023-b68c-2dd9a93e1c51.png)

![image](https://user-images.githubusercontent.com/19663316/141606977-fa1457b9-ba1a-4650-a498-99a2d1d5e2ee.png)

![image](https://user-images.githubusercontent.com/19663316/141606985-fd551d4a-fa34-4abc-9a89-a84137990ba5.png)

```python
>>> import sys
>>> a = 'my-string'
>>> sys.getrefcount(a)
2
```

Notice that there are two references to our variable a. One is from creating the variable. The second is when we pass the variable a to the sys.getrefcount() function.

```python
>>> import sys
>>> a = 'my-string'
>>> b = [a] # Make a list with a as an element.
>>> c = { 'key': a } # Create a dictionary with a as one of the values.
>>> sys.getrefcount(a)
4
```

There are a few ways to increase the reference count for an object, such as 

* Assigning an object to a variable.
* Adding an object to a data structure, such as appending to a list or adding as a property on a class instance.
* Passing the object as an argument to a function.

![image](https://user-images.githubusercontent.com/19663316/141606994-d0a96cbd-467a-4b78-af37-a41b3963ef51.png)

![image](https://user-images.githubusercontent.com/19663316/141607008-292ec6c7-b57c-46e8-b955-7c466fd73535.png)

![image](https://user-images.githubusercontent.com/19663316/141607025-c68758b0-b1cb-4c6e-8867-f0526bf06bb5.png)

![image](https://user-images.githubusercontent.com/19663316/141607018-31f0b176-0762-4044-88e0-4308f9df9a4f.png)

![image](https://user-images.githubusercontent.com/19663316/141607049-0d983eaa-873c-46a3-9352-b0d3ca1b80a1.png)

![image](https://user-images.githubusercontent.com/19663316/141607058-98419b2f-cf0d-4d08-a5f7-56bd73448855.png)

## Garbage collection

![image](https://user-images.githubusercontent.com/19663316/141607072-9c8b9a61-fd1b-4dd9-9b6b-2e823e2c1038.png)

![image](https://user-images.githubusercontent.com/19663316/141607083-2e8829fe-52bb-4f8a-a483-0cfd8355700f.png)

![image](https://user-images.githubusercontent.com/19663316/141607088-d7ac4fed-9993-4856-b68c-475cdcbdb021.png)

![image](https://user-images.githubusercontent.com/19663316/141607103-700a17d9-adef-437b-928a-c600fb550af4.png)

![image](https://user-images.githubusercontent.com/19663316/141607119-e3cc0675-ca24-4c6a-b951-3d0d6b0a734b.png)

![image](https://user-images.githubusercontent.com/19663316/141607130-be71c350-b3e5-4024-a3a5-3403b66d0e0d.png)

![image](https://user-images.githubusercontent.com/19663316/141607141-a9006ed4-5ea1-433a-9cae-6270b701ba99.png)

![image](https://user-images.githubusercontent.com/19663316/141607148-6b13cab1-b887-455a-a509-b8222709ced4.png)

![image](https://user-images.githubusercontent.com/19663316/141607169-80803fd3-a390-4acf-9159-d24da2aada5a.png)

![image](https://user-images.githubusercontent.com/19663316/141607189-267c7b10-b2b9-4e3c-9b68-4e673a8cbe43.png)

![image](https://user-images.githubusercontent.com/19663316/141607199-ac2a2748-5af8-4f17-b48f-de4abda4798f.png)

![image](https://user-images.githubusercontent.com/19663316/141607235-0c9fe860-f4a9-46ba-be2b-4186b1d241eb.png)

![image](https://user-images.githubusercontent.com/19663316/141607219-34777022-a18f-43ae-9444-c218d89f1c18.png)

![image](https://user-images.githubusercontent.com/19663316/141607209-4ed6f83d-1878-4b17-bf59-54ef3eec8cc4.png)

![image](https://user-images.githubusercontent.com/19663316/141607274-eef544ac-b518-4639-a4d1-69fb4b9fb810.png)

![image](https://user-images.githubusercontent.com/19663316/141607264-2d4e20a1-8882-4dc2-93b9-4f915f0c4f87.png)

![image](https://user-images.githubusercontent.com/19663316/141607289-bfc0bf88-f069-4100-a5ea-9c38ddaedf3f.png)

![image](https://user-images.githubusercontent.com/19663316/141607294-288cbe40-3245-4309-b783-fa0b951657d4.png)

![image](https://user-images.githubusercontent.com/19663316/141607305-14728b8c-ec1a-4138-a751-c8ce095ff505.png)

There are two key concepts to understand with the generational garbage collector.

* The first concept is that of a generation.
* The second key concept is the threshold. 

The garbage collector is keeping track of all objects in memory. A new object starts its life in the first generation of the garbage collector. If Python executes a garbage collection process on a generation and an object survives, it moves up into a second, older generation. The Python garbage collector has three generations in total, and an object moves into an older generation whenever it survives a garbage collection process on its current generation.

For each generation, the garbage collector module has a threshold number of objects. If the number of objects exceeds that threshold, the garbage collector will trigger a collection process. For any objects that survive that process, they’re moved into an older generation.

Unlike the reference counting mechanism, you may change the behavior of the generational garbage collector in your Python program. This includes changing the thresholds for triggering a garbage collection process in your code. Additionally, you can manually trigger a garbage collection process, or disable the garbage collection process altogether.

```python
>>> import gc
>>> gc.get_threshold()
(700, 10, 10)
```

By default, Python has a threshold of 700 for the youngest generation and 10 for each of the two older generations.

You can check the number of objects in each of your generations with the get_count() method:

```python
>>> import gc
>>> gc.get_count()
(596, 2, 1)
```

As you can see, Python creates a number of objects by default before you even start executing your program. You can trigger a manual garbage collection process by using the gc.collect() method:

```python
>>> gc.get_count()
(595, 2, 1)
>>> gc.collect()
577
>>> gc.get_count()
(18, 0, 0)
```

Running a garbage collection process cleans up a huge amount of objects—there are 577 objects in the first generation and three more in the older generations.

You can alter the thresholds for triggering garbage collection by using the set_threshold() method in the gc module:

```python
>>> import gc
>>> gc.get_threshold()
(700, 10, 10)
>>> gc.set_threshold(1000, 15, 15)
>>> gc.get_threshold()
(1000, 15, 15)
```

**General rule: Don’t change garbage collector behavior**

## `__slots__`

![image](https://user-images.githubusercontent.com/19663316/141607340-6d398b61-d732-4b50-91e3-4c866ef05232.png)

![image](https://user-images.githubusercontent.com/19663316/141607353-b0fd263e-c5f5-40c4-99f1-7a2087f9d71a.png)

![image](https://user-images.githubusercontent.com/19663316/141607359-1d373f60-daab-441e-beed-996c3b7745a4.png)

![image](https://user-images.githubusercontent.com/19663316/141607366-a53cd87e-b5af-40fe-8fa0-f408ec53c873.png)

![image](https://user-images.githubusercontent.com/19663316/141607331-c04d64e3-3329-4452-8ddf-fe69415b2ebd.png)

## GIL

![image](https://user-images.githubusercontent.com/19663316/141607431-8a99417c-88a4-4b8a-a3b3-4858c1281f17.png)

![image](https://user-images.githubusercontent.com/19663316/141607456-a56b3c3e-1cf2-4ea7-b74c-89c63bab7c2b.png)

![image](https://user-images.githubusercontent.com/19663316/141607428-854f85e2-a957-4ac0-a86f-9724fcdfdb71.png)

![image](https://user-images.githubusercontent.com/19663316/141607460-b12ef94a-8cc0-451b-abec-e7e29c27c507.png)

![image](https://user-images.githubusercontent.com/19663316/141607466-34367ad0-fa69-4d22-a3bb-05a4061bafd2.png)

![image](https://user-images.githubusercontent.com/19663316/141607479-d53d6c0a-8a45-47d4-b8b5-5ccfbadf9781.png)


## Memory management in Python

Everything in Python is an object. Some objects can hold other objects, such as lists, tuples, dicts, classes, etc. Because of dynamic Python's nature, such an approach requires a lot of small memory allocations. To speed-up memory operations and reduce fragmentation Python uses a special manager on top of the general-purpose allocator, called PyMalloc.

We can depict the whole system as a set of hierarchical layers:

![image](https://user-images.githubusercontent.com/19663316/141608079-6a672939-d73b-40d2-acc6-0fea0a8556a4.png)

source: https://github.com/python/cpython/blob/ad051cbce1360ad3055a048506c09bc2a5442474/Objects/obmalloc.c#L534 and https://rushter.com/blog/python-memory-managment/

### Small object allocation

To reduce overhead for small objects (less than 512 bytes) Python sub-allocates big blocks of memory. Larger objects are routed to standard C allocator. Small object allocator uses three levels of abstraction — arena, pool, and block.

Let's start with the smallest structure — block.

#### Block
Block is a chunk of memory of a certain size. Each block can keep only one Python object of a fixed size. The size of the block can vary from 8 to 512 bytes and must be a multiple of eight (i.e., use 8-byte alignment). For convenience, such blocks are grouped in 64 size classes.

![image](https://user-images.githubusercontent.com/19663316/141608436-4e6dbce0-9eb3-4371-b79d-91119cc4b9d0.png)

#### Pool

A collection of blocks of the same size is called a pool. Normally, the size of the pool is equal to the size of a memory page, i.e., 4Kb. Limiting pool to the fixed size of blocks helps with fragmentation. If an object gets destroyed, the memory manager can fill this space with a new object of the same size.

Each pool has a special header structure, which is defined as follows:

```c
/* Pool for small blocks. */
struct pool_header {
    union { block *_padding;
            uint count; } ref;          /* number of allocated blocks    */
    block *freeblock;                   /* pool's free list head         */
    struct pool_header *nextpool;       /* next pool of this size class  */
    struct pool_header *prevpool;       /* previous pool       ""        */
    uint arenaindex;                    /* index into arenas of base adr */
    uint szidx;                         /* block size class index        */
    uint nextoffset;                    /* bytes to virgin block         */
    uint maxnextoffset;                 /* largest valid nextoffset      */
};
```

Pools of the same sized blocks are linked together using doubly linked list (the `nextpool` and `prevpool` fields). The `szidx` field keeps the size class index, whereas `ref.count` keeps the number of used blocks. The `arenaindex` stores the number of an arena in which Pool was created.

The freeblock field is described as follows:

```
Blocks within pools are again carved out as needed.  pool->freeblock points to
the start of a singly-linked list of free blocks within the pool.  When a
block is freed, it's inserted at the front of its pool's freeblock list.  Note
that the available blocks in a pool are *not* linked all together when a pool
is initialized.  Instead only "the first two" (lowest addresses) blocks are
set up, returning the first such block, and setting pool->freeblock to a
one-block list holding the second such block.  This is consistent with that
pymalloc strives at all levels (arena, pool, and block) never to touch a piece
of memory until it's actually needed.

So long as a pool is in the used state, we're certain there *is* a block
available for allocating, and pool->freeblock is not NULL.  If pool->freeblock
points to the end of the free list before we've carved the entire pool into
blocks, that means we simply haven't yet gotten to one of the higher-address
blocks.  The offset from the pool_header to the start of "the next" virgin
block is stored in the pool_header nextoffset member, and the largest value
of nextoffset that makes sense is stored in the maxnextoffset member when a
pool is initialized.  All the blocks in a pool have been passed out at least
once when and only when nextoffset > maxnextoffset.
```

Therefore, If a block is empty instead of an object, it stores an address of the next empty block. This trick saves a lot of memory and computation.

Each pool has three states:

* used — partially used, neither empty nor full
* full — all the pool's blocks are currently allocated
* empty — all the pool's blocks are currently available for allocation

In order to efficiently manage pools Python uses an additional array called usedpools. It stores pointers to the pools grouped by class. As we already know, all pools of the same block size are linked together. To iterate over them, we just need to know the start of the list. If there are no pools of such size, then a new pool will be created on the first memory request.

![image](https://user-images.githubusercontent.com/19663316/141608539-850445c0-e6e4-4a81-8685-602c5c2c58b1.png)

Note that pools and blocks are not allocating memory directly, instead, they are using already allocated space from arenas.

### Arena

The arena is a chunk of 256kB memory allocated on the heap, which provides memory for 64 pools.

![image](https://user-images.githubusercontent.com/19663316/141608554-995fe69a-7352-4d5b-a052-8745259951f2.png)

The structure of arena object looks as follows:

```c
struct arena_object {
    uintptr_t address;
    block* pool_address;
    uint nfreepools;
    uint ntotalpools;
    struct pool_header* freepools;
    struct arena_object* nextarena;
    struct arena_object* prevarena;
};
```

All arenas are linked using doubly linked list (the `nextarena` and `prevarena` fields), it helps to manage them. The `ntotalpools` and `nfreepools` are storing information about currently available pools.

The `freepools` field points to the linked list of available pools.

There is nothing complicated in the implementation of the arena. Think of it as a list of containers, which automatically allocates new memory for pools when needed.

### Memory deallocation
Python's small object manager rarely returns memory back to the Operating System.

An arena gets fully released If and only if all the pools in it are empty. For example, it can happen when you use a lot of temporary objects in a short period of time.

Speaking of long-running Python processes, they may hold a lot of unused memory because of this behavior.

#### Allocation statistics
You can get allocations statistics by calling `sys._debugmallocstats()`.
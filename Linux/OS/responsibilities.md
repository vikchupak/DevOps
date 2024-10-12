- Processor (and Processes) Management
- Memory Management
- Input/Output Devices Management
- File System Management
- Security Management (user space/scopes, permissions, passwords, firewall)

# Processor vs Processes Management

### Processor (CPU) Management (Hardware resource)
- **CPU scheduling**: The OS uses various scheduling algorithms (e.g., Round Robin, Priority Scheduling) to decide which process should get CPU time at any given moment.
- **Context switching**: When switching between processes, the OS saves the current process’s state and loads the next one’s state. This allows multiple processes to share the CPU.
- **Handling multiple CPUs**: In systems with multiple processors or cores, the OS allocates tasks across them to balance the load, improving performance and efficiency.
- **Managing CPU affinity and priorities**: The OS may assign certain processes to specific CPU cores to optimize performance, especially in multi-core systems.

### Processes Management (Software units)
- **Creating processes**: When you start a program, the OS creates a new process and allocates necessary resources like memory and file handles.
- **Managing process states**: Processes go through various states (e.g., running, waiting, terminated), and the OS tracks and manages these states.
- **Synchronizing processes**: When multiple processes need to interact (like sharing data), the OS ensures they are properly synchronized to prevent race conditions or deadlocks.
- **Terminating processes**: Once a process completes its task or needs to be closed, the OS deallocates its resources and removes it from the system.

### Key Differences
| **Aspect**               | **Process Management**                                   | **Processor Management**                                |
|--------------------------|----------------------------------------------------------|---------------------------------------------------------|
| **Focus**                 | Managing individual processes and their execution        | Managing how the CPU is allocated to processes           |
| **Main Concern**          | The lifecycle, states, and resource allocation of processes| Efficient CPU utilization and task scheduling            |
| **Examples of Tasks**     | Process creation, termination, IPC, synchronization      | CPU scheduling, context switching, load balancing        |
| **Resource Managed**      | Processes (software units)                              | Processor (hardware resource)                            |

### Relationship Between the Two
While **process management** and **processor management** are distinct, they are closely linked:
- **Process management** ensures that processes are created, managed, and terminated effectively, while **processor management** ensures that the CPU is shared among these processes in a fair and efficient manner.
- When the OS manages processes, it needs the CPU to run them. The OS schedules the CPU (processor management) to execute processes (process management).
- Both are essential for **multitasking** and **multiprocessing** environments, where multiple processes are running concurrently and need to share the CPU without conflicts.

### Conclusion
While **process management** and **processor management** both deal with running programs on a computer, they focus on different levels of the system:
- **Process management** handles the software side of things—managing the individual programs (processes) that are running on the system.
- **Processor management** focuses on the hardware side—deciding how the physical CPU is shared among the processes.

# Memory Management

**Memory management** is the process by which the OS controls and coordinates computer memory, assigning portions of memory to various running processes, managing their use, and freeing up memory when it's no longer needed.

### Key Objectives of Memory Management:
1. **Efficient Memory Allocation**: Ensuring that memory is used optimally by allocating enough memory to each process and minimizing wastage.
2. **Protection**: Preventing processes from accessing each other's memory space, which could lead to system instability or security vulnerabilities.
3. **Sharing**: Allowing processes to share memory when necessary, particularly in cases of shared libraries or inter-process communication.
4. **Virtual Memory Management**: Extending the system's memory by using disk space as additional memory when physical RAM is insufficient.
5. **Swapping**: Managing how processes are moved between physical memory and disk to free up RAM for other tasks.

### Main Functions of Memory Management

#### 1. **Process Address Space Management**
Each process in an OS has its own **address space** — a range of memory addresses it can use. The OS manages this by:
- **Allocating memory** when a process is created.
- **Deallocating memory** when the process is terminated or no longer needs certain resources.
- **Tracking memory usage** to ensure that no process exceeds its allotted space or encroaches on another process's space.

#### 2. **Memory Allocation**
There are two main types of memory allocation:
- **Static (fixed) Allocation**: Memory is allocated to a process before execution starts and does not change during its lifetime. This is less flexible and can lead to inefficient memory use.
- **Dynamic Allocation**: Memory is allocated to a process as it needs it during execution. This is more efficient as memory is assigned as required, but it’s also more complex to manage.

There are also several strategies for allocating memory:
- **Contiguous Allocation**: Each process is given a single continuous block of memory, making memory management simpler but can lead to fragmentation.
- **Non-contiguous Allocation**: Processes can be allocated non-contiguous blocks of memory, which allows for more efficient memory use but adds complexity in tracking which blocks are allocated and free.

#### 3. **Paging and Segmentation**
These are two techniques to allow non-contiguous memory allocation and manage larger address spaces.

- **Paging**: The OS divides memory into fixed-size units called **pages** (for processes) and **frames** (for physical memory). Pages can be mapped to any available memory frame, allowing processes to use non-contiguous memory locations. Paging helps reduce fragmentation and enables the use of **virtual memory**.
    - The OS maintains a **page table** that maps pages of a process to frames in physical memory.
  
- **Segmentation**: Memory is divided into variable-sized segments, each representing a logical unit like a function, array, or data structure. Unlike paging, segmentation reflects the logical structure of a program. A segment table is used to map segments to memory locations.

Both techniques can also be combined to use the benefits of both in modern systems.

#### 4. **Virtual Memory**
**Virtual memory** is one of the most important aspects of modern memory management. It allows the OS to use disk space as an extension of physical RAM, enabling the system to run processes that require more memory than is physically available.

- Virtual memory creates an abstraction where processes think they have a large contiguous block of memory to work with, even if the actual memory is spread out across RAM and disk (in pages).
- The OS swaps pages between **RAM** and a special disk area known as **swap space** or a **pagefile** when physical memory becomes full.
- **Page fault**: When a process requests a page that isn’t currently in RAM, a **page fault** occurs, and the OS must load the page from disk.

#### 5. **Swapping**
Swapping is the process where an entire process is moved between RAM and disk to free up physical memory for other tasks.
- **Context switching**: When processes are swapped in and out of memory, the OS must save the process state, which can introduce some overhead.
- **Thrashing**: This is when excessive swapping occurs, slowing down the system due to constant data being swapped in and out of memory. It usually happens when the system is overloaded with too many processes competing for limited RAM.

#### 6. **Memory Protection**
The OS protects the memory of one process from being accessed by another process. This is achieved through:
- **Base and limit registers**: These registers store the base (starting address) and limit (ending address) of the allocated memory for each process. The OS ensures that the process stays within its allocated range.
- **Access rights**: The OS assigns access rights (read, write, execute) to specific regions of memory. For example, a process might be allowed to read from a region but not write to it.

#### 7. **Fragmentation**
Memory fragmentation occurs when free memory is scattered across small, non-contiguous blocks, making it difficult to allocate large chunks of memory even though there is sufficient total free space.

- **External Fragmentation**: Occurs when free memory is divided into small blocks, making it difficult to allocate contiguous memory for new processes.
- **Internal Fragmentation**: Happens when allocated memory blocks are larger than the process requires, leading to wasted memory space within allocated regions.

The OS tries to minimize fragmentation using techniques like **compaction** (moving processes to combine free memory into larger blocks) and **paging** (breaking memory into small, fixed-size units).

### Summary:
Memory management is a critical function of the OS that ensures efficient use of RAM, prevents processes from interfering with each other, and allows processes to run even when physical memory is limited. The OS handles allocation and deallocation of memory, manages virtual memory, and ensures memory protection and isolation between processes. It also employs techniques to minimize fragmentation and efficiently allocate memory space.

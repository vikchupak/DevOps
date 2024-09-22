# With bare-metal, is RAM "reserved" for each guest OS or is there some resource sharing?

In a **bare-metal hypervisor** (also known as a **Type 1 hypervisor**), **RAM** can be either **reserved** for each guest OS or **shared dynamically** depending on the hypervisor’s capabilities and configuration. Here’s how it works:

### 1. **Reserved Memory Allocation** (Static):
   - In many cases, RAM is **statically reserved** for each virtual machine (VM) when it is created or started.
   - The hypervisor allocates a **fixed amount of RAM** to the guest OS, and that memory is **exclusively** used by that guest for as long as it is running. Other VMs cannot use this memory, even if the guest is not actively using all of it.
   - This method provides **predictability** and ensures that each VM has the resources it needs, but it can lead to inefficiency if VMs don’t fully utilize their allocated memory.

### 2. **Dynamic Memory Allocation** (Overcommitting or Sharing):
   - Many modern hypervisors, such as **VMware ESXi**, **Hyper-V**, and **KVM**, support **dynamic memory allocation** or **memory overcommitment**.
   - In this scenario, the hypervisor can allocate **more virtual memory to the VMs than the physical memory available**. It dynamically adjusts the amount of RAM available to each guest OS based on **actual usage**.
   - This allows for **resource sharing**: VMs that are not actively using all their allocated RAM can have their unused memory made available to other VMs that need more.
   - **Hypervisors manage memory sharing** techniques, such as:
     - **Ballooning**: A technique where the hypervisor reclaims memory from a VM that isn’t using all of its allocated RAM and reallocates it to another VM that needs it.
     - **Transparent Page Sharing (TPS)**: In some hypervisors, duplicate memory pages (used by multiple VMs) are shared between VMs, reducing the total physical memory used.

### 3. **Memory Management Techniques**:
   - **Hyper-V Dynamic Memory**: In Hyper-V, dynamic memory allows a VM to start with a minimum amount of RAM and grow or shrink based on its needs. This allows better memory utilization across multiple VMs.
   - **VMware ESXi**: VMware allows **memory overcommitment**, where more virtual memory is assigned than physical memory is available, thanks to techniques like **TPS** (Transparent Page Sharing) and **ballooning**.

### Summary:
- In a **bare-metal hypervisor**, **RAM can be reserved** (static allocation) or **dynamically shared** (dynamic allocation) among guest OSs, depending on the hypervisor's settings.
- **Dynamic sharing** allows for **better utilization** of memory resources through techniques like ballooning and page sharing, while **reserved memory** guarantees that each guest gets a fixed amount of RAM but may lead to inefficient use of memory.

Most modern hypervisors use a combination of both approaches to optimize performance and resource usage based on the workload and system demands.

# How about CPU?

For **CPU allocation** in a **bare-metal hypervisor** (Type 1 hypervisor), the approach is somewhat similar to how RAM is managed. There are two main strategies for handling CPU resources: **dedicated (reserved)** CPU allocation and **shared (dynamic)** CPU allocation. Here's how CPU management works in a virtualized environment:

### 1. **Dedicated (Reserved) CPU Allocation**:
   - Some hypervisors allow you to **reserve physical CPU cores** (vCPUs) for each virtual machine (VM). In this case, the VM is guaranteed a certain number of CPU cycles, and no other VM can use those specific CPU resources.
   - This method ensures **consistent performance**, especially for workloads that are sensitive to CPU latency or require guaranteed compute power. However, it can lead to underutilization if the VM is not fully using the allocated CPU resources.
   - In this setup, the **physical CPU resources** (or cores) are **strictly mapped** to virtual CPUs (vCPUs) that the VM sees, and the VM gets exclusive access to those cores.

### 2. **Shared (Dynamic) CPU Allocation**:
   - In most modern hypervisors, **CPU sharing** is common, where multiple VMs can share the same physical CPU cores. This allows for **overcommitting**, where more virtual CPUs (vCPUs) are assigned across VMs than the actual number of physical CPU cores.
   - The hypervisor schedules **CPU time slices** for each VM based on their needs and prioritization. The physical cores are time-shared between VMs, allowing more efficient use of the available CPU resources.
   - This technique can lead to slight variations in performance for VMs, especially if many VMs compete for CPU cycles. However, for many workloads, this is sufficient and results in better overall resource utilization.

### 3. **CPU Overcommitment**:
   - Similar to memory overcommitment, many hypervisors (e.g., **VMware ESXi**, **KVM**, **Hyper-V**) allow you to allocate more vCPUs to VMs than there are physical CPU cores available. This is possible because the hypervisor can **dynamically schedule** the CPU resources to VMs as needed.
   - **Overcommitting** can lead to more efficient resource usage, but if too many VMs are active at the same time, it can cause **CPU contention**, where VMs must wait for available CPU cycles, potentially leading to performance degradation.
   - To mitigate this, hypervisors implement features such as **CPU prioritization**, where some VMs are given higher priority for CPU resources than others.

### 4. **CPU Management Techniques**:
   - **CPU Pinning**: Some hypervisors allow **CPU pinning**, where a VM’s virtual CPUs are mapped directly to specific physical cores. This ensures that a VM always runs on the same physical cores, which can be useful for latency-sensitive applications, but reduces flexibility in resource allocation.
   - **CPU Limits, Reservations, and Shares**: 
     - **Reservations** ensure a VM gets a guaranteed minimum amount of CPU time.
     - **Limits** cap the maximum CPU resources a VM can use.
     - **Shares** define the relative importance of VMs, so in times of contention, the hypervisor knows how to distribute CPU cycles.

### 5. **Hyper-Threading and Virtual CPUs**:
   - If the host’s CPU has **Hyper-Threading** enabled, each physical core will appear as two **logical cores** to the hypervisor. The hypervisor can then allocate these **logical cores** to VMs as **vCPUs**.
   - The hypervisor will decide how to assign these logical cores, and it can either allocate **full physical cores** or **Hyper-Threaded logical cores** to the VMs, depending on the VM's configuration and the host's available resources.

### Summary:
- **CPU allocation** in a bare-metal hypervisor can be either **dedicated** (reserved) or **shared** (dynamic), much like memory.
- In **dedicated CPU allocation**, physical cores are reserved for a VM, ensuring consistent performance but possibly leading to underutilization.
- In **shared CPU allocation**, multiple VMs share the physical cores, and the hypervisor schedules CPU time for each VM, allowing better overall utilization but with the potential for performance variation.
- **CPU overcommitment** is common in hypervisors, where more vCPUs are assigned to VMs than there are physical cores, leading to greater flexibility and efficiency, but possibly causing CPU contention under heavy load.

Hypervisors also use advanced management techniques like **CPU pinning, reservations, limits, and shares** to optimize how CPU resources are allocated based on the needs and priorities of the VMs.

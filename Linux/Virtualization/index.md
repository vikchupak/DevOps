Read here about pros and corns of Type 1 and Type 2 https://aws.amazon.com/what-is/hypervisor/

- Type 1 hypervisor (native or bare-metal hypervisors). Examples: VMware ESXi, Microsoft Hyper-V, and Xen
- Type 2 hypervisor (hosted or embedded hypervisors). Examples: Oracle VirtualBox, VMware Workstation, and Parallels Desktop

Virtual Machine Images(Snapshots) - allows to backup the OS and all apps installed in case of hardware failure.

# Containers vs VMs

![image](https://github.com/user-attachments/assets/1c576f4d-5ec8-4c6b-96f2-dd3c75077ccb)

# WSL2

![image](https://github.com/user-attachments/assets/3371d6a2-4fa4-428c-9f6c-702c3da872ab)

**WSL2 (Windows Subsystem for Linux 2)** uses a **Type 1 (bare-metal) hypervisor** to run a full Linux kernel on Windows, **but** WSL2 itself is not a hypervisor. Instead, it leverages the **Hyper-V** hypervisor, which is built into Windows, to create a lightweight virtual machine where the Linux kernel can run.

Here’s how WSL2 works in relation to hypervisors:

### Key Points about WSL2 and Hyper-V:

1. **Hyper-V Integration**:
   - WSL2 relies on Microsoft's **Hyper-V** technology, a Type 1 hypervisor, to run a virtualized Linux kernel. However, unlike traditional Hyper-V virtual machines, WSL2 is optimized to be lightweight and offers near-native performance by tightly integrating with the Windows operating system.

2. **Full Linux Kernel**:
   - Unlike WSL1, which translated Linux system calls into Windows system calls, WSL2 runs a full Linux kernel inside a virtual machine. This approach provides full system call compatibility and better performance, especially for file I/O, networking, and running Docker containers.

3. **Virtual Machine (VM) Architecture**:
   - While WSL2 uses a virtual machine under the hood, it is not a full-blown, standalone VM like traditional Hyper-V VMs. It is designed to be more resource-efficient, with the ability to start and stop quickly, and it doesn’t require users to manage a separate VM instance.

4. **Seamless Integration with Windows**:
   - One of WSL2’s strengths is its ability to tightly integrate with Windows. You can run Linux applications and tools side by side with Windows apps, and they can interact with each other (e.g., accessing the same file system or network interfaces).

5. **Use of Virtualization-Based Security (VBS)**:
   - WSL2 leverages **Virtualization-Based Security** features of Windows, where Hyper-V is used to isolate processes and create secure execution environments.

### How WSL2 Differs from Traditional Hypervisors:
- **Purpose**: WSL2 is not a traditional hypervisor like Hyper-V, VMware, or VirtualBox. Its purpose is to run Linux applications natively on Windows in a highly integrated and lightweight way, rather than to manage full virtual machines.
- **No Full VM Management**: Users don’t interact with WSL2 as they would with a virtual machine. They interact with a Linux distribution (e.g., Ubuntu, Debian) installed via WSL2, which is abstracted from the underlying hypervisor.
- **Lightweight Virtualization**: WSL2 is designed to be much lighter than a standard virtual machine, with less overhead and better resource sharing between Linux and Windows environments.

### In Summary:
While WSL2 uses **Hyper-V**, a Type 1 hypervisor, for virtualization, WSL2 itself is not a hypervisor. It is more of an optimized environment that allows Windows users to run a full Linux kernel in a lightweight, virtualized space provided by Hyper-V.

![image](https://github.com/user-attachments/assets/a8de8698-a5d4-44a7-8ba3-05007aa72bb4)

### How Hyper-V Works in Windows

**Hyper-V** is a bit unique because it **blurs the line** between Type 1 and Type 2 hypervisors. Here's why:

1. **Hyper-V as a Type 1 (Bare-Metal) Hypervisor**:
   - **Hyper-V is a Type 1 hypervisor**, even though it can be installed on **Windows Server** or **Windows 10/11**. Once Hyper-V is enabled, it operates **directly on the hardware**, making it **bare-metal**. 
   - When you install **Hyper-V** on a Windows machine, the system **restructures** itself, placing the **Windows operating system** on top of the hypervisor. This means Windows effectively runs in a **VM** managed by Hyper-V.
   - Hyper-V becomes the controlling entity for all hardware interactions, managing both the host OS (Windows) and any guest VMs. Essentially, **Windows itself becomes a guest operating system** on top of Hyper-V.

2. **How Hyper-V Restructures the OS**:
   - After enabling Hyper-V, the Windows OS is moved into what's called the **"parent partition"** (or "management OS"). The **parent partition** has direct access to the hardware and manages the hypervisor and the virtual machines. It can be seen as a privileged VM that controls resource allocation to other VMs.
   - Guest operating systems run in **child partitions**, which are fully virtualized environments without direct access to the hardware.

3. **Hyper-V's "Bare-Metal" Nature**:
   - Although you see Windows running, underneath the surface, **Hyper-V is running directly on the hardware**. It functions as the **bare-metal hypervisor**, and Windows is just a "guest" OS with extra management responsibilities.

### Why Hyper-V is Considered Bare-Metal:

- **Direct Hardware Access**: Despite being installed through Windows, **Hyper-V interacts directly with the hardware**, bypassing any operating system layer that would introduce additional overhead. Once Hyper-V is active, Windows and other VMs access hardware resources through Hyper-V.
  
- **Reorganization of Windows**: After installation, the **Windows OS no longer runs directly on the hardware**. Instead, it's relegated to a VM-like environment within Hyper-V. This setup makes Hyper-V a **bare-metal hypervisor** because **all operating systems** (including the host OS) run on top of it.

### Summary:
- **Hyper-V** is technically a **bare-metal (Type 1) hypervisor**, even when it’s installed alongside Windows. Once enabled, **Hyper-V takes control of the hardware**, and Windows itself is moved into a special **parent partition**, acting as a management OS but no longer controlling the hardware directly. This architecture allows Hyper-V to remain **bare-metal**, even though it's integrated into a Windows environment.

## Sometimes there is virtualization settings in bios to enable/disable, is it the same settings as hyper-V?

![image](https://github.com/user-attachments/assets/60ec90eb-ef2b-4959-a702-00f9bea3694d)

The **virtualization settings** in the BIOS, such as **Intel VT-x** (for Intel processors) or **AMD-V** (for AMD processors), are not exactly the same as **Hyper-V**, but they are **closely related**. Let’s break it down:

### Virtualization Settings in BIOS (VT-x / AMD-V):
- **VT-x** (Intel Virtualization Technology) and **AMD-V** (AMD Virtualization) are **hardware virtualization extensions** provided by the processor.
- These settings in the BIOS enable the **CPU hardware features** that allow efficient virtualization. Specifically, they allow a hypervisor (like **Hyper-V**, **VMware**, or **VirtualBox**) to run virtual machines (VMs) with better performance and access to system resources, such as CPU and memory.
- **Hardware virtualization** helps by allowing virtual machines to run **directly on the CPU** without needing to emulate all CPU instructions in software, significantly improving performance for virtualized environments.

### Hyper-V:
- **Hyper-V** is a **software-based hypervisor** built into Windows that enables running virtual machines.
- **Hyper-V** relies on the **virtualization technology** provided by the CPU (such as **VT-x** or **AMD-V**) to function effectively. If the virtualization setting is **disabled** in the BIOS, **Hyper-V** (or any other hypervisor) cannot fully utilize the CPU's virtualization features, and it may either fail to start or run with degraded performance.

### Relationship Between BIOS Virtualization Settings and Hyper-V:
- **Enabling virtualization in the BIOS** is a **prerequisite** for using **Hyper-V** or any other hypervisor (like VMware or VirtualBox) that takes advantage of hardware virtualization.
- **Disabling virtualization in the BIOS** will prevent **Hyper-V** and other hypervisors from functioning correctly or efficiently. Even though **Hyper-V** is software, it depends on these **hardware extensions** to operate properly.

### Summary:
- The **virtualization settings** in the BIOS (such as **VT-x** or **AMD-V**) are **hardware-based** features that support virtualization.
- **Hyper-V** is a **software hypervisor** that uses these hardware virtualization extensions to manage virtual machines.
- The BIOS setting and Hyper-V are **different**, but **BIOS virtualization must be enabled** for Hyper-V to take full advantage of the hardware’s virtualization capabilities.

![image](https://github.com/user-attachments/assets/8b84a29b-0c75-4ae1-b8e2-a9c2f49fb577)

SVM stands for Secure Virtual Machine. It is AMD's hardware virtualization technology, equivalent to Intel's VT-x.

# WSL2 and other virtualization tools such as VirtualBox

https://learn.microsoft.com/en-us/windows/wsl/faq#will-i-be-able-to-run-wsl-2-and-other-3rd-party-virtualization-tools-such-as-vmware--or-virtualbox-

![image](https://github.com/user-attachments/assets/9fad984a-bc2b-4cd1-9dc2-1ccc583f8903)

# WSL 2 in a virtual machine

https://learn.microsoft.com/en-us/windows/wsl/faq#can-i-run-wsl-2-in-a-virtual-machine-

![image](https://github.com/user-attachments/assets/302c9b20-2bdb-48fa-91df-29079e4a916f)

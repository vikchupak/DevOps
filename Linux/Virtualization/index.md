Read here about pros and corns of Type 1 and Type 2 https://aws.amazon.com/what-is/hypervisor/

- Type 1 hypervisor (native or bare-metal hypervisors). Examples: VMware ESXi, Microsoft Hyper-V, and Xen
- Type 2 hypervisor (hosted or embedded hypervisors). Examples: Oracle VirtualBox, VMware Workstation, and Parallels Desktop

Virtual Machine Images(Snapshots) - allows to backup the OS and all apps installed in case of hardware failure.

# Containers vs VMs

![image](https://github.com/user-attachments/assets/1c576f4d-5ec8-4c6b-96f2-dd3c75077ccb)

# If Hyper-V is built in Windows, how can it be bare-metal?

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

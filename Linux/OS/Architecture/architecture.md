# Linux architecture list 

### **Summary of Most Common Architectures in Use Today**:
- **General Computing**: `x86_64`, `x86`, `arm64`
- **Mobile and Embedded**: `armhf`, `aarch64`, `mips`, `riscv`
- **High-Performance Servers/Mainframes**: `ppc64le`, `s390x`, `sparc64`

Here is a list of common architectures in Linux, along with their typical uses:

### **1. x86 (i386, i486, i586, i686)**
   - **Description**: The 32-bit architecture originally based on Intel's x86 family (e.g., 80386, 80486).
   - **Uses**: Common on older PCs and embedded systems, though less common today as 64-bit systems have become standard.

### **2. x86_64 (also called amd64)**
   - **Description**: The 64-bit extension of x86, introduced by AMD and also supported by Intel. Backward-compatible with x86.
   - **Uses**: Standard for most modern desktops, laptops, and servers.

### **3. ARM (armhf, armv6, armv7)**
   - **Description**: The 32-bit architecture. A family of reduced instruction set computing (RISC) architectures. `armhf` stands for "ARM hard-float," indicating hardware floating-point support.
   - **Uses**: Common in mobile devices, Raspberry Pi models, and embedded systems.

### **4. ARM64 (aarch64) - used in Apple's M-series chips (e.g., M1, M2)**
   - **Description**: 64-bit ARM architecture, also known as `aarch64`.
   - **Uses**: Found in newer mobile devices, tablets, Raspberry Pi 3 and 4, some servers, and **newer Macs with Apple Silicon**.

### **5. PowerPC (ppc, ppc64, ppc64le)**
   - **Description**: An architecture developed by IBM, Motorola, and Apple (32-bit `ppc` and 64-bit `ppc64`). `ppc64le` indicates little-endian 64-bit PowerPC.
   - **Uses**: Used in IBM servers, some older Apple computers, and high-performance computing.

### **6. MIPS (mips, mips64)**
   - **Description**: A RISC architecture that comes in both 32-bit and 64-bit versions.
   - **Uses**: Common in embedded systems, routers, and network devices.

### **7. RISC-V (rv32, rv64)**
   - **Description**: An open-source RISC architecture available in both 32-bit (`rv32`) and 64-bit (`rv64`) versions.
   - **Uses**: Emerging in embedded systems, research, and specialized hardware. Increasingly adopted in Linux distributions.

### **8. SPARC (sparc, sparc64)**
   - **Description**: Originally developed by Sun Microsystems, SPARC includes 32-bit and 64-bit versions.
   - **Uses**: Common in high-performance workstations and servers, especially in legacy Sun/Oracle systems.

### **9. S/390 (s390x)**
   - **Description**: IBM’s architecture for its mainframe systems, primarily 64-bit.
   - **Uses**: Found in enterprise-level IBM mainframes for high-reliability computing.

### **10. Itanium (ia64)**
   - **Description**: A 64-bit architecture developed by Intel and HP, separate from `x86_64`.
   - **Uses**: Used in specialized enterprise servers but is now largely obsolete.

### **11. Alpha**
   - **Description**: A 64-bit RISC architecture developed by Digital Equipment Corporation (DEC).
   - **Uses**: Found in older high-performance systems, especially DEC servers. Mostly deprecated today.

### **12. SuperH (sh, sh4)**
   - **Description**: A 32-bit architecture mainly used in embedded systems.
   - **Uses**: Common in embedded systems and legacy video game consoles.

### **13. HP-PA (PA-RISC)**
   - **Description**: HP's Precision Architecture RISC.
   - **Uses**: Used in HP’s older high-performance servers and workstations.

### **14. AVR32**
   - **Description**: A 32-bit architecture from Atmel, mostly for microcontroller use.
   - **Uses**: Embedded systems, though ARM and RISC-V have largely replaced it.

# Check the architecture of your Linux system

These commands should help identify the exact architecture and bit-width of your Linux system.

1. **Using `uname` command**:
   ```bash
   uname -m
   ```
   - **Output explanations**:
     - `x86_64`: 64-bit Intel/AMD architecture.
     - `armv7l`: 32-bit ARM architecture.
     - `aarch64` or `arm64`: 64-bit ARM architecture.

2. **Using `dpkg` (for Debian-based systems)**:
   ```bash
   dpkg --print-architecture
   ```
   - This will show the primary architecture, such as
     - `amd64` for `x86_64`
     - `armhf` for `armv7`
     - `arm64` for ARM 64-bit.

3. **Using `lscpu`**:
   ```bash
   lscpu
   ```
   - Look for the `Architecture` line for a detailed report, including compatibility and exact architecture details.

4. **Using `file` command on the kernel**:
   ```bash
   file /bin/bash
   ```
   - The output will specify whether it is `64-bit` or `32-bit` along with the architecture type.

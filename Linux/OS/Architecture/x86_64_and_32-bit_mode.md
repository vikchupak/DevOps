# About `x86_64` architercture

The term `x86_64` refers to the 64-bit version of the x86 instruction set architecture. Here’s a breakdown of what it means:

1. **"x86" Family**:
   - Originally, `x86` referred to a family of CPUs and their instruction sets, originating from Intel's 8086 processor in the late 1970s. **32-bit**
   - Over time, the term "x86" came to represent Intel-compatible processors using similar instruction sets (like 80386, 80486, etc.), widely used in PCs.

2. **Transition to 64-Bit**:
   - **x86_64** is a 64-bit extension of the 32-bit x86 architecture, introduced by AMD as AMD64. Intel later adopted it as Intel 64.
   - It allows systems to address more than 4 GB of memory (the limit for 32-bit architectures) and supports 64-bit computing.
   - This architecture is backward-compatible, meaning it can still run 32-bit x86 code.

3. **Advantages of x86_64 over x86**:
   - **Increased Memory**: It can address significantly more memory (up to 16 exabytes theoretically).
   - **Wider Registers**: 64-bit processors have larger registers, making certain computations faster.
   - **Improved Performance**: Enhanced instructions for optimized performance, especially in tasks that benefit from wide data paths like scientific computing or multimedia processing.

4. **Typical Uses**:
   - `x86_64` is the dominant architecture for most desktop computers, laptops, and many servers.
   - Most modern software for PCs is designed to run on `x86_64` to leverage its 64-bit capabilities.

So, `x86_64` signifies a 64-bit processor architecture based on and compatible with the older x86 architecture but with enhancements that support modern computing needs.

# Does `x86_64` support running x86 (32-bit) applications?

The `x86_64` architecture fully supports running `x86` (32-bit) applications. This compatibility is built into the design of `x86_64` processors, which can run both 32-bit and 64-bit code.

Here's how it works:

1. **Compatibility Mode (32-bit mode)**:
   - `x86_64` processors have a "compatibility mode" that allows them to execute 32-bit applications natively.
   - This means that when you run a 32-bit application on a 64-bit system, the processor switches to a mode that mimics the `x86` (32-bit) environment, allowing the application to function correctly without modification.

2. **Operating System Support**:
   - Most 64-bit operating systems, including Linux and Windows, come with support for running `x86` applications on `x86_64` hardware.
   - **On Linux, this is often achieved by installing 32-bit compatibility libraries, especially for applications that require specific libraries or dependencies in 32-bit versions.**

3. **Performance**:
   - Running `x86` applications on `x86_64` might have slightly reduced performance compared to running native `x86_64` applications, mainly due to mode switching and differences in memory usage.
   - However, for most applications, this performance difference is minimal and generally unnoticeable.

4. **Limitations**:
   - Some modern `x86_64`-only operating systems might drop native support for `x86` applications, though this is rare on Linux. For instance, certain versions of macOS (since 10.15 Catalina) have removed support for 32-bit apps, but this is specific to Apple's implementation.

So, as long as the OS supports it, `x86_64` architecture can run `x86` applications quite effectively.

# Check if the 32-bit mode (x86 compatibility mode) enabled

To check if 32-bit (i386 or i686) support is already enabled on your `x86_64` Linux system, you can follow these steps depending on the package manager and tools available on your system.

### **1. Check with `dpkg` (Debian/Ubuntu-based systems)**

On Debian-based systems (like Ubuntu), you can use the following command to check if the `i386` architecture is enabled:

```bash
dpkg --print-architecture
```

- If it returns `amd64`, it means the system is set to use only the 64-bit architecture.
- If it returns `amd64` and `i386`, it means multiarch support is enabled, and the system can run 32-bit applications.

You can also verify which architectures are enabled by running:

```bash
dpkg --print-foreign-architectures
```

If `i386` is listed, then 32-bit support is enabled.

### **2. Check the Installed Libraries**

You can also check if 32-bit libraries are installed, which indicates 32-bit application support.

#### **For `dpkg`-based systems (Debian/Ubuntu)**:
```bash
ls /lib/i386-linux-gnu/
```

If the directory exists and contains 32-bit libraries, then 32-bit support is enabled.

### **3. Check with `arch` or `uname -m`**:
The output of these commands shows the architecture your system is currently running. 

- If it shows `x86_64`, then you are using a 64-bit system.
- If `i686` or `i386` appears, it indicates 32-bit code is running, even on a 64-bit system.

```bash
arch
```

or

```bash
uname -m
```

### **Conclusion**:
- If you see `i386` or `i686` in any of the checks above, then 32-bit support is enabled.
- If you only see `amd64` or `x86_64`, 32-bit support may not be enabled, or it might require installing additional packages or enabling multiarch.

# Enable/disable support of 32-bit applications

On most modern Linux distributions, you can enable or disable support for 32-bit applications (i386 or `x86`) on an `x86_64` system. This support typically involves installing the necessary 32-bit libraries and configuring compatibility modes. Here's how you can manage this:

### **1. Enabling 32-Bit Support**
To enable 32-bit application support on a Linux `x86_64` system, you typically need to install the 32-bit libraries and packages that the 32-bit apps require.

#### **On Debian/Ubuntu-based systems**:
1. **Enable multiarch support**:
   If your system doesn't already support multiarch (running 32-bit and 64-bit binaries side by side), you can enable it by adding the `i386` architecture:
   ```bash
   sudo dpkg --add-architecture i386
   sudo apt update
   ```

2. **Install 32-bit libraries**:
   To install the 32-bit libraries, you can use the following command:
   ```bash
   sudo apt install libc6:i386
   ```
   This will install the 32-bit version of the `libc` library, which is required for most 32-bit applications.

3. **Install other necessary 32-bit libraries**:
   Some applications may require other specific 32-bit libraries, so you can install them in a similar manner (e.g., `lib32z1`, `lib32stdc++6`, etc.).

### **2. Disabling 32-Bit Support**
If you no longer need to run 32-bit applications and want to disable support, you can:

#### **On Debian/Ubuntu-based systems**:
1. **Remove 32-bit libraries**:
   You can uninstall the 32-bit libraries that you installed for compatibility.
   ```bash
   sudo apt remove libc6:i386
   sudo apt autoremove
   ```

2. **Remove multiarch**:
   If you no longer need multiarch, you can remove it with:
   ```bash
   sudo dpkg --remove-architecture i386
   sudo apt update
   ```

### **Summary**:
- **Enabling**: Add `i386` (or `i686`) architecture support and install the necessary 32-bit libraries.
- **Disabling**: Remove `i386` (or `i686`) architecture and the associated libraries.

Once you disable 32-bit support, any existing 32-bit applications or dependencies will no longer work unless re-enabled.

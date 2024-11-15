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

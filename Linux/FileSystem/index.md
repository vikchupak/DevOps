`man hier`

| ![photo_2024-07-20_22-59-52](https://github.com/user-attachments/assets/28873705-ae55-44af-aee5-f3e495422d18) | ![photo_2024-09-28_21-02-56](https://github.com/user-attachments/assets/b4e06cba-e33b-4940-b087-bb70c4b12d63) |
|------------------------|------------------------|

![photo_2024-09-28_21-01-09](https://github.com/user-attachments/assets/b4dbfee7-5ce5-4dfb-af75-7fe942821b2c)

- /home/{user}/ - users home directory. Only that user specific files/configs/apps. NOT system wide.
- /root - root user home directory
- /bin - user binaries | command that any user can run
- /sbin - system binarires | sudo commands
- /lib - libraries that /bin and /sbin use

  ![Screenshot from 2024-09-23 20-32-11](https://github.com/user-attachments/assets/c6dda356-50a8-45ba-8306-c500adc8ad9a)

- /usr - historically, old user home directory, but now the name doesn't reflect nowadays puprose (it is now used system wide, NOT specific to a user). Previously, due to memory limitations, files were split to /bin (system wide) and /usr/bin (user specific) directories. Terminal commands usually are executed from /usr/bin directory. Nowadays /bin is a soft link to /usr/bin and /sbin is a soft link to /usr/sbin.
  
  ![Screenshot from 2024-09-23 20-11-19](https://github.com/user-attachments/assets/24c2a092-2bbe-422b-8628-143223e99eca)

  ## There are /bin, /sbin and /usr/bin, /usr/sbin directories in Linux. What the difference?

  In Linux, directories such as `/bin`, `/sbin`, `/usr/bin`, and `/usr/sbin` contain executable programs (binaries) and are part of the file system hierarchy. Here's the difference between them:

  ### 1. **/bin (Binaries)**
  - **Purpose**: Contains essential user command binaries (executables) required for the system to boot, repair, or operate in single-user mode.
  - **Who can access**: Regular users and the root user.
  - **Examples**: Common commands like `ls`, `cat`, `cp`, `mv`, `bash`, and `mkdir` are stored here.
  - **Availability**: These commands must be available even if no other file systems (like `/usr`) are mounted, hence the need for basic functionality during system startup or repair.

  ### 2. **/sbin (System Binaries)**
  - **Purpose**: Contains essential system administration binaries used primarily by the root user for system maintenance.
  - **Who can access**: Usually restricted to the root user, though non-root users can execute some commands with `sudo`.
  - **Examples**: Commands like `ifconfig`, `fdisk`, `fsck`, and `reboot` are stored here.
  - **Availability**: Like `/bin`, `/sbin` contains critical binaries that must be available during system startup or single-user mode.

  ### 3. **/usr/bin (User Binaries)**
  - **Purpose**: Contains non-essential user command binaries. This is the main location for user programs that are not required for booting or in single-user mode but are used during normal multi-user operation.
  - **Who can access**: Regular users and the root user.
  - **Examples**: Common applications like `gcc`, `vim`, `python`, `git`, and `ssh` are stored here.
  - **Availability**: Programs in `/usr/bin` become available after the `/usr` partition is mounted.

  ### 4. **/usr/sbin (System Binaries for Superuser)**
  - **Purpose**: Contains non-essential system administration binaries that are used after the system is fully operational. These commands are generally meant for system administration by the root user.
  - **Who can access**: Primarily the root user, but some binaries can be accessed with `sudo`.
  - **Examples**: Commands like `apache2`, `dhcpd`, `named`, and `useradd` are stored here.
  - **Availability**: Like `/usr/bin`, the binaries here are available after the `/usr` partition is mounted.

  ### Key Differences:
  - **Location**: `/bin` and `/sbin` contain essential binaries, while `/usr/bin` and `/usr/sbin` contain non-essential binaries.
  - **Purpose**: `/bin` and `/usr/bin` are for general-purpose user commands, while `/sbin` and `/usr/sbin` are reserved for system administration.
  - **Accessibility**: `/bin` and `/usr/bin` are accessible by all users, whereas `/sbin` and `/usr/sbin` are primarily intended for root or administrative tasks.

  In modern Linux distributions, some differences between these directories are becoming less distinct due to changes like symlinking `/bin` to `/usr/bin`, which is part of the **"Merged /usr"** initiative. However, understanding their traditional separation is still useful.
  
- /usr/local/ - third-party apps are installed here (apps that installed by a user). **Those apps are system wide available**.
- /home/{user}/.local/ - third-party apps are installed here (apps that installed by a user). **User specific apps are installed here**.

On Linux, to install an application for a specific user (not system-wide), you can install the application in your user's home directory. There are a few approaches:

- **Using package managers** (for languages like Python, Node.js):
  - For **Python**:
    ```bash
    pip install --user package_name
    ```
    This installs the package to `~/.local/lib/pythonX.Y/site-packages`.

  - For **Node.js**:
    ```bash
    npm install --global --prefix ~/.local package_name
    ```
    This installs the Node.js package to your home directory under `~/.local`.

- **Compiling software from source**:
  You can download the source code for an application, compile it, and specify the installation directory in your home folder, for example:
  ```bash
  ./configure --prefix=/home/username/local
  make
  make install
  ```

- /opt - stands for optional. Third-party app are installed here. But only not splitable apps (no splitting on /bin, /sbin, /lib, etc.)
- /etc - config files. Historical name, nowadays doesn't reflect purpose. **editable and system wide**.
- /home/{user}/.config/ - user specific configs.
- /dev - stands for devices. all files that system needs to interact with devices
- /var - all system logs stored here
- /var/cache - applications chache
- /tmp - for temporary data
- /media - **automatically mounts removable media devices (like usb, cd card). So we can see content opening the corresponding folder.**
  ![Screenshot from 2024-10-21 23-49-08](https://github.com/user-attachments/assets/ae757b1c-d592-4611-97ab-2ffe8206ebd8)
- /mnt - for manual mounting, like file system.
- /proc - stands for procesess. Intersection between procesess and file system. State of processes in virtual file system(mounted in /proc). The place where the kernel places the information about processes. https://www.youtube.com/watch?v=0XdjODvsRN8

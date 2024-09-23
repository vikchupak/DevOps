`man hier`

![photo_2024-07-20_22-59-52](https://github.com/user-attachments/assets/28873705-ae55-44af-aee5-f3e495422d18)

![photo_2024-07-20_23-01-39](https://github.com/user-attachments/assets/db3679a0-a70a-4da1-a3ba-1b352fbbb93b)

- /home/{user}/ - users home directory. Only that user specific files/configs/apps. NOT system wide.
- /root - root user home directory
- /bin - command that any user can run
- /sbin - system (sudo) commands
- /lib - libraries that /bin and /sbin use
- /usr - historically, old user home directory, but now the name doesn't reflect nowadays puprose (it is now used system wide, NOT specific to a user). Previously, due to memory limitations, files were split to /usr/bin and /usr/bin directories. Terminal commands usually are executed from /usr/bin directory BECAUSE /bin is a soft link to /usr/bin and /sbin is a soft link to /usr/sbin.
  ![Screenshot from 2024-09-23 20-11-19](https://github.com/user-attachments/assets/24c2a092-2bbe-422b-8628-143223e99eca)
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
- /media - automatically mounts removable media devices (like usb, cd card). So we can see content opening the corresponding folder.
- /mnt - for manual mounting, like file system.
- /proc - stands for procesess. Intersection between procesess and file system. State of processes in virtual file system(mounted in /proc). The place where the kernel places the information about processes. https://www.youtube.com/watch?v=0XdjODvsRN8

`man hier`

![photo_2024-07-20_22-59-52](https://github.com/user-attachments/assets/28873705-ae55-44af-aee5-f3e495422d18)

![photo_2024-07-20_23-01-39](https://github.com/user-attachments/assets/db3679a0-a70a-4da1-a3ba-1b352fbbb93b)

- /bin - command that any user can run
- /sbin - sudo commands
- /lib - libraries that /bin and /sbin use
- /usr - historically, old user home directory, but now the name doesn't reflect nowadays puprose (it is now used system wide, NOT specific to a user). Previously, due to memory limitations, files were split to /bin and /usr/bin directories. Terminal commands usually are executed from /usr/bin directory.
- /usr/local/ - third-party apps are installed here (apps that installed by a user). **Those apps are system wide available**.
- /home/{user}/.local/ - third-party apps are installed here (apps that installed by a user). **User wide apps are installed here**.

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
  

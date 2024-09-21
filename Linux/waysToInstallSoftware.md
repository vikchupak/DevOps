- APT manager (uses repositories to fetch packages; sometimes we have to add repositories to official list [/etc/apt/sources.list] to install aplications that are not yet in the official repositories)
- Ubuntu Software Center (Like an app store. A discontinued high-level graphical front end for the APT/dpkg package management system. Can also be used to add repositories)\
   https://en.wikipedia.org/wiki/Ubuntu_Software_Center \
   ![Screenshot from 2024-09-21 14-55-58](https://github.com/user-attachments/assets/1d2d1ffd-0a62-4527-87e9-e3e53890918e)
- Snap (Snap is a package management system developed by Canonical, the makers of Ubuntu, for operating systems that use the Linux kernel. A snap is an application containerised with all its dependencies. Snap packages have `.snap` extension. `snapd` - the snap daemon, which manages and executes snaps on your system)

  [Snap Store](https://snapcraft.io/store) an application repository hosted and managed by Canonical, and are free for anyone to download\
  Snapcraft - framework used to build and publish snaps

  https://snapcraft.io/about \
  https://ubuntu.com/core/services/guide/snaps-intro \
  https://en.wikipedia.org/wiki/Snap_(software)

  To install Snap on your Linux system, you typically use the following commands:
  ```bash
  sudo apt update
  sudo apt install snapd
  ```
  Once Snap is installed, you can install applications using the `snap` command, like this:
  ```bash
  sudo snap install <package-name>
  ```
  

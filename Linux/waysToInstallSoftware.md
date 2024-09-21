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

- Personal Package Archive (PPA)

A **Personal Package Archive (PPA)** is a specialized software repository for Ubuntu and its derivatives, like Linux Mint. PPAs allow individuals or organizations to distribute their own software packages or versions of existing software __independently of the official repositories__. PPAs are hosted on **Launchpad**, a platform maintained by Canonical, and they provide a way for developers to deliver the latest versions of applications or custom-built software that may not be available in the default Ubuntu repositories.

### Key Features of PPAs:
1. **Easy Software Distribution**: PPAs allow developers to create and distribute packages to users quickly and easily without having to go through the more stringent official Ubuntu repository process.
2. **User Flexibility**: Users can add PPAs to their system to install newer or custom versions of software that may not be available through official channels.
3. **Launchpad Integration**: PPAs are hosted on Launchpad (https://launchpad.net), which provides tools for maintaining, building, and uploading software packages.

### How to Add a PPA in Ubuntu
To add a PPA to your system, use the following commands:

1. **Add the PPA**:
   ```bash
   sudo add-apt-repository ppa:<ppa-name>
   ```
   For example, to add the PPA for the latest version of the `VLC` media player:
   ```bash
   sudo add-apt-repository ppa:videolan/stable-daily
   ```

2. **Update the package list**:
   After adding the PPA, update the system's package list:
   ```bash
   sudo apt update
   ```

3. **Install the software**:
   Once updated, install the software as you normally would:
   ```bash
   sudo apt install <package-name>
   ```

### Managing PPAs
- **List installed PPAs**: To list the PPAs added to your system:
  ```bash
  grep ^ /etc/apt/sources.list.d/*
  ```

- **Remove a PPA**: To remove a PPA from your system, use:
  ```bash
  sudo add-apt-repository --remove ppa:<ppa-name>
  ```

### Benefits of PPAs:
- Access to the latest software versions.
- Availability of niche or less mainstream software.
- Community-driven updates and customizations.

### Drawbacks:
- PPAs are not officially tested or verified by Ubuntu, which may introduce stability or security risks.
- Outdated or unmaintained PPAs can cause issues if the software becomes incompatible with newer versions of the system.

PPAs are an excellent way to access cutting-edge software while maintaining the flexibility of a traditional package manager system.

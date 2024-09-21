- **APT manager** (uses repositories to fetch packages; sometimes we have to add repositories to official list [/etc/apt/sources.list] to install aplications that are not yet in the official repositories)
- **Ubuntu Software Center** (Like an app store. A discontinued high-level graphical front end for the APT/dpkg package management system. Can also be used to add repositories)\
   https://en.wikipedia.org/wiki/Ubuntu_Software_Center \
   ![Screenshot from 2024-09-21 14-55-58](https://github.com/user-attachments/assets/1d2d1ffd-0a62-4527-87e9-e3e53890918e)
- **Snap** (Snap is a package management system developed by Canonical, the makers of Ubuntu, for operating systems that use the Linux kernel. A snap is an application containerised with all its dependencies. Snap packages have `.snap` extension. `snapd` - the snap daemon, which manages and executes snaps on your system)

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

- **Personal Package Archive (PPA)**
  
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

# Install using .deb
https://docs.docker.com/desktop/install/linux/ubuntu/

![image](https://github.com/user-attachments/assets/fa85eaad-7da3-44a2-b217-b8f0e938e647)

The difference between installing a `.deb` file using `sudo apt-get install ./package.deb` and installing a package directly via `sudo apt install package-name` comes down to how the package is managed and where it comes from:

### 1. **Installing a Local `.deb` File**
When you download a `.deb` file manually (e.g., `docker-desktop-<arch>.deb`) and run:

```bash
sudo apt-get install ./docker-desktop-<arch>.deb
```

- **Local File**: You're instructing `apt-get` to install the specific file you've already downloaded.
- **No Repositories**: It doesn't use online repositories to find and install the package; instead, it works with the `.deb` file located on your local machine.
- **Dependencies**: If this `.deb` package has dependencies, `apt` will try to resolve and install them from the repository. However, for this to work properly, you must have run `sudo apt update` earlier.

### 2. **Installing from Repositories**
When you run:

```bash
sudo apt install docker-desktop-<arch>
```

- **Repository Search**: This command searches for `docker-desktop-<arch>` in the repositories that are defined in your system's package source list (usually in `/etc/apt/sources.list` and `/etc/apt/sources.list.d/`).
- **No `.deb` Needed**: You don't need to manually download the package, as `apt` will handle the download and installation automatically if the package exists in one of the repositories.
- **Official/Third-Party Repos**: If `docker-desktop-<arch>` isn't available in the default repositories, you'd need to add a custom repository (like Docker's official repository) for it to be found.

### Why Download a `.deb` File?

You need to manually download a `.deb` file in cases like:

- The package isn't available in your system's repositories.
- You don't want to (or can't) add an external repository (e.g., Docker's repository).
- You're installing a specific version of the package that's not in the repository.
  
In the case of `docker-desktop`, Docker provides `.deb` packages for direct download, but you can also install it via their repository by adding it to your `sources.list`, after which `sudo apt install docker-desktop` would work without manually downloading the `.deb`.

### Example of Adding Docker’s Repository

```bash
# Add Docker’s official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Set up the stable repository
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update package list
sudo apt update

# Install Docker Desktop
sudo apt install docker-desktop
```

This way, `apt install docker-desktop` would work without needing to download the `.deb` file manually.

![image](https://github.com/user-attachments/assets/7a27d642-c6bc-4a7a-9e26-4402517ba6ad)


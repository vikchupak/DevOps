- ***APT manager***

```bash
# List installed apt packages
apt list --installed
```

  (uses repositories to fetch packages (__.deb packages__); sometimes we have to add repositories to official list [/etc/apt/sources.list] to install aplications that are not yet in the official repositories)

  ### Does `apt` use `dpkg` under the hood?

  Yes, **`apt` uses `dpkg` under the hood** for low-level package management tasks. While `apt` is a **higher-level package manager**, `dpkg` is the **core tool** responsible for actually installing, removing, and configuring `.deb` packages on Debian-based systems like Ubuntu.

   ### Relationship Between `apt` and `dpkg`:
   - **`dpkg`**: Handles the basic operations of installing, removing, and querying individual packages. However, it does **not manage dependencies** on its own. If a package requires additional software, `dpkg` will not automatically resolve or install those dependencies.
  
   - **`apt`**: Acts as a **higher-level package manager** that interacts with **online repositories**, handles **dependencies**, and provides an easier-to-use interface. It ensures that all required packages are installed or removed together. When `apt` installs a package, it ultimately uses `dpkg` to perform the actual package installation or removal.

   ### How `apt` Uses `dpkg`:
   1. **Dependency Management**:
      - When you run a command like `sudo apt install <package>`, `apt` first determines which additional packages (dependencies) are needed. After resolving dependencies, it downloads all the necessary `.deb` files from repositories.
   
   2. **Calling `dpkg`**:
      - Once `apt` has all the required packages, it **calls `dpkg`** in the background to handle the **installation** or **removal** of each `.deb` package.

   3. **Low-Level Tasks**:
      - Operations such as **configuring installed packages**, **querying package status**, or **handling post-install scripts** are also performed by `dpkg` during this process, but `apt` abstracts these details from the user.

   ### Example Workflow:
   When you run `sudo apt install <package>`, here’s what happens:
   1. **`apt`** fetches the package and its dependencies from the repository.
   2. It uses `dpkg` to **unpack** and **install** the `.deb` files.
   3. `dpkg` installs the software and manages the configuration.
   4. **`apt`** handles package cleanup and repository maintenance (e.g., updating the package cache, resolving any remaining dependencies).

   ### Summary:
   - **`apt`** provides a higher-level interface for users, handling dependencies and repository management.
   - **`dpkg`** performs the actual installation and configuration of `.deb` packages, which is invoked by `apt` for low-level tasks.
  
- ***Ubuntu Software app***

  (Like an app store. A discontinued high-level graphical front end for the **APT and snap** package management. Can also be used to add repositories)\
   https://en.wikipedia.org/wiki/Ubuntu_Software_Center \
   ![Screenshot from 2024-09-21 14-55-58](https://github.com/user-attachments/assets/1d2d1ffd-0a62-4527-87e9-e3e53890918e)

  ![Screenshot from 2024-09-24 21-16-41](https://github.com/user-attachments/assets/4392ba52-8ad4-4e9d-b553-110853485408)

  ### What is Ubuntu Software Center?
  
  The **Ubuntu Software Center** (now known as **Ubuntu Software**) is a **graphical application** that provides a user-friendly interface for managing software on **Ubuntu**. It allows users to easily browse, install, update, and remove applications without needing to use the command line. It functions similarly to an app store but for Linux packages.

   ### Key Features:
   1. **Software Discovery**:
      - Users can browse through thousands of applications, categorized by type (e.g., productivity, games, utilities).
      - Applications are displayed with descriptions, ratings, and reviews to help users choose the right software.

   2. **One-Click Installations**:
      - You can install software with just one click, as opposed to using the command line with tools like `apt`.
      - Software packages include both **open-source** applications and proprietary software.

   3. **Managing Installed Software**:
      - Users can update, remove, or manage installed applications easily from the interface.
      - It supports **automatic updates** and notifications when new software updates are available.

   4. **Support for Snap Packages**:
      - In addition to traditional **APT packages** (from Ubuntu's official repositories), the Ubuntu Software Center supports **Snap packages**. Snaps are self-contained packages that include all dependencies, allowing for easier software management across different Linux distributions.

   5. **Graphical Alternative to `apt`**:
      - Ubuntu Software provides a graphical alternative to command-line tools like `apt` and `dpkg`. This makes it easier for non-technical users to install and manage software without needing to understand Linux package management commands.

   ### History:
   - **Ubuntu Software Center** was the original name of this tool, introduced in **Ubuntu 9.10 (Karmic Koala)** to replace older package management tools like **Synaptic Package Manager**.
   - In more recent versions of Ubuntu, it has been rebranded to **Ubuntu Software** and is now based on **GNOME Software**, a broader software management tool used in many Linux distributions.
   
   ### Summary:
   **Ubuntu Software Center** (or **Ubuntu Software**) is the graphical user interface for managing software in Ubuntu, designed to make it easy for users to discover, install, update, and remove applications without using the terminal. It supports both traditional APT packages and newer Snap packages, giving users flexibility and ease of use when managing software.

- ***Snap management system***

```bash
# List installed snaps
snap listt
```
  (Snap is a package management system developed by Canonical, the makers of Ubuntu, for operating systems that use the Linux kernel. A snap is an application containerised with all its dependencies. Snap packages have `.snap` extension. `snapd` - the snap daemon, which manages and executes snaps on your system)

  ### Is that correct to say `snap package manager`?

  Yes, it's correct to refer to Snap as a package manager, though it's technically more than that. Snap is a package management system to distribute and manage applications in the form of snap packages across different Linux distributions.

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

- ***Personal Package Archive (PPA)***
  
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


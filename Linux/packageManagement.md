- ```apt-get``` (Advanced package tool) - old low-level interface that communicates more closely with core Linux processes
- ```apt``` - new designed as a more user-friendly alternative to apt-get, combining the functionality of multiple package management tools for user convenience. Надстройка над apt-get. Потребує super user rights?

- https://aws.amazon.com/compare/the-difference-between-apt-and-apt-get/#:~:text=The%20apt%20command%20line%20tool,closely%20with%20core%20Linux%20processes.
- https://www.baeldung.com/linux/apt-vs-apt-get

- ```apt update``` - updates packages list (info about available updates)
- ```apt upgrade``` - downloads and installes the updates for each outdated package and dependency on your system
- ```alias uup="sudo apt update && sudo apt upgrade"``` - **useful alias**

  ![image](https://github.com/user-attachments/assets/d76bfd36-40c8-434f-b705-7deeae8c2e39)
  
   ### Will `sudo apt upgrade` update all installed packages?

  Yes, running `sudo apt upgrade` will attempt to **update all installed packages** on your system to their latest available versions, but with some key points to understand:

   ### How `sudo apt upgrade` Works:
   - **`apt upgrade`** updates all **installed packages** for which new versions are available in the repositories.
   - It will only upgrade packages if the upgrade **does not require removing any currently installed packages** or installing new ones (dependencies). In other words, `apt upgrade` will perform "safe" upgrades where the new versions are compatible with the currently installed package set.

   ### Key Behaviors:
   1. **No Package Removal**:
      - `apt upgrade` will **not remove** any packages. If an upgrade would require removing an existing package, the upgrade will be skipped for that package.
   
   2. **No New Package Installations**:
      - `apt upgrade` will **not install new packages**. If an upgrade requires installing new dependencies or packages, that particular package will not be upgraded.

   3. **Upgrades Only**:
      - It only **upgrades the packages** that can be updated without altering the existing package dependencies or structure.

   ### For More Comprehensive Upgrades:
   - If you want to allow package upgrades that might require **removing** or **installing new packages**, you should use:
     - **`sudo apt full-upgrade`** (previously `dist-upgrade`): This command performs a more comprehensive upgrade, allowing for package removals or new installations as necessary to complete the upgrade process.
  
     - **`sudo apt autoremove`**: After using `apt full-upgrade`, you might want to run `sudo apt autoremove` to clean up unused packages and dependencies that are no longer needed.

   ### Summary:
   - **`sudo apt upgrade`** will update all installed packages **as long as no new packages or removals are required**.
   - For a more aggressive upgrade that may remove or install additional packages, use **`sudo apt full-upgrade`**.

- ```apt install <package_name>``` - install package

- ```apt list --installed``` or ```dpkg --list``` - show instlled packages
- ```apt purge <package_name>``` - remove package with all its config files
- ```apt remove <package_name>``` - remove package keeping the package’s configuration files
- ```apt autoremove && apt clean``` - post uninstall clean up https://www.geeksforgeeks.org/how-to-uninstall-packages-with-apt-package-manager-in-linux/
  - `apt clean`
    - Clears the local cache of downloaded package files.
    - Removes everything from `/var/cache/apt/archives/`, freeing up disk space.
    - Does not remove installed packages, only cleans up cached .deb files.
  - `apt autoremove`
    - Removes packages that were automatically installed as dependencies but are no longer needed.
    - Helps clean up orphaned packages that were installed along with a program you later uninstalled.

  **`apt clean` vs `apt autoremove`**
  | Command          | Removes Installed Packages? | Clears Cache? | Purpose |
  |-----------------|---------------------------|--------------|---------|
  | `apt clean`     | ❌ No                      | ✅ Yes       | Frees space by deleting cached `.deb` files. |
  | `apt autoremove` | ✅ Yes                     | ❌ No       | Removes unused dependencies. |

- ```alias purgepkg='f(){ sudo apt purge -y "$1" && sudo apt autoremove -y && sudo apt clean; }; f'``` - **useful alias**
  - Usage `purgepkg "openjdk-8-*"`
  - `"openjdk-8-*"` - asterisk to remove all the **pattern** matching packages like
    - `openjdk-8-jdk`
    - `openjdk-8-jdk-headless`
    - `openjdk-8-jre`
    - `openjdk-8-jre-headless`
- ```apt search <search_term>``` - search package
   ### Do I have to run `sudo apt update` before running `sudo apt search <package>`?
  It is not strictly necessary to run `sudo apt update` before running `sudo apt search <package>`, but it is generally a good idea. Here’s why:
   #### What Happens with `sudo apt search <package>`:
   - The `apt search` command looks for the specified package in the local cache of available packages. It shows information from the **package metadata** stored on your system.
   - If you haven't updated this cache in a while, the information may be **outdated**. It may not reflect the latest versions of packages or the availability of new packages that have been added to the repositories since your last update.
  
- ```apt show <package_name>``` - show info about package
- ```apt policy python3``` - display information about the Python 3 package, **including the candidate version** (latest available version in the repository) and the installed version (if applicable) 

# Difference between apt, apt-get, apt-cache, apt-config

https://www.geeksforgeeks.org/difference-between-apt-apt-get-apt-cache-and-apt-config/

- ```apt``` is replacement fot ```apt-get``` and ```apt-cache```
- ```apt``` is NOT replacement for ```apt-config```

![image](https://github.com/user-attachments/assets/6174ac30-3938-459a-9fc5-f84153898e0d)

https://aws.amazon.com/compare/the-difference-between-apt-and-apt-get/

![image](https://github.com/user-attachments/assets/dad547f7-890f-434b-b9b0-cb8b555ac803)

__Ubuntu is a Linux distribution derived from Debian__

![image](https://github.com/user-attachments/assets/b7bf02b3-6ef7-44b2-9d00-dcb64f9acd3f)

# Find out system apt or apt-get

To determine whether you have `apt` or `apt-get` (or both) installed on your system, you can use the command line to check their availability. Here's how you can do it:

1. **Check for `apt`**:
   Open a terminal and type the following command:
   ```sh
   apt --version
   ```
   If `apt` is installed, this command will display the version information. If not, it will return an error indicating that the command was not found.

2. **Check for `apt-get`**:
   Open a terminal and type the following command:
   ```sh
   apt-get --version
   ```
   If `apt-get` is installed, this command will display the version information. If not, it will return an error indicating that the command was not found.

### Notes
- __*It's common for modern Debian-based systems (including Ubuntu) to have both `apt` and `apt-get` installed.*__
- You can also check the availability of `apt-cache` and `apt-config` using the same method:
  ```sh
  apt-cache --version
  apt-config --version
  ```

These commands will help you verify whether the respective tools are installed on your system.

# Difference in commands

```bash
# apt
apt update
# apt-get
apt-get update
```
```bash
# apt
apt upgrade
# apt-get
apt-get upgrade
```
```bash
# apt
apt install <package_name>
# apt-get
apt-get install <package_name>
```
```bash
# apt
apt remove <package_name>
# apt-get
apt-get remove <package_name>
```
```bash
# apt
apt purge <package_name>
# apt-get
apt-get purge <package_name>
```
```bash
# apt
apt autoremove
# apt-get
apt-get autoremove
```
```bash
# apt
apt search <package_name or description>
# apt-cache
apt-cache search <package_name or description>
```
```bash
# apt
apt show <package_name>
# apt-cache
apt-cache show  <package_name> 
```

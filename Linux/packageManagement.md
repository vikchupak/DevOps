- ```apt-get``` (Advanced package tool) - old low-level interface that communicates more closely with core Linux processes
- ```apt``` - new designed as a more user-friendly alternative to apt-get, combining the functionality of multiple package management tools for user convenience. Надстройка над apt-get. Потребує super user rights?

- https://aws.amazon.com/compare/the-difference-between-apt-and-apt-get/#:~:text=The%20apt%20command%20line%20tool,closely%20with%20core%20Linux%20processes.
- https://www.baeldung.com/linux/apt-vs-apt-get

- ```apt update``` - updates packages list (info about available updates)
- ```apt upgrade``` - downloads and installes the updates for each outdated package and dependency on your system
- ```apt install <package_name>``` - install package

- ```apt list --installed``` - show instlled packages
- ```apt purge <package_name>``` - remove package with all its config files
- ```apt remove <package_name>``` - remove package keeping the package’s configuration files
- ```apt clean && apt autoremove``` - post uninstall clean up https://www.geeksforgeeks.org/how-to-uninstall-packages-with-apt-package-manager-in-linux/
- ```apt search <search_term>``` - search package
- ```apt show <package_name>``` - show info about package

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

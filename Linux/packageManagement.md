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

# Difference between apt, apt-get, apt-cache, apt-config

https://www.geeksforgeeks.org/difference-between-apt-apt-get-apt-cache-and-apt-config/

- ```apt``` is replacement fot ```apt-get``` and ```apt-cache```
- ```apt``` is NOT replacement for ```apt-config```

GPT says:\
`apt` is not a replacement for `apt-config`. While `apt` provides a unified interface for many of the common functionalities of `apt-get` and `apt-cache`, it does not encompass the specific configuration querying and setting functionalities of `apt-config`.

**`apt`** is designed to simplify package management commands, combining the more frequently used options of `apt-get` and `apt-cache` into a single command for ease of use.

**`apt-config`**, on the other hand, is a specialized tool for handling APT configuration settings. It allows you to query and manipulate the APT configuration, which is not something `apt` is designed to do.

Therefore, `apt-config` remains a necessary and distinct tool for managing APT configuration, particularly for advanced users and developers who need to customize APT's behavior at a detailed level.

```bash
# apt
apt update
# apt-get
apt get update
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

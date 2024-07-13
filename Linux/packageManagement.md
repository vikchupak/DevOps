- apt-get (Advanced package tool) - old low-level interface that communicates more closely with core Linux processes
- apt - new designed as a more user-friendly alternative to apt-get, combining the functionality of multiple package management tools for user convenience. Надстройка над apt-get. Потребує super user rights?

- https://aws.amazon.com/compare/the-difference-between-apt-and-apt-get/#:~:text=The%20apt%20command%20line%20tool,closely%20with%20core%20Linux%20processes.
- https://www.baeldung.com/linux/apt-vs-apt-get

- apt update - updates packages list (info about available updates)
- apt upgrade - downloads and installes the updates for each outdated package and dependency on your system
- apt install <package_name> -install package

- apt list --installed - show instlled packages
- apt purge <package_name> - remove package with all its config files
- apt remove <package_name> - remove package keeping the package’s configuration files
- apt clean && apt autoremove - post uninstall clean up https://www.geeksforgeeks.org/how-to-uninstall-packages-with-apt-package-manager-in-linux/

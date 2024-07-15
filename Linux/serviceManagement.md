# service vs systemctl

Both `service` and `systemctl` are used to manage system services in Linux, but they belong to different init systems and have distinct functionalities and usage scenarios. Here's a detailed comparison:

### `service`

- **Legacy Tool**:
  - `service` is part of the System V (SysV) init system, which is an older init system used to manage system services.
  - It provides a more uniform way to interact with scripts located in `/etc/init.d/`.

- **Basic Usage**:
  - The syntax is relatively simple:
    ```sh
    service <service_name> <command>
    ```
  - Example commands:
    ```sh
    service apache2 start    # Starts the apache2 service
    service apache2 stop     # Stops the apache2 service
    service apache2 restart  # Restarts the apache2 service
    ```

- **Common Commands**:
  - `start`: Starts a service.
  - `stop`: Stops a service.
  - `restart`: Restarts a service.
  - `status`: Checks the status of a service.

### `systemctl`

- **Modern Tool**:
  - `systemctl` is part of the `systemd` init system, which is the default on most modern Linux distributions (e.g., Ubuntu 16.04 and later, Fedora, CentOS 7 and later).
  - `systemd` is more powerful and feature-rich than SysV, providing better performance and more capabilities.

- **Extended Functionality**:
  - `systemctl` can manage services, sockets, timers, devices, and more.
  - It provides a more extensive set of commands and options for managing services.

- **Basic Usage**:
  - The syntax is a bit more verbose but also more consistent:
    ```sh
    systemctl <command> <service_name>
    ```
  - Example commands:
    ```sh
    systemctl start apache2    # Starts the apache2 service
    systemctl stop apache2     # Stops the apache2 service
    systemctl restart apache2  # Restarts the apache2 service
    systemctl status apache2   # Checks the status of the apache2 service
    ```

- **Common Commands**:
  - `start`: Starts a service.
  - `stop`: Stops a service.
  - `restart`: Restarts a service.
  - `status`: Checks the status of a service.
  - `enable`: Enables a service to start on boot.
  - `disable`: Disables a service from starting on boot.
  - `is-enabled`: Checks if a service is enabled.
  - `is-active`: Checks if a service is currently active (running).
  - `daemon-reload`: Reloads the systemd manager configuration.

### Summary

- **`service`**:
  - Part of the older SysV init system.
  - Simple and straightforward for basic service management.
  - Limited to start, stop, restart, and status commands.

- **`systemctl`**:
  - Part of the modern `systemd` init system.
  - More powerful and feature-rich, with extended capabilities.
  - Used for managing a wide range of system entities beyond just services.

In most modern Linux distributions, `systemctl` is the preferred tool due to its advanced capabilities and the prevalence of `systemd` as the init system. However, `service` may still be useful in systems that use SysV or for backward compatibility purposes.

# Determine whether there is service or systemctl tool in a system

To determine whether you have the `service` or `systemctl` tool on your system, you can use the following methods:

### Check for `service`

1. **Command Line Check**:
   - Open a terminal and type the following command:
     ```sh
     service --version
     ```
   - If `service` is installed, it will display the version information or a usage message. If it is not installed, it will return an error indicating that the command was not found.

### Check for `systemctl`

1. **Command Line Check**:
   - Open a terminal and type the following command:
     ```sh
     systemctl --version
     ```
   - If `systemctl` is installed, it will display the version information of `systemd`. If it is not installed, it will return an error indicating that the command was not found.

### Example Outputs

- For `service`:
  ```sh
  $ service --version
  Usage: service <option> | --status-all | [ service_name [ command | --full-restart ] ]
  ```
  - If `service` is available, it will show a usage message or version information.

- For `systemctl`:
  ```sh
  $ systemctl --version
  systemd 245 (245.4-4ubuntu3.11)
  +PAM +AUDIT +SELINUX +IMA +APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 +ZSTD +SECCOMP +BLKID +ELFUTILS +KMOD +IDN2 -IDN +PCRE2 default-hierarchy=hybrid
  ```
  - If `systemctl` is available, it will show the version information along with the build details of `systemd`.

### Summary

- Use `service --version` to check for the presence of the `service` command.
- Use `systemctl --version` to check for the presence of the `systemctl` command.

__*If both commands are available, it is likely that your system uses `systemd`, but it also includes the `service` command for compatibility with older SysV init scripts. Modern distributions typically use `systemctl` as the primary tool for service management.*__

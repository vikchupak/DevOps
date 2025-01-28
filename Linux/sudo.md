# sudo group

![image](https://github.com/user-attachments/assets/cdcf2e56-4b30-4b6d-b3d8-42a0433c6f1e)

![image](https://github.com/user-attachments/assets/9c6cf488-fe9b-4565-acc4-2ca23831769f)

![Screenshot from 2024-07-13 13-43-54](https://github.com/user-attachments/assets/ea06d845-d7c0-4527-b91f-db9ddc40e2f2)

To switch to root: ```sudo -i```

# Add a user to sudo group

```bash
sudo usermod -aG sudo <username>
```
- `-G` - to add as secondary group
- `-a` - append mode

# sudo password

Sudo password is only asked first time and cached for some time frame(default 15 minutes)
- https://unix.stackexchange.com/questions/442552/how-does-sudo-decide-whether-to-ask-for-a-password-when-given-a-command-which-d
- https://askubuntu.com/questions/814758/user-in-admin-group-still-being-prompted-for-password-to-sudo

How a user can run docker commands without sudo:
- https://medium.com/devops-technical-notes-and-manuals/how-to-run-docker-commands-without-sudo-28019814198f
- https://www.baeldung.com/linux/docker-run-without-sudo

So, there are 3 "issues":
1. We have to belong to sudo group
2. We have to use sudo prefix https://unix.stackexchange.com/questions/276474/how-can-i-execute-any-command-as-a-normal-user-without-sudo
3. We have to type sudo password

That a user is in sudo group doesn't mean you won't be asked password when running commands with sudo.

# Disable sudo password for a spesific user

**It is done by editing `/etc/sudoers` file with command `sudo visudo`.**

- https://www.youtube.com/watch?v=07LXPEHAyyg
- https://alexhost.com/faq/how-to-disable-the-password-for-the-sudo-command-in-linux/
- https://askubuntu.com/questions/147241/execute-sudo-without-password
- https://ostechnix.com/run-particular-commands-without-sudo-password-linux/

The `/etc/sudoers` file is a critical configuration file on Unix-like systems that controls which users or groups can run commands with superuser (root) privileges using the sudo command. It provides fine-grained control over who can execute commands as root or other users, and it also allows specifying which commands can be executed with elevated privileges.

# Some commands have to be run with sudo to "see" the whole information
![image](https://github.com/user-attachments/assets/71e1c785-6372-434d-af15-5cba9f1b5e1d)
![image](https://github.com/user-attachments/assets/0c219a13-ad87-4fb1-95f1-377db95da53e)

# Are a root user and a sudo user the same?

No, a **root user** and a **sudo user** are not the same, though they are closely related in terms of system privileges:

### 1. **Root User:**
   - The root user is the **superuser** on a Linux or Unix system, with **unrestricted access** to all commands, files, and system resources.
   - The root user can perform any task on the system, including changing any system files, creating or deleting other users, and controlling permissions.
   - It is the most powerful user account on a system, and operating directly as root can be dangerous if commands are misused.

### 2. **Sudo User:**
   - A sudo (short for "superuser do") user is a regular user who is **granted temporary root privileges** to run specific commands or access system resources that typically require root access.
   - **`sudo`** allows a user to elevate their privileges for certain tasks without logging in as the root user.
   - The sudo user's actions are usually logged, offering better accountability and security.

### Key Differences:
   - **Access:** The root user has full, always-on access, whereas a sudo user has temporary or limited access to root privileges.
   - **Security:** Direct use of the root user account is riskier because there are no restrictions or logging of actions, while sudo adds an extra layer of security by limiting access and logging actions.
   - **Convenience:** The sudo mechanism allows administrators to perform tasks without needing to fully switch to the root user, improving convenience and safety.

In general, it's best practice to use `sudo` for administrative tasks and avoid logging in as the root user unless absolutely necessary.

# Is there necessity to add `sudo` to `apt search <package>`?

No, there is **no necessity** to add `sudo` to the `apt search <package>` command. 

Here’s why:

- **`apt search`** only queries the local package cache and displays information about available packages. It does not modify your system in any way, so it does **not require elevated (root) permissions**.
- You can run `apt search` as a regular user, and it will work just fine.

### When to Use `sudo`:
- **`sudo`** is needed for commands that modify your system, such as:
  - **`sudo apt update`**: To update the package list (since it modifies the local package cache).
  - **`sudo apt install <package>`**: To install software (since it makes changes to your system by installing packages).
  - **`sudo apt upgrade`**: To upgrade installed packages.
  
### Summary:
- **`sudo` is not needed** for `apt search`, as it’s a read-only operation that doesn’t change your system.
- Use `sudo` only for commands that require administrative privileges, such as installing, updating, or upgrading packages.


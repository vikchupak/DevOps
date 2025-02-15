# passwd command

```bash
# When root or with sudo 
passwd username
```
If you have the necessary permissions (usually root or with sudo), you can change the password for another user.

# But it is not secure if I can change another user password?

Yes, allowing any user to change another user's password can pose significant security risks. However, there are built-in mechanisms in Linux to ensure that only authorized users (usually system administrators) can change passwords for other users. Here's how Linux handles this, along with ways to maintain security:

### Key Points on Password Security in Linux

1. **Permissions and Privileges:**
   - **Root Access:** Only the `root` user has the privilege to change any user's password. Regular users cannot change another user's password unless granted specific permissions.
   - **Using `sudo`:** Typically, changing another user's password requires `sudo` privileges. Users must be listed in the `/etc/sudoers` file to use the `sudo passwd username` command.

2. **Controlled Access with `sudo`:**
   - The `/etc/sudoers` file allows for fine-grained control over who can run specific commands as root. By carefully managing this file, you can limit which users have the ability to change passwords.
   - Example of a secure configuration:
     ```bash
     # Allow user 'admin' to change the password of 'johndoe' only
     admin ALL=(ALL) /usr/bin/passwd johndoe
     ```
   - This grants `admin` permission to change `johndoe`'s password without giving them the ability to change other users' passwords.

### Conclusion

While Linux provides mechanisms for password changes, the potential for abuse exists, particularly with root and sudo access. By carefully managing permissions, using the `/etc/sudoers` file, monitoring access, and enforcing password policies, you can maintain a secure environment that limits unauthorized access and password changes. Proper system administration practices are crucial for maintaining security.

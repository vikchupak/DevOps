# runuser command

```bash
runuser -l username -c "export APP_ENV=dev && npm install && node server.js &"
```
```bash
runuser -u username -c "/path/to/script.sh"
```
The `runuser` command in Linux allows you to run commands as another user without requiring the root user to enter the target user’s password. It is similar to su, but typically used in scripts and systemd services because it does not prompt for a password.

# But it is not secure if I can ran command from another user?

Yes, allowing unrestricted use of the `runuser` command could indeed be a security risk if not properly controlled. However, **`runuser` is generally restricted to the root user**, which mitigates the security concern. Let's break down why it's not insecure under typical circumstances and how to keep it secure:

### Why `runuser` is Usually Secure:

1. **`runuser` Can Be Used Only by `root`:**
   - The `runuser` command is designed to be used only by the `root` user. Non-root users cannot execute `runuser` to switch to another user without having root privileges.
   - This means that only the system administrator (root) can run commands as another user, and ordinary users cannot misuse it.

2. **Controlled Access by `sudo` and Permissions:**
   - Typically, access to `root` privileges is controlled by `sudo`. Non-root users need to be granted specific permissions in the `/etc/sudoers` file to use `sudo` to run commands as another user.
   - **Even if you allow certain users to execute specific commands with `sudo`, you can limit what commands they can run, preventing misuse.**

### Conclusion:
The `runuser` command is secure as long as it's restricted to the **root** user or users with carefully configured **sudo** permissions. It's important to control access to `runuser` (or commands like `sudo` that can invoke it) by ensuring that only trusted users can execute commands as other users.

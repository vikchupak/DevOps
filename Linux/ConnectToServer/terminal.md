# `~/.ssh` directory content
The `~/.ssh` folder typically contains files related to SSH (Secure Shell), including private and public keys used for authentication, as well as known hosts and configuration files. Here are some common files found inside the `~/.ssh` folder:

1. **`id_rsa`**: The default private key for SSH authentication. It should be kept secure and not shared with anyone.
2. **`id_rsa.pub`**: The public key that corresponds to the private key (`id_rsa`). This can be shared with remote systems to grant SSH access.
3. **`authorized_keys`**: A file that lists public keys that are allowed to SSH into the system. This file is used on the remote server to permit access to the user with matching private keys.
4. **`known_hosts`**: A list of servers the user has connected to via SSH. It contains their host keys and prevents man-in-the-middle attacks by verifying that the server has not changed.
5. **`config`**: An optional file for configuring SSH behavior, such as setting aliases for hosts, defining specific ports, or using different identity files for specific servers.
6. **`id_ed25519`**: A private key using the Ed25519 algorithm, an alternative to RSA. It's becoming more common for modern systems.
7. **`id_ed25519.pub`**: The corresponding public key for `id_ed25519`.

You can list the contents of your `~/.ssh` directory with the following command:

```bash
ls -la ~/.ssh
```

# Generate SSH keys
![image](https://github.com/user-attachments/assets/f39eb96f-403c-496f-9632-915c07ccf95d)

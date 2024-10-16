# `~/.ssh` directory content
The `~/.ssh` folder typically contains files related to SSH (Secure Shell), including private and public keys used for authentication, as well as known hosts and configuration files. Here are some common files found inside the `~/.ssh` folder:

1. **`id_rsa`**: The default private key for SSH authentication. It should be kept secure and not shared with anyone.
2. **`id_rsa.pub`**: The public key that corresponds to the private key (`id_rsa`). This can be shared with remote systems to grant SSH access.
3. **`authorized_keys`**: A file that lists public keys that are allowed to SSH into the system. This file is used on the remote server to permit access to the user with matching private keys.
4. **`known_hosts`**: A list of servers the user has connected to via SSH. It contains their **host keys** and prevents man-in-the-middle attacks by verifying that the server has not changed.
5. **`config`**: An optional file for configuring SSH behavior, such as setting aliases for hosts, defining specific ports, or using different identity files for specific servers.
6. **`id_ed25519`**: A private key using the Ed25519 algorithm, an alternative to RSA. It's becoming more common for modern systems.
7. **`id_ed25519.pub`**: The corresponding public key for `id_ed25519`.

You can list the contents of your `~/.ssh` directory with the following command:

```bash
ls -la ~/.ssh
```

![02_ssh config](https://github.com/user-attachments/assets/d4102020-ed54-4a3c-acfa-f5c9ab316689)

![image](https://github.com/user-attachments/assets/dc901e2e-c0bd-4b01-86f6-5b46451f82df)

# Host SSH keys (remote server keys | known_hosts file on client)
Host keys are cryptographic keys used by SSH (Secure Shell) servers to identify themselves to clients. They play a critical role in securing SSH connections by preventing man-in-the-middle attacks, ensuring that the client connects to the correct server. Here’s an overview of host keys and their purpose:

### 1. **Purpose of Host Keys:**
   - **Server Authentication**: When a client attempts to connect to a server via SSH, the server presents its host key. The client uses this key to verify that it is connecting to the intended server and not a malicious or unauthorized one.
   - **Prevent Man-in-the-Middle Attacks**: By validating the host key, the client ensures that no intermediary is impersonating the server, which would otherwise allow an attacker to intercept or manipulate the communication.

### 2. **Host Key on the Server Side:**
   - The SSH server generates a host key when it is first installed, and it is stored on the server (e.g., in `/etc/ssh/` directory). The server may have multiple host keys (one for each supported algorithm).
   - These keys are static and should not change frequently. If they do, for instance after a system reinstallation, the SSH client will notice the change and warn the user.

### 3. **Host Key Types:**
   - **RSA** (`ssh-rsa`): A widely used algorithm for host keys. It's being phased out in favor of more secure algorithms in newer systems.
   - **DSA** (`ssh-dss`): Another algorithm used for host keys but is deprecated due to weaker security.
   - **ECDSA** (`ecdsa-sha2-nistp256`, etc.): A newer elliptic-curve-based algorithm that is faster and more secure than RSA.
   - **Ed25519**: The most modern and recommended host key algorithm, offering fast performance and high security.

### 4. **Host Key Storage on the Client Side:**
   - On the client machine, SSH clients maintain a file called `known_hosts` (usually in the `.ssh` directory). This file stores the host keys of servers that the client has connected to in the past. When the client connects to a server again, it compares the server's host key with the key stored in `known_hosts` to verify its identity.
   - If the key has changed, SSH will issue a warning, and depending on the configuration, it might refuse to connect unless the change is manually confirmed by the user.

### 5. **Example: Known Hosts File on Client**
   The `~/.ssh/known_hosts` file contains entries like:

   ```
   server.example.com,192.168.1.10 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIBaZj6FeexydK12J...
   ```
   - This line contains the server’s hostname (`server.example.com`), IP address (`192.168.1.10`), key type (`ssh-ed25519`), and the base64-encoded public key.

### 6. **SSH Warning Example:**
   When connecting to a server for the first time, SSH may prompt:

   ```
   The authenticity of host 'server.example.com (192.168.1.10)' can't be established.
   RSA key fingerprint is SHA256:abc123...
   Are you sure you want to continue connecting (yes/no)?
   ```
   By typing "yes," the server’s host key is added to the `known_hosts` file.

If the server’s host key changes unexpectedly, SSH will display a warning like:

```
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
```
This could indicate either the server has been reinstalled or there is a potential attack, so caution is necessary.

In summary, host keys are critical to ensuring that SSH connections remain secure and trusted between clients and servers.

### Example how gitlab keys are added to clients known_hosts

![Screenshot from 2024-10-16 23-07-20](https://github.com/user-attachments/assets/9b0c9b6b-a9e5-4df4-bffa-00fef27a3f6a)

# Where to put `id_rsa.pub` on remote server (authorized_keys file on remote server)

Copy `id_rsa.pub` content to `~/.ssh/authorized_keys` on a remote server.\
If no folders/file exists create it.\
Probably, for securety reasons, it will be needed to to change folder and file permissions.\
**This key will be used to authenticate a specific user(the user in which home directory the file `~/.ssh/authorized_keys` is located).**

# Generate SSH keys
![image](https://github.com/user-attachments/assets/f39eb96f-403c-496f-9632-915c07ccf95d)

# Connect to a removte server
```bash
ssh <username>@<hostname|server_ip> -p <port> -i ~/.ssh/<public_keyname>
```
- port and path to a public key are optional unless they are not default ones

# Copy to and from a remote server
```bash
# Copy to remote
scp -P <port> <local_source_file> <username>@<hostname|server_ip>:<remote_target_dir> -i ~/.ssh/<public_keyname>
```
```bash
# Copy from remote
scp -P <port> <username>@<hostname|server_ip>:<remote_source_file> <local_target_dir> -i ~/.ssh/<public_keyname>
```

Note: in ssh, a port is specified with `-p(lower case)`, in scp with `-P(upper case)`  

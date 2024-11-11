# How CLI commands are executed

Example with docker CLI command `docker ps`

Docker commands are structured so that they consist of the main command and subcommands.

- `docker` - is the main command;
- `ps` - is a subcommand;

1. **Docker as a Command-Line Tool**: 
   - The `docker` command is the main entry point for interacting with Docker, much like how `git` is used for Git version control.

2. **`[docker] ps` as a Subcommand**:
   - `docker` provides many subcommands that perform different tasks, such as:
     - `[docker] run` to run a container
     - `[docker] build` to build a Docker image
     - `[docker] ps` to list running containers
     - `[docker] logs` to view container logs, and so on.

   Each of these actions is called a **subcommand** of the `docker` command. The `ps` subcommand specifically lists the running Docker containers.

3. **Namespace of Docker Commands**:
   - Just like other command-line tools (e.g., `git`, `kubectl`, `aws`), Docker organizes its functionality into different commands and subcommands. In this case:
     - **`docker`** is the main command that interfaces with Docker's functionalities.
     - **`ps`** is a subcommand of `docker` used to list containers.

*****
 If you were to try running just `ps`, it would not work unless the `ps` command was in your `$PATH` and intended to be run independently (for example, listing processes on a Linux system).

4. **System vs. Docker-specific Commands**:
   The `ps` command in the context of Docker is different from the standard Unix/Linux `ps` command, which lists processes on the operating system. When you run `docker ps`, you're asking Docker to list the containers it is managing, not the system processes.

   - **System `ps`**: Lists processes on your operating system (e.g., running programs).
   - **Docker `ps`**: Lists the containers running in Docker, which may or may not correspond directly to OS processes.

   Thus, to tell the system you're using Docker's functionality, you need to precede `ps` with `docker`.

*****

# Step by step explanation

### 1. **Command Parsing and Execution Flow**

When you enter `docker ps` in the terminal, the system performs the following steps:

- **Shell Process**: You type `docker ps` in your terminal. The shell (like Bash) first looks for the `docker` command, which is typically located in a directory listed in the `$PATH` environment variable (e.g., `/usr/bin/docker`).
  
- **Command Execution**: The shell invokes the `docker` binary found in the `$PATH`. This binary is the Docker CLI (command-line interface), which is a program designed to interact with the Docker daemon (the background service responsible for managing containers, images, networks, etc.).

### 2. **Docker CLI and Subcommand Parsing**

- **Docker CLI**: Once the Docker CLI is invoked, it starts parsing the command you entered. It checks if `ps` is a valid subcommand of `docker`.
  
- **Argument Parsing**: The `docker ps` command can also accept additional flags or arguments (e.g., `docker ps -a` to show all containers, `docker ps -q` to show just container IDs). The Docker CLI will parse these options and prepare the appropriate arguments for further processing.

### 3. **Docker Daemon Communication**

- **Client-Server Model**: Docker follows a **client-server architecture**. The Docker CLI (the client) communicates with the Docker daemon (the server) to perform tasks like managing containers, images, networks, etc. The daemon is usually running as a background service (typically as `dockerd`).
  
- **Request to Docker Daemon**: When you run `docker ps`, the Docker CLI sends a request to the Docker daemon via a **REST API** (usually over a Unix socket, e.g., `/var/run/docker.sock`, or over HTTP if configured for remote access).

    The request sent to the Docker daemon is asking for the list of containers that are currently running (if no other options like `-a` are used).

### 4. **Docker Daemon Processing**

- **Querying Container Data**: The Docker daemon processes the request by accessing its internal container management system. Docker keeps track of containers' states in a database-like structure or memory. The daemon checks which containers are running, stopped, or paused.
  
- **Container Information Retrieval**: The daemon gathers information about containers and then formats this information, which will be returned to the Docker CLI.

### 5. **Response to Docker CLI**

- **Return Data**: The Docker daemon sends the response back to the Docker CLI. This response contains the relevant data about running containers.
  
- **Formatting the Output**: The data returned by the daemon is structured (typically as JSON), and the Docker CLI formats this into a user-friendly table-like format (or a more concise format if specified). For example, `docker ps` might output something like:

  ```
  CONTAINER ID   IMAGE     COMMAND       CREATED       STATUS       PORTS     NAMES
  abc123456789   ubuntu    "/bin/bash"   2 hours ago   Up 2 hours   80/tcp    vibrant_wozniak
  def987654321   nginx     "nginx -g..." 3 hours ago   Up 3 hours   443/tcp   epic_thompson
  ```

### 6. **Displaying the Output**

- **CLI Output**: The formatted output is then printed back to your terminal window, so you can see the list of containers, their status, and other relevant details.

- **Shell Interaction**: Once the data is printed to your terminal, control is returned to the shell, which is ready to accept new commands.

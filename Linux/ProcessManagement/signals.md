### 1. About signals
https://www.youtube.com/watch?v=lP7xoqkqDZQ

__Processes communicate with each other through signals.__

`kill -l` list all the signals supported by your system\
https://www.javatpoint.com/linux-signals

![image](https://github.com/user-attachments/assets/72917cc7-0a6c-4433-90bf-9e797f6e5052)

__trap__\
Normally, we use trap to process signals.
- Trapping Signals https://www.tutorialspoint.com/unix/unix-signals-traps.htm
- trap with exit  https://www.baeldung.com/linux/return-vs-exit#using-the-trap-command-with-exit

# What are signals in Linux?

In Linux, **signals** are a mechanism used by the operating system to notify or interrupt processes when certain events occur.\
Signals can be sent by:
- the operating system
- the user
- other processes

and they are used for:
- inter-process communication (IPC)
- error handling
- controlling processes

Each signal represents a specific event, such as a process termination request, a pause instruction, an exception (like division by zero). Signals are identified by a **name** (e.g., `SIGTERM`) and a corresponding **number** (e.g., `15` for `SIGTERM`).

When a process receives a signal, it typically performs some action depending on the signal type. This action can be:
 - **Terminating**: The process stops execution.
 - **Pausing**: The process temporarily halts.
 - **Ignoring**: The process ignores the signal (if allowed).
 - **Handling**: The process runs a custom signal handler (if one is defined) to manage the signal in a specific way.

### Signal Management Commands:

1. **kill**:
   - Sends signals to processes.
   ```bash
   kill -9 <PID>  # Send SIGKILL (forcefully terminate)
   kill -15 <PID> # Send SIGTERM (gracefully terminate)
   ```

2. **killall**:
   - Sends signals to all processes matching a name.
   ```bash
   killall -9 myprocess  # Sends SIGKILL to all instances of "myprocess"
   ```

3. **pkill**:
   - Similar to `killall`, but allows more flexible process selection.
   ```bash
   pkill -f myscript.sh  # Sends signal to all processes matching the script name
   ```

4. **trap** (in shell scripting):
   - Used to catch signals and define custom signal handlers in shell scripts.
   ```bash
   trap 'echo "Caught SIGINT, exiting"; exit' SIGINT
   ```

### Summary:
- Signals are a way to communicate with processes in Linux, used to control processes and handle events such as termination, pausing, and error handling.
- There are different types of signals, each with a specific purpose, such as `SIGTERM` (graceful termination), `SIGKILL` (forceful termination), and `SIGINT` (interrupt from keyboard).
- Signals can be sent manually using commands like `kill` or automatically by the system in response to events such as segmentation faults or user interrupts.

# Trap

The `trap` command in Linux is used to **capture and handle signals in shell scripts**. By using `trap`, **you can specify custom actions** (such as executing commands or functions) to take when a script receives specific signals.

### How `trap` Works:
- `trap` allows you to define **signal handlers**—specific actions that the shell should execute when it receives certain signals.
- Without `trap`, a signal like `SIGINT` (sent by pressing `Ctrl+C`) would terminate a script immediately. By using `trap`, you can intercept the signal and take actions before terminating or even ignore it.

### Syntax:
```bash
trap 'commands' signal(s)
```
- **`commands`**: The command(s) or action(s) to run when the specified signal is received.
- **`signal(s)`**: One or more signals that trigger the commands. These can be signal names like `SIGINT`, `SIGTERM`, or `EXIT`.

### Example Scenarios for `trap`:

1. **Gracefully Handle `Ctrl+C` (SIGINT)**:
   When you press `Ctrl+C` during a running script, the `SIGINT` signal is sent. You can use `trap` to handle this signal and perform cleanup or exit gracefully.

```bash
#!/bin/bash

trap 'echo "Script interrupted! Cleaning up..."; rm -f /tmp/tempfile; exit' SIGINT

echo "Running script..."
touch /tmp/tempfile
sleep 60  # Simulating a long-running process
```

- When you press `Ctrl+C` while this script is running, it will:
  1. Print "Script interrupted! Cleaning up..."
  2. Remove the temporary file `/tmp/tempfile`
  3. Exit gracefully

2. **Clean Up on Script Exit (`EXIT` Signal)**:
   The `EXIT` signal is special—it’s not tied to user signals but is triggered when the script finishes, either normally or due to an interrupt. This can be used to ensure that certain cleanup actions always occur, regardless of how the script ends.

```bash
#!/bin/bash

trap 'rm -f /tmp/tempfile; echo "Script finished, cleaned up!"' EXIT

echo "Creating temporary file..."
touch /tmp/tempfile
sleep 10  # Simulating work
echo "Work done."
```

- When the script finishes (either naturally or interrupted), the `trap` command will:
  1. Remove `/tmp/tempfile`
  2. Print "Script finished, cleaned up!"

3. **Ignore a Signal**:
   You can use `trap` to **ignore signals**. This can be useful in scripts where you don’t want the script to be interrupted by `SIGINT` or other signals.

```bash
#!/bin/bash

trap '' SIGINT  # Ignore Ctrl+C (SIGINT)

echo "Try pressing Ctrl+C. The script will not be interrupted."
sleep 10
echo "Script completed."
```

- Pressing `Ctrl+C` during the script’s execution will not stop the script because `SIGINT` is ignored.

4. **Resetting a Trap**:
   You can reset a signal handler back to its default action by using `trap` with an empty string.

```bash
trap - SIGINT  # Reset SIGINT to its default behavior
```

5. **Multiple Signals in One `trap`**:
   You can handle multiple signals with a single `trap` by listing them together.

```bash
trap 'echo "Received SIGINT or SIGTERM! Exiting..."; exit' SIGINT SIGTERM
```

- This will trigger the same action for both `SIGINT` (interrupt) and `SIGTERM` (termination request).

### Useful Signals with `trap`:
1. **`SIGINT`** (`2`): Interrupt signal, typically sent by pressing `Ctrl+C`. Commonly used for stopping a running script.
2. **`SIGTERM`** (`15`): Termination signal, often sent by commands like `kill`. It’s used to request a graceful shutdown of a process.
3. **`SIGQUIT`** (`3`): Sent by pressing `Ctrl+\`. It can generate a core dump.
4. **`SIGTSTP`** (`20`): Sent by pressing `Ctrl+Z`, used to pause (suspend) a process.
5. **`EXIT`**: Triggered when the script exits, either because it finished or was terminated.
6. **`ERR`**: Triggered when a command fails (returns a non-zero exit code), often used for error handling in scripts.
7. **`DEBUG`**: Triggered before every command in the script, useful for debugging purposes.
8. **`SIGHUP`** (`1`): Sent when a terminal is closed or a user logs out, often used to reload configurations in daemons.

### Advanced Example: Clean Up on `SIGINT` and `SIGTERM`
Here’s a more complex example that handles both `SIGINT` and `SIGTERM`, cleans up, and gracefully exits.

```bash
#!/bin/bash

cleanup() {
    echo "Caught signal. Cleaning up..."
    rm -f /tmp/tempfile
    exit
}

trap cleanup SIGINT SIGTERM  # Handle Ctrl+C and termination

echo "Running script. Press Ctrl+C to stop."
touch /tmp/tempfile
while true; do
    sleep 5
    echo "Working..."
done
```

- This script will:
  - Handle `SIGINT` (Ctrl+C) and `SIGTERM` (termination) using the `cleanup` function.
  - Remove the temporary file `/tmp/tempfile` when interrupted.
  - Exit the script gracefully.

### Summary:
- **`trap`** allows you to intercept signals like `SIGINT`, `SIGTERM`, and `EXIT` to run custom commands or scripts.
- It’s commonly used for **cleanup tasks**, handling interrupts, or ensuring that scripts exit gracefully.
- You can use `trap` to **ignore** signals, **reset** signal handlers, or manage multiple signals with a single handler.

By using `trap` effectively, you can make your scripts more robust and handle unexpected events gracefully.

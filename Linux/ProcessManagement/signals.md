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

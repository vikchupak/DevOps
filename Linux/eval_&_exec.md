# eval

https://www.geeksforgeeks.org/eval-command-in-linux-with-examples/

```bash
eval "pwd; echo Hello $USER; date"

/home/joe
Hello joe
Sun Mar 27 01:01:06 PM EDT 2022
```

# exec
https://developnsolve.com/understanding-the-linux-exec-command-with-practical-examples

Sure! The `exec` command is a built-in shell command that replaces the current shell process with a new process. When you run a command in a shell (like Bash), the shell normally creates a new process (a child process) to execute that command. However, when you use `exec`, the shell does not create a new process. Instead, it replaces the current shell process with the process of the command you want to execute.

Here’s a more detailed explanation:

1. **Normal Command Execution**:
   - When you run a command normally (e.g., `ls`), the shell forks a new process (child process) and the `ls` command runs in this new process.
   - The shell waits for the child process to finish.
   - Once the child process completes, the shell resumes control.

2. **Using `exec`**:
   - When you use `exec ls`, the shell itself is replaced by the `ls` process.
   - There is no child process; the original shell process now becomes the `ls` process.
   - Once the `ls` process completes, there is no shell process to return to, because it has been replaced.

### Example:

Consider the following script:

```sh
#!/bin/bash
echo "Before exec"
exec ls
echo "After exec"
```

- When you run this script, you will see the output of the `ls` command, but you will **not** see "After exec" because the shell running the script is replaced by the `ls` command process. 
- After `ls` completes, there is no shell process to continue the script, so the script ends.

### Practical Use:

- `exec` can be useful in scripts or system administration tasks where you want to replace the current process without creating a new one, such as replacing the current shell with a different one, or when chaining commands without creating additional processes.

### Summary:

Using `exec` effectively replaces the current shell process with the specified command, meaning the original shell process ceases to exist and there is no return to the shell after the command completes. This is different from the usual way commands are executed, where the shell forks a new child process to run the command.

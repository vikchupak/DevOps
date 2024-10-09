File descriptors for I/O streams:\
https://en.wikipedia.org/wiki/File_descriptor

- 0 is stdin
- 1 is stdout (default, so ```ls > ls.out``` equals ```ls 1> ls.out```
- 2 is stderr

``ls -l /proc/$$/fd`` list file descriptors

![image](https://github.com/user-attachments/assets/7649036a-5f6d-4947-9322-27c648ac3470)

https://medium.com/@emilycoco/what-are-stdout-stdin-and-stderr-2d6d27892c38#:~:text=Stdout%20and%20stderr%20point%20to,displayed%20in%20your%20terminal%20screen.
![Screenshot from 2024-07-12 17-05-56](https://github.com/user-attachments/assets/8748eece-d960-423d-8a3e-2d4a78c4d986)

https://www.geeksforgeeks.org/input-output-redirection-in-linux/
![Screenshot from 2024-07-12 17-08-09](https://github.com/user-attachments/assets/b8fea078-45b8-4068-9e2f-d8219eb0d790)

Redirections:

- ```>``` (Output redirection)
- ```>>``` (Append stdout redirection) ```ls 1>> ls.out```
- ```<``` (Input redirection)
- ```<<``` (Append stdin redirection)
- ```<<<``` (Here string, input redirection - passes as input only first line, the others will be ignored)\
  https://linuxhandbook.com/here-input-redirections/
- ```<<DELIMITER``` (Here document, input redirection - passes as input all lines)\
  https://linuxhandbook.com/here-input-redirections/ \
  ```<<-DELIMITER``` (Here Document with tab suppression, input redirection - passes as input all lines and only leading tabs are suppressed; if you have spaces, they will be preserved)\
  https://phoenixnap.com/kb/bash-heredoc
- ```>&descriptor``` (Redirect to file descriptor, example `2>&1` => redirect stderr to stdout)\
  https://stackoverflow.com/questions/818255/what-does-21-mean
- ```>& or &>``` (Merge redirect, descriptor 1 and 2 are merged. Special case) ```&>/dev/null```
  https://www.gnu.org/software/bash/manual/bash.html#Redirections
  ![image](https://github.com/user-attachments/assets/4163770a-6b01-4d00-a939-f0cf168a944a)

Piping
- ```|``` (redirects stdout of an app to stdin of another app)

# Tricky case

`java -version` - outputs the version information to the **stderr (stream 2)**. So `java -version | grep "openjdk version"` piping won't work.

### Solution:
`java -version 2>&1 > /dev/null  | grep "openjdk version"` - this will redirect **only stderr** to the pipe.

### Explanation:
1. When you run `java -version`, the version information is output to **stderr (stream 2)**, not stdout.
2. `2>&1`: Redirects **stderr (stream 2)** to **stdout (stream 1)**, so now stderr points to the same destination that stdout.
3. `> /dev/null`: Redirects **stdout (stream 1)** to `/dev/null`, discarding it.
4. Wnen **stdout (stream 1)** is redirected to `/dev/null`, only **stderr (stream 2)** (which has been redirected to stdout) remains available for the pipe.

So, we can redirect many streams to a file descriptor, and the strems remain separate but their output printed in the file descriptor.\
So it "looks" like streams are merged, but it is NOT so.

## So after redirections fds are pointing to same destination, but fd1 and fd2 continue to exist on their own?

Exactly! After redirections, **file descriptors (`fd`) 1 (stdout) and 2 (stderr)** continue to exist independently, even though they may point to the same or different destinations. The key thing to understand is that when you use redirection, you're changing where those descriptors point, but the descriptors themselves remain separate.

Let’s dive a bit deeper into this concept.

### File Descriptors and Redirection

- **File descriptors** (like `1` for stdout and `2` for stderr) are essentially "pointers" that tell the system where to send the output.
- When you redirect a file descriptor (using redirections like `>`, `2>`, `&>`, etc.), you're telling the shell to change where that file descriptor points, but it still exists as its own entity.

### What Happens After Redirection?

Let’s take a closer look at the behavior of the redirection.

1. **Without Redirection**:
   - `fd1 (stdout)` → terminal (normally, output goes to the screen).
   - `fd2 (stderr)` → terminal (normally, error messages also go to the screen).

2. **After `2>&1`**:
   - `fd2 (stderr)` is now redirected to wherever `fd1` (stdout) is currently pointing (which is still the terminal at this point).
   - **However, `fd2` is still its own entity**. It just happens to point to the same destination as `fd1`.

3. **After `> /dev/null`**:
   - Now, `fd1 (stdout)` is redirected to `/dev/null` (meaning normal output is discarded).
   - `fd2 (stderr)` continues to point to where `fd1` was pointing **before** (which was the terminal).
   - Thus, even though `fd2` was temporarily redirected to match `fd1`, it is still a **separate descriptor** that keeps pointing to the terminal (because it was redirected before stdout was sent to `/dev/null`).

### So, to clarify:

- **fd1 (stdout)** and **fd2 (stderr)** remain separate, independent file descriptors.
- Redirection only changes where each descriptor points (their **destination**), but it doesn’t merge them into a single descriptor.
- Even after redirections, `fd1` and `fd2` still exist as separate entities. The redirection just changes where they point (i.e., where the output or errors go). When you use `2>&1`, it doesn’t combine or merge them into one; it just synchronizes their destinations **at that moment**, but they still exist independently.

# Commands not reading from standard input. Command substitution vs `xargs` command

`xargs` is a command-line utility in Unix/Linux systems that is used to build and execute command lines from standard input. It allows you to take output from one command and use it as arguments for another command. This is particularly useful when **dealing with commands that do not accept standard input directly but can take multiple arguments**.

### Key Features of `xargs`:
1. **Argument Handling**: `xargs` takes input from the standard input (stdin) and converts it into arguments for a specified command.
2. **Handling Multiple Arguments**: It can process multiple lines of input and provide them as arguments to a command.
3. **Efficiency**: Instead of running a command for each line of input separately, `xargs` can batch the arguments together, making it more efficient.
4. **Customizable Behavior**: You can specify delimiters, control the number of arguments passed to each invocation of the command, and handle other options.

### Basic Syntax
```bash
command | xargs [options] command_to_run
```

### Basic Usage
```bash
echo "file1.txt file2.txt file3.txt" | xargs rm
```
In this example:
- `echo` produces a list of filenames.
- `xargs` takes those filenames and passes them as arguments to the `rm` command, effectively running `rm file1.txt file2.txt file3.txt`.

#### Using a Custom Delimiter
By default, `xargs` treats whitespace as a delimiter. You can change the delimiter using the `-d` option. For example, if your input is comma-separated:
```bash
echo "file1.txt,file2.txt,file3.txt" | xargs -d ',' rm
```
In this case, `xargs` uses the comma as the delimiter and deletes the specified files.

#### Limiting the Number of Arguments passed at once
You can limit how many arguments are passed to the command at once using the `-n` option:
```bash
echo "a b c d e" | xargs -n 2 echo
```
This will output:
```
a b
c d
e
```
Here, `xargs` takes two arguments at a time and runs `echo` with them.

#### With `find`
You can use `xargs` with `find` to process files:
```bash
find . -name "*.log" | xargs rm
```
This command finds all `.log` files in the current directory and its subdirectories and deletes them using `rm`.

### Summary:
- **`xargs`** is a powerful tool for transforming input into arguments for other commands.
- It enhances efficiency by allowing batch processing of arguments instead of executing commands individually for each line of input.
- You can customize its behavior with various options to handle delimiters, limit argument counts, and work with special characters.


The command below will not work as intended. Here's why:

```bash
echo "file1.txt file2.txt file3.txt" | rm
```

- `echo "file1.txt file2.txt file3.txt"` generates a string containing the filenames separated by spaces.
- The output of the `echo` command is sent to the `rm` command via a **pipe (`|`)**.

### Why It Doesn't Work:
- The `rm` command does not read from standard input when it's used in this way. It expects filenames as command-line arguments directly, not from stdin.
- As a result, `rm` won't see the filenames and will simply return an error or do nothing.

### Correct Way to Use `rm` with Filenames from `echo`:
To use the output of `echo` correctly with `rm`, you can use command substitution or use `xargs`:

#### Option 1: Using Command Substitution
You can execute the command like this:
```bash
rm $(echo "file1.txt file2.txt file3.txt")
```
- Here, the `$(...)` syntax executes the `echo` command and substitutes its output directly into the `rm` command as arguments.

#### Option 2: Using `xargs`
You can use `xargs` as previously discussed:
```bash
echo "file1.txt file2.txt file3.txt" | xargs rm
```
- In this case, `xargs` takes the output from `echo` and passes it as arguments to the `rm` command.

### Conclusion:
To summarize, while piping the output of `echo` directly to `rm` does not work because `rm` does not read from stdin in this context, using either command substitution or `xargs` will allow you to achieve the desired result of deleting the specified files.

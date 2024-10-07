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
- ```<<``` (Here document, input redirection)\
  https://linuxhandbook.com/here-input-redirections/ \
  ```<<-``` (Here Document with tab suppression, input redirection) \
  https://phoenixnap.com/kb/bash-heredoc
- ```<<<``` (Here string, input redirection)\
  https://linuxhandbook.com/here-input-redirections/
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

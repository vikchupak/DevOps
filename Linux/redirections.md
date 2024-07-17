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
- ```>&descriptor``` (Redirect to file descriptor)\
  https://stackoverflow.com/questions/818255/what-does-21-mean
- ```>& or &>``` (Merge redirect, descriptor 1 and 2 are merged. Special case) ```&>/dev/null```
  https://www.gnu.org/software/bash/manual/bash.html#Redirections

Piping
- ```|``` (redirects stdout of an app to stdin of another app)

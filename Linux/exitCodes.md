https://www.geeksforgeeks.org/how-to-use-exit-code-to-read-from-terminal-from-script-and-with-logical-operators/ \
List of codes\
https://www.cyberciti.biz/faq/linux-bash-exit-status-set-exit-statusin-bash/

# If statement
- https://unix.stackexchange.com/questions/22726/how-to-conditionally-do-something-if-a-command-succeeded-or-failed

When a command or condition returns exit code 0 ```inside if statement```, then it considered true, and any non 0 exit code considered false.

- Command is just executed as usual. We can suppress logs and errors with ```&>/dev/null```
  ```bash
  if command &>/dev/null; then #...
  ```
- Condition is checked with test utility https://ru.wikipedia.org/wiki/Test
  ```bash
  if test 5 -gt 0; then #...
  # or
  if [ 5 -gt 0 ]; then #...
  ```
  ![image](https://github.com/user-attachments/assets/a46ca560-1d9d-45c9-96ac-c26d104c12e7)

# Return vs Exit
Return sets __exit code__ for a function and immediately exits from the function.\
Exit sets __exit code__ for a whole script and immediately exits from the script.\
https://www.baeldung.com/linux/return-vs-exit

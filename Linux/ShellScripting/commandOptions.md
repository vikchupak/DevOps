### Double-Dash special delimiter, possible names:
- end of command options
- end of command flags

Useful links
- https://unix.stackexchange.com/questions/11376/what-does-double-dash-double-hyphen-mean
- https://www.cyberciti.biz/faq/what-does-double-dash-mean-in-ssh-command/
- https://www.baeldung.com/linux/double-dash-in-shell-commands

### Options with Single-Dash and Double-Dash

1. **Single Dash (`-`)**:
   - Used for **short options** (single-character options), typically followed by one or more letters/flags.
   - Often allows options to be **combined** when they are single characters. For example:
     ```bash
     ls -a -h
     ```
     can be combined as:
     ```bash
     ls -ah
     ```

2. **Double Dash (`--`)**:
   - Used for **long options** (multi-character options with descriptive names, making commands more readable).
   - Cannot be combined:
     ```bash
     ls --all --human-readable
     ```

![image](https://github.com/user-attachments/assets/568c5fad-135a-4d70-874b-03a95c64ea5d)

Useful links
- https://serverfault.com/questions/387935/whats-the-difference-between-the-single-dash-and-double-dash-flags-on-shell-com

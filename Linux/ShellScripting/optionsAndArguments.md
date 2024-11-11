## What can accept options and arguments
- commands
- functions
- scripts

## General
- **Options are NOT positional**
- **Argument are positional**
- **Options modify the behavior of a command/function/script**
- **Best practice to place options before arguments** [though, in many cases, the order doesn't matter]

## About options
**Double-Dash special delimiter, possible names:**
- end of command options
- end of command flags

**A double-dash in a shell command signals the end of options and disables further option processing.**

Useful links
- https://unix.stackexchange.com/questions/11376/what-does-double-dash-double-hyphen-mean
- https://www.cyberciti.biz/faq/what-does-double-dash-mean-in-ssh-command/
- https://www.baeldung.com/linux/double-dash-in-shell-commands

**Options with Single-Dash and Double-Dash**

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

## How to make arguments named

There are ways to pass argumets as named using options/flags.

### Real examples

```bash
sudo openconnect --user=example.user --server=vpn.example.com
```
```bash
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -H "Content-Type: application/json" \
  -H "Connection: keep-alive" \
  -d '{"title":"foo","body":"bar","userId":1}'
```

**In general, options are parsed and the parsed option values are used as arguments.**

******

**Parsing implementation in format --user=value**

To handle arguments like `--user=example.user` in a shell script, where the argument is passed as a key-value pair (e.g., `--user=value`), you can read and process these arguments explicitly in a way similar to how options are passed in commands like `openconnect`.

### Example: Reading Arguments Like `--user=example.user`

```bash
#!/bin/bash

# Initialize variables
user=""
host=""

# Parse the arguments
while [[ $# -gt 0 ]]; do
  case "$1" in
    --user=*)
      user="${1#--user=}"  # Remove --user= from the argument to get the value
      shift  # Move to the next argument
      ;;
    --host=*)
      host="${1#--host=}"  # Remove --host= from the argument to get the value
      shift
      ;;
    *)
      echo "Unknown option: $1"
      exit 1
      ;;
  esac
done

# Print the captured values (for demonstration purposes)
echo "User: $user"
echo "Host: $host"
```

### Usage:

```bash
./script.sh --user=example.user --host=192.168.1.1
```

Output:
```
User: example.user
Host: 192.168.1.1
```

### Notes:
- The script can easily be extended to handle more options by adding more `case` conditions.
- This method allows you to accept non-positional arguments in a flexible and structured way, similar to how commands like `openconnect` use named options (`--user=example.user`).

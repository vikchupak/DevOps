```bash
declare [-aAfFgiIlnrtux] [-p] [name[=value] ...]
```

Declare variables and give them attributes. If no NAMEs are given, display the attributes and values of all variables.

Options:
- ```-f``` restrict action or display to function names and definitions
- ```-F``` restrict display to function names only (plus line number and source file when debugging)
- ```-g``` create global variables when used in a shell function; otherwise ignored
- ```-I``` if creating a local variable, inherit the attributes and value of a variable with the same name at a previous scope
- ```-p``` display the attributes and value of each NAME

Options which set attributes:
- ```-a``` to make NAMEs indexed arrays (if supported)
- ```-A``` to make NAMEs associative arrays (if supported)
- ```-i``` to make NAMEs have the `integer' attribute
- ```-l``` to convert the value of each NAME to lower case on assignment
- ```-n``` make NAME a reference to the variable named by its value
- ```-r``` to make NAMEs readonly
- ```-t``` to make NAMEs have the `trace' attribute
- ```-u``` to convert the value of each NAME to upper case on assignment
- ```-x``` to make NAMEs export

```bash
declare -A person=(
    [name]='John'
    [city]='New York'
    [job]='Software Engineer'
)
```
- ```echo $person``` __echo will not print arrays correctly__
- ```declare -p``` виведе змінні такі як скалярні(string or integer), масиви, асоціативні масиви
- ```declare -F``` виведе список функцій

```bash
myvar="Hello, World!"
declare -p myvar
# Output
# declare -- myvar="Hello, World!"
# Here the output '--' means that myvar is a string
```

### Null vs unset
![NULL(just_empty_string)_and_unset](https://github.com/user-attachments/assets/be19b45b-a4cf-4049-834a-639bf9839585)

**Null string - string the length of zero. If value is not given, the variable is assigned the null string.** By default unset(not existing) vars are assigned null string on the fly while being substituted.
- https://unix.stackexchange.com/questions/280430/are-the-null-string-and-the-same-string
- https://stackoverflow.com/questions/10733317/whats-a-null-string-in-bash

### `set` command
- A built-in shell command used to set or unset values of ___shell options___ and positional parameters.
- `set -u; echo $var` > bash: var: unbound variable

# Boolean

Shell scripting (like `bash`, `sh`, or `zsh`) doesn’t have explicit **boolean** values like `true` or `false` found in many programming languages. Instead, it relies on **exit statuses** of commands to represent **truth** and **falsehood**.

### How Booleans Work in Shell:

In shell scripting, the concept of **truth** and **falsehood** is represented by:
- **Success (True)**: A command exits with status **`0`**.
- **Failure (False)**: A command exits with a **non-zero** exit status.

### `true` and `false` Commands in Shell:
The `true` and `false` commands in most shells always return specific exit statuses:
- `true` returns an exit status of `0` (success).
- `false` returns an exit status of `1` (failure).

These commands can be used to explicitly return "true" or "false" in a script.

Example:
```bash
if true; then
    echo "This is always true"
fi

if false; then
    echo "This will never run"
fi

while true
    do
        echo "Infinite loop"
    done
```

### Summary:
- In shell scripts, boolean values are represented by **exit statuses**: `0` for success (true), and non-zero for failure (false).
- You can simulate boolean variables with the built-in `true` and `false` commands.
- Conditionals and loops often rely on these exit statuses to determine "truth" or "falsehood."

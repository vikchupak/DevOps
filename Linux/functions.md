# Ways to declare a func

1. **Basic Function Declaration (Preferred in `bash`)**:
   This is the most common and widely-used way to define a function in modern shells like `bash`.

   ```bash
   function_name() {
       # commands
   }
   ```

2. **Using `function` Keyword (Alternative Syntax)**:
   Some shells, like `bash` and `zsh`, also allow using the `function` keyword to define a function.

   ```bash
   function function_name {
       # commands
   }
   ```

3. **Using `function` Keyword with Parentheses**:
   In `bash`, you can combine the `function` keyword and parentheses. This style is not recommended as it mixes different syntaxes, but it is valid in `bash`.

   ```bash
   function function_name() {
       # commands
   }
   ```

### Returning Values from Functions:
In shell scripting, functions don't return values like in many programming languages. Instead:
- The `return` command is used to return an **exit status** (0 for success, non-zero for failure).
- To return a computed value, you can use **`echo`** to print the result, which can then be captured by the caller.

Example:

```bash
add() {
    result=$(( $1 + $2 ))
    echo $result   # Return the result via echo
}

sum=$(add 5 10)   # Capture the output of the function
echo "Sum: $sum"  # Output: Sum: 15
```

### Exit Status in Functions:
- A function's exit status is the exit status of the **last command** it executed, unless overridden by the `return` statement.
  
Example:

```bash
check_file_exists() {
    if [[ -f "$1" ]]; then
        return 0  # Success
    else
        return 1  # Failure
    fi
}

check_file_exists "/path/to/file"
if [[ $? -eq 0 ]]; then
    echo "File exists."
else
    echo "File does not exist."
fi
```

### Summary:
- Functions in shell scripting are defined with or without the `function` keyword.
- Most commonly used syntax: `function_name() { commands }`.
- You can call functions by using their names and pass arguments.
- Functions can return values via `echo` and set exit statuses using `return`.

#

Shell functions do not return common values\
https://stackoverflow.com/questions/8742783/returning-value-from-called-function-in-a-shell-script \
But exit codes with return satatemant https://github.com/VIK2395/DevOps/blob/main/Linux/exitCodes.md#return-vs-exit

Function arguments\
https://stackoverflow.com/questions/6212219/passing-parameters-to-a-bash-function

Variable scopes\
![image](https://github.com/user-attachments/assets/cc846aff-073c-406a-8f97-23af2d29c78f)

Arguments are positional, but there are "tricks" with flags to make arguments named

Call function with arguments\
https://tecadmin.net/create-bash-functions-with-arguments/
```bash
someFunc arg1 arg2
```

Run sh script with arguments\
https://www.baeldung.com/linux/use-command-line-arguments-in-bash-script
``` bash
sh someScript.sh john 25 'John Smith'
```

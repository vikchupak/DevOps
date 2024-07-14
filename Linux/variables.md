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
declare -A associative_array=(
  ["key1"]="value1",
  ["key2"]="value2",
  ["key3"]="value3")
```

- ```declare -p``` виведе змінні такі як скалярні(string or integer), масиви, асоціативні масиви
- ```declare -F``` виведе список функцій

```bash
myvar="Hello, World!"
declare -p myvar
# output
declare -- myvar="Hello, World!"
# Here the output 'declare --' means that myvar is a string
```

```bash
# Without quotes white spaces are replaced by a sinqle white space
echo Some     string \\n with special char \*
# Some string \n with special char *
```
```bash
# Double quotes keep white spaces
echo "Some     string \n with new line"
# Some     string \n with new line
```
```bash
# -e - enable interpretation of backslash escapes (\n, \t, etc.)
echo -e "Line1\nLine2"
# Line1
# Line2
```
```bash
# Single quotes can be used to escape special characters
echo 'Special           symbols: " \'
# Special           symbols: " \

# Or inside double quotes, \ can be used to escape special characters
echo "Special           symbols: \" \\"
# Special           symbols: " \

# No varible expansion works inside single quotes
echo 'var="$var"'
# var="$var"
```

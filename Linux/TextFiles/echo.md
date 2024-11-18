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

![photo_2024-05-19_19-12-483](https://github.com/user-attachments/assets/c0b79644-3f02-4e98-b114-0eb1e8d71681)

![photo_2024-05-19_12-22-52](https://github.com/user-attachments/assets/764fa1b1-adca-4f72-a850-c8f441e4fa42)

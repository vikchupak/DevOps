# bash command

```
bash [options] [file | command_string]
```

The bash command "expects" a file/script as an input
```bash
bash script.sh
```

To pass a command we need to add -c option:
```bash
bash -c 'echo $0 $1' _ 5
# output: _ 5
```

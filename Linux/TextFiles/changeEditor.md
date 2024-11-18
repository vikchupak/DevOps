How to change default cli text editor\
https://askubuntu.com/questions/615178/getting-the-default-text-editor-used-in-system

List available editors
```bash
update-alternatives --list editor
```
Set editor for current terminal session
```bash
export EDITOR=nano
```

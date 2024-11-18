## How to change default cli text editor
- https://askubuntu.com/questions/615178/getting-the-default-text-editor-used-in-system
- https://unix.stackexchange.com/questions/470561/open-default-text-editor-from-terminal

List available **terminal-based** editors
```bash
update-alternatives --list editor
```
Set **terminal-based** editor for current terminal session.\
To set the editor for a spesific user for all sessions, add to `~/.bashrc` file
```bash
export EDITOR=nano
```
Set **terminal-based** editor system-wide
```
sudo update-alternatives --config editor
```

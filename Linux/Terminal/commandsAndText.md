- `Ctrl + A` `Home` - set the cursor to a line beginning
- `Ctrl + E` `End` - set the cursor to a line end


- `Ctrl + >` `Alt + >` `Alt + B` - move the cursor one word back|left
- `Ctrl + <` `Alt + <` `Alt + F` - move the cursor one word forward|right


- `Ctrl + U` - erase everything before the cursor
- `Ctrl + K` - erase everything after the cursor

- `Ctrl + W` - delete the word before the cursor

- `Ctrl + Y` - redo, reversing a previous Undo. Used for pasting the erased text that we removed using `Ctrl+K`, `Ctrl+U`, and `Ctrl+W` shortcuts keys. It is efficient in case we erased text or when we have to use that erased text again.

- `Ctrl + R` - search command history by a match (backward search). Repeat to switch to preceding matching command.
- `Enter` `Ctrl + O` - run found command
- `Ctrl + C` `Ctrl + G`- leave the search without the last search outputbut and executing
- `Esc` - leave the search with the last search outputbut without executing

- `history [n]` `history | grep match` - show command history. n - history length to show
- `!history-num` - run history command

- `Ctrl + A` `Home` - set the cursor to a line beginning
- `Ctrl + E` `End` - set the cursor to a line end


- `Ctrl + >` `Alt + >` `Alt + B` - move the cursor one word back | left
- `Ctrl + <` `Alt + <` `Alt + F` - move the cursor one word forward | right


- `Ctrl + U` - erase everything before the cursor
- `Ctrl + K` - erase everything after the cursor
- `Alt + R` - erase typed text(like whole line), but `Ctrl + Y` won't work

- `Alt + Backspace` `Ctrl + W` - delete the word before the cursor. `Ctrl + W` - 12_345_678 treats as one word, cuts by whitespaces. `Alt + Backspace` - as 3 words, cuts by special characters.
- `Alt + D` `Ctrl + Delete` - delete the word after the cursor

- `Ctrl + _` where `_` is `Shift + -` - undo last key press

- `Ctrl + Y` - IT IS NOT REDO. Used for pasting the erased text removed using `Ctrl+K`, `Ctrl+U`, `Ctrl+W`, and `Alt + D` shortcuts. It is efficient in case we erased text or when we have to use that erased text again. The Y here stands for "yank". Does't work with`Ctrl + Shift + C`

- `Ctrl + D` `Delete` - delete character UNDER the cursor

- `Ctrl + R` - search command history by a match (backward search). Repeat to switch to preceding matching command.
- `Enter` `Ctrl + O` - run found command
- `Ctrl + C` `Ctrl + G`- leave the search without the last search outputbut and executing
- `Esc` - leave the search with the last search outputbut without executing

- `history [n]` `history | grep match` - show command history. n - history length to show
- `!history-num` - run history command

_There is no `undo` in linux https://unix.stackexchange.com/questions/996/do-we-have-an-undo-in-linux_ \
_There is no text selecting without a mouse in linux terminal. And so `Ctrl + Shift + C` not possible without a mouse. Even selected text cannot be deleted or cut at once._

### BOX select printed text

- `Ctrl + Alt + mouse left button` - box | area select \
  https://www.youtube.com/watch?v=iChlT2W3b8g

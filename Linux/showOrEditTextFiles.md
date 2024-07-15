# Command vs Utility
Command can invoke utility => so command is NOT the same as an utility.\
Often utility is invoked by its name.\
https://unix.stackexchange.com/questions/703873/are-they-commands-or-utilities

- ```cat file.txt``` (utility, to view only)
- ```tac file.txt``` (utility, to view only, reverse cat print order)
- ```more file.txt``` (utility, to view only, forward direction only, page by page[space], line by line[enter], exit[q])
- ```less file.txt``` (utility, to view only, bi-direction, page by page[space|(PgUp|PgDn], line by line[enter|(ArUp|ArDn)], exit[q])
- ```gedit file.txt``` (default text editor)
- ```nano file.txt``` (text editor)
- ```vim file.txt``` (text editor)
- ```head file.txt``` (utility, to view only)
- ```tail file.txt``` (utility, to view only) use -f flag to run in watch mode
- ```nl file.txt``` (like cat, but prints line numbers as well)
- ```sed file.txt``` (utility, stands for Stream [text] EDitor. By default original file is not mutated)\
  https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/
- ```awk``` (utility, comes from the initials of its designers: Aho, Weinberger, and Kernighan. A programming language that is designed for processing text-based data, either in files or data streams, or using shell pipes)\
  https://www.cyberciti.biz/faq/bash-scripting-using-awk/

For testing ```ps -A | less```

How to change default cli text editor\
https://askubuntu.com/questions/615178/getting-the-default-text-editor-used-in-system

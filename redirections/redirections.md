\>& vs &\>\
https://www.gnu.org/software/bash/manual/bash.html#Redirections

File descriptors:\
https://en.wikipedia.org/wiki/File_descriptor

- 0 is stdin
- 1 is stdout
- 2 is stderr

Redirections:

- \> (Output redirection)
- \>> (Append stdout redirection)
- < (Input redirection)
- << (Append stdin redirection)
- << (Here document, input redirection)\
  https://linuxhandbook.com/here-input-redirections/ \
  <<- (Here Document with tab suppression, input redirection) \
  https://phoenixnap.com/kb/bash-heredoc
- <<< (Here string, input redirection)\
  https://linuxhandbook.com/here-input-redirections/
- \>&__descriptor__ (Redirect to file descriptor)\
  https://stackoverflow.com/questions/818255/what-does-21-mean
- \>& or &\> (Merge redirect, descriptor 1 and 2 are merged)

Piping
- |

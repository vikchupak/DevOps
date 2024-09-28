Primary vs Secondary group

https://unix.stackexchange.com/questions/605531/primary-vs-secondary-groups-in-linux
https://www.baeldung.com/linux/primary-vs-secondary-groups

- `/etc/passwd` - file with all users
- `/etc/group` - file with groups
- `/etc/shadow` - file that stores **hashed passwords** and related security information for user accounts.

- `sudo usermod -g admin viktor` - change primary group for a user
- `sudo usermod -G admin viktor` - override secondary group list for a user
- `sudo usermod -aG admin viktor` - add secondary group to group list for a user

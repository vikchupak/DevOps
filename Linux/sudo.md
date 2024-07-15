![image](https://github.com/user-attachments/assets/cdcf2e56-4b30-4b6d-b3d8-42a0433c6f1e)

![image](https://github.com/user-attachments/assets/9c6cf488-fe9b-4565-acc4-2ca23831769f)

![Screenshot from 2024-07-13 13-43-54](https://github.com/user-attachments/assets/ea06d845-d7c0-4527-b91f-db9ddc40e2f2)

To switch to root: ```sudo -i```

Sudo password is only asked first time and cached for some time frame(default 15 minutes)
- https://unix.stackexchange.com/questions/442552/how-does-sudo-decide-whether-to-ask-for-a-password-when-given-a-command-which-d
- https://askubuntu.com/questions/814758/user-in-admin-group-still-being-prompted-for-password-to-sudo

How a user can run docker commands without sudo:
- https://medium.com/devops-technical-notes-and-manuals/how-to-run-docker-commands-without-sudo-28019814198f
- https://www.baeldung.com/linux/docker-run-without-sudo

So, there are 3 "issues":
1. We have to belong to sudo group
2. We have to use sudo prefix https://unix.stackexchange.com/questions/276474/how-can-i-execute-any-command-as-a-normal-user-without-sudo
3. We have to type sudo password

That a user is in sudo group doesn't mean you won't be asked password when running commands with sudo.

Disable sudo password for a spesific user:
- https://www.youtube.com/watch?v=07LXPEHAyyg
- https://alexhost.com/faq/how-to-disable-the-password-for-the-sudo-command-in-linux/
- https://askubuntu.com/questions/147241/execute-sudo-without-password
- https://ostechnix.com/run-particular-commands-without-sudo-password-linux/

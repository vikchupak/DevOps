### Tutorials
- https://www.youtube.com/watch?v=ls5cGi12kGw&list=PLtK75qxsQaMLZSo7KL-PmiRarU7hrpnwK&index=15
- https://www.youtube.com/watch?v=EbWDTvHh2pQ&list=PLI-knp71HL3WcQocBNgTc9Cnj9Wg-2Xki

### 1. Show processes

Windows Task Manager alternatives in Linux\
https://www.reddit.com/r/linux4noobs/comments/p2takc/is_there_a_task_manager_equivalent_for_linux/

- `ps aux` show running processes
- `pstree` to find the parent process of a process
- `top`
- `htop`
- System Monitor `gnome-system-monitor` out-of-the-box\
  __Stop vs End vs Kill a process__\
  https://askubuntu.com/questions/124927/in-system-monitor-what-is-the-difference-between-kill-process-and-end-process \
  https://help.gnome.org/users/gnome-system-monitor/stable/process-kill.html.en

### 2. About htop and how to __monitor__, kill processes like in Windows Task Manager. Set task priority
https://www.youtube.com/watch?v=vsEJz9aKGKU

Priority range [-20, 19]. The less this number, the higher priority

There are priority and niceness

### 2.1 Kill process

https://www.cyberciti.biz/faq/how-force-kill-process-linux/

List services (__a service is a process, so can be killed like a normal process__)\
https://www.tecmint.com/list-all-running-services-under-systemd-in-linux/

**Kill a service vs stop a service**

- stop\
  ![Screenshot from 2024-08-16 15-10-19](https://github.com/user-attachments/assets/dba776eb-e21d-4eb8-8528-6e346cee7df6)
  ![Screenshot from 2024-08-16 15-10-56](https://github.com/user-attachments/assets/71343698-0a44-486a-9d9a-e17a1d7e1071)
  ![Screenshot from 2024-08-16 15-11-22](https://github.com/user-attachments/assets/aae4e998-a8aa-4a6d-b979-9e3609d2f84d)
- kill\
  `ps aux | grep apache2`\
  `sudo kill PID`

The both above have the same result.

### 3. About proc
https://www.youtube.com/watch?v=0XdjODvsRN8

- `proc` intersection between procesess and file system. State of processes in virtual file system(mounted in /proc). The place where the kernel places the information about processes.

### 4. Background vs foreground processes
https://www.youtube.com/watch?v=ghh-8trIFYk&list=PLI-knp71HL3WcQocBNgTc9Cnj9Wg-2Xki&index=3

- A foreground process is a process that interacts directly with the user through the terminal or command line interface. It receives input from the user and displays output to the terminal.
- A background process is a process that runs without user interaction. It does not have control over the terminal, allowing the user to continue using the terminal for other tasks.

Example
- `sleep 30` foreground process
- `sleep 30 &` background process

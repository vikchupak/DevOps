Windows syntax (CMD):
- `set VARIABLE=1` - set env var
- `echo %VARIABLE%` - print env var value
- `set VARIABLE=` - delete env var
- `set` - print all env vars key-value pairs

Linux syntax:
- `export VARIABLE=1` - set env var
- `echo $VARIABLE` - print env var value
- `unset VARIABLE` - delete env var
- `printenv` - print all env vars key-value pairs

Env vars types:\
https://stackoverflow.com/questions/4477660/what-is-the-difference-between-user-variables-and-system-variables \
https://askubuntu.com/questions/58814/how-do-i-add-environment-variables
- System variables - shared for all users
- User variables - only for a user account/profile

# Scopes & inheritance
When you use the `export` command to set an environment variable in a terminal (e.g., `export DB_USER=5`), that environment variable is only available in the current terminal session. It is not visible to other terminal windows because **environment variables are local to the session (or PROCESS) in which they are defined**.

Here are a few reasons why this happens:

1. **Session Scope:** Each terminal window opens a new shell session. Environment variables defined in one shell session are not shared with others.
2. **Non-persistence:** When you set environment variables with `export`, they are not stored globally. Once the terminal session is closed, the variable will no longer exist.
3. **Child Process Inheritance:** Environment variables are inherited by child processes of the shell, but they do not propagate to other shell processes running separately.

## How to set with scopes
- To set **simple variable** only for current shell **(NOT inherited by child processes)**:\
  `VARNAME="my value"`

- To set **env variable** for current shell and all processes started from current shell **(inherited by child processes)**:\
  `export VARNAME="my value"`

- To set **env variable** permanently for all future bash sessions (user specific):\
  Add `export VARNAME="my value"` to `~/.bashrc` file

- To set **env variable** permanently, and system wide (all users, all processes):\
  Add `VARNAME="my value"` to `/etc/environment`. IMPORTANT: Do not use `export` keyword

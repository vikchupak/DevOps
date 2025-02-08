# Create a new linux user

https://www.geeksforgeeks.org/useradd-command-in-linux-with-examples/

If we create user without setting the user's password,
then  the user account won't be activated until we set the password

- https://unix.stackexchange.com/questions/103288/passwords-for-newly-created-users
- https://askubuntu.com/questions/695701/what-is-the-default-password-when-you-create-new-user-in-ubuntu
- https://stackoverflow.com/questions/14570334/retrieve-linux-password-for-current-user

### User password

```bash
sudo cat /etc/shadow | grep test_user

# Output
# test_user:!:19919:0:99999:7:::
# ! - Поле пароля. Символ ! указывает на то, что учетная запись заблокирована. Если бы здесь был зашифрованный пароль, он выглядел бы как длинная строка символов.
```

### User name creteria

Print regexp the user name has to match
```bash
cat /etc/adduser.conf | grep NAME_REGEX

# Output
# NAME_REGEX="^[a-z][-a-z0-9_]*\$"
```

### Add user

```bash
sudo adduser <user_name>
```

### List users

```bash
cat /etc/passwd
```

# Create a new user (non interactive)

```bash
useradd -m -s /bin/bash viktor
echo viktor:viktor | chpasswd
usermod -aG sudo viktor
```

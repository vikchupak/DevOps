# Create a new linux user

https://www.geeksforgeeks.org/useradd-command-in-linux-with-examples/

If we did not create user with setting the user's password,
then  the user account won't be activated until we set the password

- https://unix.stackexchange.com/questions/103288/passwords-for-newly-created-users
- https://askubuntu.com/questions/695701/what-is-the-default-password-when-you-create-new-user-in-ubuntu
- https://stackoverflow.com/questions/14570334/retrieve-linux-password-for-current-user

```bash
sudo cat /etc/shadow | grep test_user
# Output
# test_user:!:19919:0:99999:7:::
# ! - Поле пароля. Символ ! указывает на то, что учетная запись заблокирована. Если бы здесь был зашифрованный пароль, он выглядел бы как длинная строка символов.
```

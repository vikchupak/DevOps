# Directory vs file permissions

### Directory Permissions (`rwxr-xr-x` for `/home/username`):
- **Read (r)**: The ability to list the files and subdirectories inside the directory (i.e., run `ls` to see filenames).
- **Write (w)**: The ability to create, delete, or rename files inside the directory.
- **Execute (x)**: The ability to access (or "enter") the directory and navigate to files or subdirectories inside it.

### File Permissions (`rwxr-xr-x` for a file):
- **Read (r)**: The ability to view or read the contents of the file (i.e., run `cat`, `less`, or open it in a text editor).
- **Write (w)**: The ability to modify the file, such as editing, appending, or deleting its contents.
- **Execute (x)**: The ability to run the file as a program or script (only applicable to executable files like shell scripts or binaries). 

# In linux, can users see each other home directory files?

By default, in most Linux systems, **users cannot see the files in each other's home directories**, but they **can see** the contents of the home directories themselves (i.e., they can list the files but cannot access them unless permissions are specifically changed).

### Default Permissions for Home Directories

- **Home Directory Visibility**: 
  - By default, each user's home directory is located under `/home/username`.
  - Most distributions set the permission of `/home/username` as `rwxr-xr-x` (755), which means:
    - The **owner** (the user) has read, write, and execute permissions.
    - The **group** and **others** have read and execute permissions but **no write permissions**.
    - This allows other users to list the contents of your home directory (e.g., they can see the filenames), but they **cannot access or read** the actual files inside unless permissions are changed.

- **File and Folder Permissions**:
  - By default, files and subdirectories inside the home directory are typically set to `rw-------` (600 for files, 700 for directories), meaning only the owner can read, write, and execute the files or folders.
  - Other users can't open, read, modify, or delete your files by default unless you specifically grant them permission.

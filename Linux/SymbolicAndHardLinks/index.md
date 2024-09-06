# Tutorials
- https://medium.com/@hemant.heer/what-is-the-difference-between-a-symbolic-link-and-a-hard-link-7c1820f35623
- https://en.wikipedia.org/wiki/Hard_link
- https://www.youtube.com/watch?v=rQpT0bRpV3Y
- Links below are less important
- https://www.youtube.com/watch?v=lW_V8oFxQgA
- https://www.linkedin.com/pulse/what-difference-between-hard-link-symbolic-besmira-a-/
- https://stackoverflow.com/questions/185899/what-is-the-difference-between-a-symbolic-link-and-a-hard-link

# File

- A file is the file's name (that is stored in a __directory__ and points/maps to its corresponding inode) and the inode (that contains metadata about the file and points to the actual data)

# Inodes

- `inode(index node)` is a data structure on a file system that stores all the information about a file __*except its name and its actual data*__. Each file and directory is associated with an inode.

### Information Stored in an Inode

An inode contains several pieces of metadata about a file, including:

- **File type**: Regular file, directory, symbolic link, etc.
- **Permissions**: Read, write, and execute permissions for the owner, group, and others.
- **Owner**: User ID (UID) of the file owner.
- **Group**: Group ID (GID) of the owning group.
- **Size**: The size of the file in bytes.
- **Timestamps**: 
  - **ctime** (change time): The last time the inode metadata was changed.
  - **mtime** (modification time): The last time the file content was modified.
  - **atime** (access time): The last time the file was accessed.
- **Link count**: The number of hard links pointing to this inode.
- **Pointers to data blocks**: Addresses of the disk blocks where the file's data is stored.

### Modification
- Modifying a file updates the inode's metadata (e.g., `mtime`), and potentially updates the pointers to data blocks if the size of the file changes.

### Inode Numbers
- Each inode is identified by an inode number (often referred to as an "i-number" or "inode index"). This is unique within the file system and used by the system to locate the inode.

### Inode Table
- The inode table is a data structure used by the file system to store all inodes. When a file system is created, a fixed number of inodes are allocated, defining the maximum number of files the file system can hold.

# Hard links
___When a hard link is created, then a new file name is created in a directory and the name points/maps to the existing inode.___

  - Hard link is a link/pointer to inode, which points to original file data blocks.
  - All hard links for the same file points to the same inode.
  - Hard links cannot refer to directories (to avoid filesystem loops, in general, but there are exceptions) and cannot refer to different partitions and file systems.
  - The original file, is always a hard link that points to inode.\
    There are no way to figure out which hard link is the original hard link created when a file is first created.

Hard link создает дополнительную ссылку на тот же inode, поэтому несколько файловых имен могут указывать на один и тот же inode и данные.

```
  [Оригинальный файл] --> [inode 1234] --> [Данные файла]
                  \
                   \
                    --> [hard link] --> [inode 1234] --> [Данные файла]
```
 
# Symbolic links
A symbolic link is considered a special type of file in Unix-like operating systems, but it behaves differently from regular files or hard links. A symbolic link is a file that contains a reference to another file or directory. ___Instead of pointing directly to the inode of a file like a hard link does, a soft link points to the file name (or path) of the target file.___

- Symbolic link is __*a separate file*__ that points to the original file(hard link). __So it has own inode__.
- Symbolic links can refer to directories and different partitions and file systems.

Soft link, напротив, создает новый файл с собственным inode, который указывает на путь к оригинальному файлу.

```
  [Оригинальный файл] --> [inode 1234] --> [Данные файла]
                  \
                   \
                    --> [soft link] --> [inode 5678] --> [Путь к оригинальному файлу (Оригинальный файл)]
```

# Directories

### What is a Directory?

A **directory** in Unix-like systems is a special type of file that acts as a container or organizer for other files and directories. It helps structure the file system into a hierarchy, making it easier to manage and navigate through the various files on a system.

### Key Characteristics of a Directory:

1. **Special File Type**:
   - A directory is treated as a special kind of file that contains a list of other files and directories. It doesn’t hold data like regular files but instead contains mappings between file names and their corresponding inodes.

2. **Contents of a Directory**:
   - The contents of a directory are essentially a list of entries. Each entry in this list maps a file name to an inode number.
   - For example, in a directory, you might have entries like:
     ```
     file1 -> inode 12345
     file2 -> inode 67890
     dir1  -> inode 11223
     ```
     Here, `file1`, `file2`, and `dir1` are the names of the files or subdirectories, and the numbers represent their respective inodes.

3. **Hierarchical Structure**:
   - Directories allow the file system to be organized in a tree-like structure. At the top of this structure is the root directory, usually represented by `/`, which contains all other directories and files.
   - For example:
     ```
     /
     ├── home/
     │   ├── user/
     │   │   ├── documents/
     │   │   └── pictures/
     └── var/
         ├── log/
         └── tmp/
     ```
   - Each directory can contain files as well as other directories (subdirectories), leading to a nested structure.

4. **Permissions**:
   - Directories have permissions, just like regular files. The permissions control who can read, write, or execute (enter) the directory.
   - **Read (`r`)**: Allows the contents (file names) of the directory to be listed.
   - **Write (`w`)**: Allows the creation, deletion, and renaming of files within the directory.
   - **Execute (`x`)**: Allows a user to enter the directory and access its contents.

### How Directories Work with Inodes:

When you list the contents of a directory using `ls -l`, you see the names of the files and directories, but in the background, the system is actually mapping these names to their respective inodes.

For example, the command:

```bash
ls -li /path/to/directory
```

would show something like:

```
12345 drwxr-xr-x 2 user group 4096 Sep  6 10:00 dir1
67890 -rw-r--r-- 1 user group  512 Sep  6 09:00 file1.txt
```

Here, `12345` and `67890` are inode numbers. The directory `dir1` and the file `file1.txt` are linked to these inodes, which contain the metadata and pointers to their actual data on the disk.

### Summary

A directory is a fundamental concept in Unix-like systems, serving as a container that holds references to files and other directories. It provides the structure that organizes files in a hierarchical manner, allowing for efficient storage, access, and management of data within the file system.

# Commands

- `stat` - display file or file system status
- `ln` - create links between files
- `ls -li` - list directory contents. `-i` flag to displays the inode number of each file

- `ln <targetFile> <newHardLink>` - create a had link
- `ln -s <targetFile> <newSoftLinkName or absolutePathWithName>` - create a soft link

# Real use case

![photo_2024-05-19_14-02-36](https://github.com/user-attachments/assets/f23f707f-1a38-45be-9e5f-9c352a3beb5e)

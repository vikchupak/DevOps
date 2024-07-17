# Tutorials
- https://medium.com/@hemant.heer/what-is-the-difference-between-a-symbolic-link-and-a-hard-link-7c1820f35623
- https://www.youtube.com/watch?v=rQpT0bRpV3Y
- Links below are less important
- https://www.youtube.com/watch?v=lW_V8oFxQgA
- https://www.linkedin.com/pulse/what-difference-between-hard-link-symbolic-besmira-a-/
- https://stackoverflow.com/questions/185899/what-is-the-difference-between-a-symbolic-link-and-a-hard-link

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
  - Hard link is a link/pointer to inode, which points to original file data blocks.
  - All hard links for the same file points to the same inode.
  - Hard links cannot refer to directories (in general, but there are exceptions) and cannot refer to different partitions and file systems.
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
- Symbolic link is __*a separate file*__ that points to the original file(hard link). __So it has own inode__.
- Symbolic links can refer to directories and different partitions and file systems.

Soft link, напротив, создает новый файл с собственным inode, который указывает на путь к оригинальному файлу.

```
  [Оригинальный файл] --> [inode 1234] --> [Данные файла]
                  \
                   \
                    --> [soft link] --> [inode 5678] --> [Путь к оригинальному файлу (Оригинальный файл)]
```

# Commands

- `stat` - display file or file system status
- `ln` - create links between files
- `ls -li` - list directory contents. `-i` flag to displays the inode number of each file

- `ln <targetFile> <newHardLink>` - create a had link
- `ln -s <targetFile> <newSoftLink>` - create a soft link

# Real usage case

![photo_2024-05-19_14-02-36](https://github.com/user-attachments/assets/f23f707f-1a38-45be-9e5f-9c352a3beb5e)

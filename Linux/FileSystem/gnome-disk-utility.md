# What commands disks uses?

The `gnome-disk-utility` (Disks) application uses several underlying commands and utilities to perform various disk management tasks. Here are some of the common commands and utilities that `gnome-disk-utility` relies on:

### 1. **`lsblk`**
- Lists all block devices and their attributes, such as device names, sizes, and mount points.
  
  Example:
  ```bash
  lsblk
  ```

### 2. **`fdisk`**
- A command-line utility for partitioning hard drives. Used for creating, deleting, and managing disk partitions.
  
  Example (for listing partitions):
  ```bash
  sudo fdisk -l /dev/sda
  ```

### 3. **`parted`**
- A more advanced tool for managing disk partitions. It supports various file systems and allows for resizing, moving, and creating partitions.
  
  Example (to start the interactive tool):
  ```bash
  sudo parted /dev/sda
  ```

### 4. **`mkfs`**
- Used to create file systems on partitions. There are specific variants for different file systems, such as `mkfs.ext4`, `mkfs.vfat`, and `mkfs.ntfs`.

  Example (to format a partition as ext4):
  ```bash
  sudo mkfs.ext4 /dev/sdb1
  ```

### 5. **`mount` and `umount`**
- These commands are used to mount and unmount file systems, allowing access to the data stored on partitions.

  Examples:
  ```bash
  sudo mount /dev/sdb1 /mnt/myusb
  sudo umount /mnt/myusb
  ```

### 6. **`smartctl`**
- Part of the `smartmontools` package, this utility is used to control and monitor S.M.A.R.T. (Self-Monitoring, Analysis, and Reporting Technology) on hard drives to check their health.

  Example:
  ```bash
  sudo smartctl -a /dev/sda
  ```

### 7. **`dd`**
- A low-level command-line tool for copying and converting data. It can also be used for tasks like creating disk images.

  Example (to create a disk image):
  ```bash
  sudo dd if=/dev/sda of=/path/to/image.img bs=4M
  ```

### 8. **`resize2fs`**
- A command used to resize ext2, ext3, and ext4 file systems. This is typically used after resizing a partition with tools like `parted`.

  Example:
  ```bash
  sudo resize2fs /dev/sdb1
  ```

### 9. **`blkid`**
- Displays information about block devices, including their UUIDs and file system types.

  Example:
  ```bash
  sudo blkid
  ```

### 10. **`df`**
- Displays information about disk space usage for mounted filesystems.

  Example:
  ```bash
  df -h
  ```

These commands and utilities provide the underlying functionality that allows `gnome-disk-utility` to perform tasks related to disk management in a graphical user interface. You can often use these commands directly in the terminal for more advanced or specific tasks.

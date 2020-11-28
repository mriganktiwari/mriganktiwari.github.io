# Mounting a storage device on to a file-system



- ## Issue:

  - I installed Ubuntu 19.10 to my desktop, which has 2 drives, a 500 GB SSD and a 1TB HDD.
  - While installing Ubuntu I just chose the 500 GB SSD for Ubuntu, hence when using my computer now I just cannot see the 1TB disk available for use anywhere.
  - In file explorer, if I look into *Properties*  of the `Home` directory I see just approximately 500GB. Whereas looking into *About* of the Settings shows 1.5TB.

- ## Groundwork:

  - I checked file-systems usage with `df -h` , we see that the below sizes sum up to a ball park of 500GB.

  ```
  (base) mrigank@mrigank:/etc$ df -h
  Filesystem      Size  Used Avail Use% Mounted on
  udev             12G     0   12G   0% /dev
  tmpfs           2.4G  2.0M  2.4G   1% /run
  /dev/sdb2       457G   62G  373G  15% /
  tmpfs            12G  457M   12G   4% /dev/shm
  tmpfs           5.0M  4.0K  5.0M   1% /run/lock
  tmpfs            12G     0   12G   0% /sys/fs/cgroup
  /dev/loop3       68M   68M     0 100% /snap/sublime-text/85
  /dev/loop2      4.3M  4.3M     0 100% /snap/gnome-calculator/501
  /dev/loop4      161M  161M     0 100% /snap/gnome-3-28-1804/116
  /dev/loop0       15M   15M     0 100% /snap/gnome-characters/495
  /dev/loop5      143M  143M     0 100% /snap/code/31
  /dev/loop1      164M  164M     0 100% /snap/spotify/41
  /dev/loop6       55M   55M     0 100% /snap/core18/1705
  /dev/loop7      150M  150M     0 100% /snap/gnome-3-28-1804/71
  /dev/loop8      1.0M  1.0M     0 100% /snap/gnome-logs/93
  /dev/loop9       94M   94M     0 100% /snap/core/8935
  /dev/loop10     143M  143M     0 100% /snap/slack/23
  /dev/loop11     1.0M  1.0M     0 100% /snap/gnome-logs/81
  /dev/loop12      15M   15M     0 100% /snap/gnome-characters/317
  /dev/loop13     4.4M  4.4M     0 100% /snap/gnome-calculator/704
  /dev/loop14      63M   63M     0 100% /snap/gtk-common-themes/1506
  /dev/loop15      55M   55M     0 100% /snap/gtk-common-themes/1502
  /dev/loop17      94M   94M     0 100% /snap/core/9066
  /dev/loop16     143M  143M     0 100% /snap/slack/22
  /dev/loop18      55M   55M     0 100% /snap/core18/1668
  /dev/loop19     141M  141M     0 100% /snap/code/30
  /dev/sdb1       511M  9.1M  502M   2% /boot/efi
  tmpfs           2.4G   24K  2.4G   1% /run/user/124
  tmpfs           2.4G   96K  2.4G   1% /run/user/1000
  
  ```

  - As we cannot find where is my 1TB device lost with above command, we use `lsblk`, and here it is. We see a device named `sda` of ~1TB space and clearly it should be the one we are looking for.

  ```
  (base) mrigank@mrigank:/etc$ lsblk
  NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
  loop0    7:0    0  14.8M  1 loop /snap/gnome-characters/495
  loop1    7:1    0 163.7M  1 loop /snap/spotify/41
  loop2    7:2    0   4.2M  1 loop /snap/gnome-calculator/501
  loop3    7:3    0  67.6M  1 loop /snap/sublime-text/85
  loop4    7:4    0 160.2M  1 loop /snap/gnome-3-28-1804/116
  loop5    7:5    0 142.9M  1 loop /snap/code/31
  loop6    7:6    0    55M  1 loop /snap/core18/1705
  loop7    7:7    0 149.9M  1 loop /snap/gnome-3-28-1804/71
  loop8    7:8    0   956K  1 loop /snap/gnome-logs/93
  loop9    7:9    0  93.8M  1 loop /snap/core/8935
  loop10   7:10   0 142.2M  1 loop /snap/slack/23
  loop11   7:11   0   956K  1 loop /snap/gnome-logs/81
  loop12   7:12   0  14.8M  1 loop /snap/gnome-characters/317
  loop13   7:13   0   4.3M  1 loop /snap/gnome-calculator/704
  loop14   7:14   0  62.1M  1 loop /snap/gtk-common-themes/1506
  loop15   7:15   0  54.8M  1 loop /snap/gtk-common-themes/1502
  loop16   7:16   0 142.2M  1 loop /snap/slack/22
  loop17   7:17   0  93.9M  1 loop /snap/core/9066
  loop18   7:18   0  54.7M  1 loop /snap/core18/1668
  loop19   7:19   0 140.2M  1 loop /snap/code/30
  sda      8:0    0 931.5G  0 disk 
  sdb      8:16   0 465.8G  0 disk 
  ├─sdb1   8:17   0   512M  0 part /boot/efi
  └─sdb2   8:18   0 465.3G  0 part /
  
  ```

  - The command `sudo fdisk -l` will list the the drives and their partitions for us.
    - Scrolling down we find device named `/dev/sda` which is of concern right now, whereas for `/dev/sdb` you see the partitions information available.
    - We will have to create new partition for `/dev/sda`

  ```
  (base) mrigank@mrigank:/$ sudo fdisk -l
  [sudo] password for mrigank:
  
  Disk /dev/sda: 931.53 GiB, 1000204886016 bytes, 1953525168 sectors
  Disk model: ST1000DM003-1SB1
  Units: sectors of 1 * 512 = 512 bytes
  Sector size (logical/physical): 512 bytes / 4096 bytes
  I/O size (minimum/optimal): 4096 bytes / 4096 bytes
  Disklabel type: gpt
  Disk identifier: 8BBAFF6A-AC43-4365-9794-F32A35393EA3
  
  
  Disk /dev/sdb: 465.78 GiB, 500107862016 bytes, 976773168 sectors
  Disk model: Samsung SSD 850 
  Units: sectors of 1 * 512 = 512 bytes
  Sector size (logical/physical): 512 bytes / 512 bytes
  I/O size (minimum/optimal): 512 bytes / 512 bytes
  Disklabel type: gpt
  Disk identifier: C3CADC26-E36E-4796-B118-4288464233B6
  
  Device       Start       End   Sectors   Size Type
  /dev/sdb1     2048   1050623   1048576   512M EFI System
  /dev/sdb2  1050624 976771071 975720448 465.3G Linux filesystem
  
  ```

  

- ## Creating a new partition for `/dev/sda`

  - We use **fdisk** to create partition with this command `sudo fdisk /dev/sda`
  - When *fdisk* prompts for a command, `p` would print the partition table for out hard drive, which doesn't exist for `/dev/sda` right now.

  ```
  (base) mrigank@mrigank:~$ sudo fdisk /dev/sda
  
  Welcome to fdisk (util-linux 2.34).
  Changes will remain in memory only, until you decide to write them.
  Be careful before using the write command.
  
  
  Command (m for help): p
  Disk /dev/sda: 931.53 GiB, 1000204886016 bytes, 1953525168 sectors
  Disk model: ST1000DM003-1SB1
  Units: sectors of 1 * 512 = 512 bytes
  Sector size (logical/physical): 512 bytes / 4096 bytes
  I/O size (minimum/optimal): 4096 bytes / 4096 bytes
  Disklabel type: gpt
  Disk identifier: 8BBAFF6A-AC43-4365-9794-F32A35393EA3
  ```

  - For a **new partition** press `n` and them `p` for primary partition. And when asked for partition number press `1`
  - Press `Enter` for *First sector* and *Last sector* to accept the default value
  - Although `fdisk` confirms that it has created a 1TB Linux partition, which is partition number 1, nothing has changed on the hard drive yet. Until you give `fdisk` the command to write the changes to the drive, the drive is untouched. Once you are certain you’re happy with our choices, press the letter `w` to write the changes to the drive. And `q` for quitting the fdisk prompt.

  ```
  (base) mrigank@mrigank:~$ sudo fdisk /dev/sda
  
  Welcome to fdisk (util-linux 2.34).
  Changes will remain in memory only, until you decide to write them.
  Be careful before using the write command.
  
  
  Command (m for help): n
  Partition number (1-128, default 1): 1
  First sector (34-1953525134, default 2048): 
  Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-1953525134, default 1953525134): 
  
  Created a new partition 1 of type 'Linux filesystem' and of size 931.5 GiB.
  Partition #1 contains a ntfs signature.
  
  Do you want to remove the signature? [Y]es/[N]o: N
  
  Command (m for help): w
  
  The partition table has been altered.
  Calling ioctl() to re-read partition table.
  Syncing disks.
  
  ```

  - Check is now the `fdisk` command prints the partition table for `/dev/sda`

  ```
  (base) mrigank@mrigank:~$ sudo fdisk /dev/sda
  
  Welcome to fdisk (util-linux 2.34).
  Changes will remain in memory only, until you decide to write them.
  Be careful before using the write command.
  
  
  Command (m for help): p
  Disk /dev/sda: 931.53 GiB, 1000204886016 bytes, 1953525168 sectors
  Disk model: ST1000DM003-1SB1
  Units: sectors of 1 * 512 = 512 bytes
  Sector size (logical/physical): 512 bytes / 4096 bytes
  I/O size (minimum/optimal): 4096 bytes / 4096 bytes
  Disklabel type: gpt
  Disk identifier: 8BBAFF6A-AC43-4365-9794-F32A35393EA3
  
  Device     Start        End    Sectors   Size Type
  /dev/sda1   2048 1953525134 1953523087 931.5G Linux filesystem
  
  Command (m for help): q
  
  ```

  - Also we can now see an new partition `/dev/sda1` in `lsblk`

  ```
  (base) mrigank@mrigank:~$ lsblk
  NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
  .
  .
  .
  loop20   7:20   0   2.4M  1 loop /snap/gnome-calculator/730
  sda      8:0    0 931.5G  0 disk 
  └─sda1   8:1    0 931.5G  0 part 
  sdb      8:16   0 465.8G  0 disk 
  ├─sdb1   8:17   0   512M  0 part /boot/efi
  └─sdb2   8:18   0 465.3G  0 part /
  ```

  

- ## Create a file-system on the new Partition

  - We need to create a file-system on the newly created partition `/dev/sda`, using command `mkfs`.
  - **Be careful** to write **`/dev/sda1`** in `sudo mkfs -t ext4 /dev/sda1`
  - The file-system created or the drive is of `ntfs` format, so the below error. We must alter our command accordingly

  ```
  (base) mrigank@mrigank:~$ sudo mkfs -t ext4 /dev/sda1
  mke2fs 1.45.3 (14-Jul-2019)
  /dev/sda1 contains a ntfs file system labelled 'BULGOGI'
  Proceed anyway? (y,N) N
  ```

  - Instead if we use `sudo mkfs -t ntfs /dev/sda1`

  ```
  (base) mrigank@mrigank:~$ sudo mkfs -t ntfs /dev/sda1
  Cluster size has been automatically set to 4096 bytes.
  Initializing device with zeroes:   4%
  ```

  - After 110 minutes later 100% done

  ```
  (base) mrigank@mrigank:~$ sudo mkfs -t ntfs /dev/sda1
  Cluster size has been automatically set to 4096 bytes.
  Initializing device with zeroes: 100% - Done.
  Creating NTFS volume structures.
  mkntfs completed successfully. Have a nice day.
  ```

  - 

- ## Mounting the New Drive

  - We must mount the partition `/dev/sda1` on the new drive `/dev/sda` to a mount point in the file-system.
  - We’re going to use the `mount` command to [mount the filesystem](https://www.howtogeek.com/414634/how-to-mount-and-unmount-storage-devices-from-the-linux-terminal/) on the first partition on `/dev/sdb`, at `/mnt` .
  - `sudo mount /dev/sda1 /mnt`
  - `sudo umount /mnt`
  - Add `/mnt` as bookmarks in file explorer.

- 

- 

- 

- 

- [Motivated by](https://www.howtogeek.com/442101/how-to-move-your-linux-home-directory-to-another-hard-drive/#comments).

  - 
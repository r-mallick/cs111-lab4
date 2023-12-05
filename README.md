# Hey! I'm Filing Here

In this lab, I successfully implemented a basic EXT2 file system, where I created four inodes: the root directory, the lost+found directory, a hello-world file, and a hello symlink.

## Building

Run the following to compile the executable:

```shell
make
```

## Running

First you need to make a directory called `mnt` which is the directory we will use to mount our file system to.

```shell
mkdir mnt
```

Next, run the following to create cs111-base.img, mount your file system, and change your current working directory to `mnt`.

```shell
./ext2-create
sudo mount -o loop cs111-base.img mnt
cd mnt
```

If you run `ls -ain`, you should get the following:
```shell
total 7
  2 drwxr-xr-x 3    0    0 1024 Dec   3 21:01 .
402 drwxr-xr-x 5 1000 1000 4096 Dec   3 21:01 ..
 13 lrw-r--r-- 1 1000 1000   11 Dec   3 21:01 hello -> hello-world
 12 -rw-r--r-- 1 1000 1000   12 Dec   3 21:01 hello-world
 11 drwxr-xr-x 2    0    0 1024 Dec   3 21:01 lost+found
```

Note 1: Metadata about the `..` directory as well as the timestamps will vary per user.

Note 2: To dump the file system information or check that the filesystem is correct, run `dumpe2fs cs111-base.img` and `fsck.ext2 cs111-base.img` respectively.

## Cleaning up

Run the following commands:
```shell
cd .. # change out of the mnt directory
sudo umount mnt # unmount the file system
rmdir mnt # remove the mnt directory
make clean # remove all binaries nad executables
```

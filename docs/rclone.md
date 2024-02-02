---
title: rclone
tags: [computer]
---

## install

To install rclone on Linux/macOS/BSD systems, run:

```
sudo -v ; curl https://rclone.org/install.sh | sudo bash
```

## configure

The easiest way to make the config is to run rclone with the config option:

```
rclone config
```

## Basic syntax

Rclone syncs a directory tree from one storage system to another.

Its syntax is like this

```
Syntax: [options] subcommand <parameters> <parameters...>
```

## Subcommands

rclone uses a system of subcommands. For example

```
rclone ls remote:path # lists a remote
rclone copy /local/path remote:path # copies /local/path to the remote
rclone sync -i /local/path remote:path # syncs /local/path to the remote
```

The main rclone commands with most used first

-   [rclone config](https://rclone.org/commands/rclone_config/) - Enter an interactive configuration session.
-   [rclone copy](https://rclone.org/commands/rclone_copy/) - Copy files from source to dest, skipping already copied.
-   [rclone sync](https://rclone.org/commands/rclone_sync/) - Make source and dest identical, modifying destination only.
-   [rclone bisync](https://rclone.org/commands/rclone_bisync/) - [Bidirectional synchronization](https://rclone.org/bisync/) between two paths.
-   [rclone move](https://rclone.org/commands/rclone_move/) - Move files from source to dest.
-   [rclone delete](https://rclone.org/commands/rclone_delete/) - Remove the contents of path.
-   [rclone purge](https://rclone.org/commands/rclone_purge/) - Remove the path and all of its contents.
-   [rclone mkdir](https://rclone.org/commands/rclone_mkdir/) - Make the path if it doesn't already exist.
-   [rclone rmdir](https://rclone.org/commands/rclone_rmdir/) - Remove the path.
-   [rclone rmdirs](https://rclone.org/commands/rclone_rmdirs/) - Remove any empty directories under the path.
-   [rclone check](https://rclone.org/commands/rclone_check/) - Check if the files in the source and destination match.
-   [rclone ls](https://rclone.org/commands/rclone_ls/) - List all the objects in the path with size and path.
-   [rclone lsd](https://rclone.org/commands/rclone_lsd/) - List all directories/containers/buckets in the path.
-   [rclone lsl](https://rclone.org/commands/rclone_lsl/) - List all the objects in the path with size, modification time and path.
-   [rclone md5sum](https://rclone.org/commands/rclone_md5sum/) - Produce an md5sum file for all the objects in the path.
-   [rclone sha1sum](https://rclone.org/commands/rclone_sha1sum/) - Produce a sha1sum file for all the objects in the path.
-   [rclone size](https://rclone.org/commands/rclone_size/) - Return the total size and number of objects in remote:path.
-   [rclone version](https://rclone.org/commands/rclone_version/) - Show the version number.
-   [rclone cleanup](https://rclone.org/commands/rclone_cleanup/) - Clean up the remote if possible.
-   [rclone dedupe](https://rclone.org/commands/rclone_dedupe/) - Interactively find duplicate files and delete/rename them.
-   [rclone authorize](https://rclone.org/commands/rclone_authorize/) - Remote authorization.
-   [rclone cat](https://rclone.org/commands/rclone_cat/) - Concatenate any files and send them to stdout.
-   [rclone copyto](https://rclone.org/commands/rclone_copyto/) - Copy files from source to dest, skipping already copied.
-   [rclone genautocomplete](https://rclone.org/commands/rclone_genautocomplete/) - Output shell completion scripts for rclone.
-   [rclone gendocs](https://rclone.org/commands/rclone_gendocs/) - Output markdown docs for rclone to the directory supplied.
-   [rclone listremotes](https://rclone.org/commands/rclone_listremotes/) - List all the remotes in the config file.
-   [rclone mount](https://rclone.org/commands/rclone_mount/) - Mount the remote as a mountpoint.
-   [rclone moveto](https://rclone.org/commands/rclone_moveto/) - Move file or directory from source to dest.
-   [rclone obscure](https://rclone.org/commands/rclone_obscure/) - Obscure password for use in the rclone.conf
-   [rclone cryptcheck](https://rclone.org/commands/rclone_cryptcheck/) - Check the integrity of an encrypted remote.
-   [rclone about](https://rclone.org/commands/rclone_about/) - Get quota information from the remote.

## Tips

Without the use of --vfs-cache-mode this can only write files sequentially, it can only seek when reading. This means that many applications won't work with their files on an rclone mount without --vfs-cache-mode writes or --vfs-cache-mode full

for "can't copy - source file is being updated" problem add the --local-no-check-updated or the new version --no-modtime

```
rclone mount onedrive: /mnt/onedrive -vv --vfs-cache-mode full --no-modtime
```

Rclone stores all of its config in a single file. If you want to find this file, run **rclone config file** which will tell you where it is.

```
rclone config
```


for "Transport endpoint not connected"

尝试重新挂载

解除挂载命令 加上参数-z表示强制

```
fusermount -u /mnt/onedrive
```


如其它一些应用要读取挂载点可能需要加上 --allow-other 命令，此命令需要修改fuse.conf文件

```
sudo vi /etc/fuse.conf
```

uncomment "user_allow_other"

```
rclone mount onedrive: /mnt/onew --daemon --log-level INFO --log-file "/tmp/rclone.log" --vfs-cache-mode writes --no-modtime --allow-other
```
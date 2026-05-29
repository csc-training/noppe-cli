# Working with files

The following commands all assume that a file already exists. If needed, you can create some using commands such as `touch emptyfile` or `echo Hello > file-with-text`.

To make managing files easier to understand, let's also create a subdirectory: `mkdir subdir`.

## Copy

Copying file is very straightforward: `cp emptyfile another-empty` command creates a copy of the `emptyfile` called `another-empty`.

You can also copy a file to a different location: `cp file-with-text subdir/textfile-copy`.

It's also possible to copy entire directories, including their contents: `cp -R subdir dir-copy`.

When copying to a different location, you can omit the target file's name: `cp emptyfile dir-copy`. This preserves the original file name.

::: beware
The last command may seem confusing, as it could be interpreted as copying a file called `emptyfile` to a new file called `dir-copy`. However, since the `dir-copy` file already exists and is a directory, the `emptyfile` is copied into the subdirectory with its original name instead.
:::

Verify the content of the `dir-copy` directory with the command: `ls -il dir-copy`. Notice the different file attributes and compare them to the originals, if you wish.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ touch emptyfile
{{USERNAME}}@{{HOSTNAME}}:~$ echo Hello > file-with-text
{{USERNAME}}@{{HOSTNAME}}:~$ mkdir subdir
{{USERNAME}}@{{HOSTNAME}}:~$ cp emptyfile another-empty
{{USERNAME}}@{{HOSTNAME}}:~$ cp file-with-text subdir/textfile-copy
{{USERNAME}}@{{HOSTNAME}}:~$ cp -R subdir dir-copy
{{USERNAME}}@{{HOSTNAME}}:~$ cp emptyfile dir-copy
{{USERNAME}}@{{HOSTNAME}}:~$ ls -il dir-copy
total 4
525372 -rw-rw-r-- 1 {{USERNAME}} {{USERNAME}} 0 Apr  6 05:36 emptyfile
525371 -rw-rw-r-- 1 {{USERNAME}} {{USERNAME}} 6 Apr  6 05:33 textfile-copy
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

## Move

In terms of usage, moving and copying files are very similar: `mv another-empty backup-of-emptyfile` command changes the name of the `another-empty` file to `backup-of-emptyfile`. Using the `mv` command in this way is a proper way to rename files.

::: service
You can verify that they are the same file by using the `ls -il` command to compare the file's inode number before and after the `mv` command.
:::

It's also possible to move files and directories to a different location while preserving the original name: `mv dir-copy subdir` moves the directory `dir-copy` and its contents under `subdir` directory. Verify the result using the `ls -ilR subdir` command.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ mv another-empty backup-of-emptyfile
{{USERNAME}}@{{HOSTNAME}}:~$ mv dir-copy subdir
{{USERNAME}}@{{HOSTNAME}}:~$ ls -ilR subdir
subdir/:
total 8
525370 drwxrwxr-x 2 {{USERNAME}} {{USERNAME}} 4096 Apr 06 05:36 dir-copy
525369 -rw-rw-r-- 1 {{USERNAME}} {{USERNAME}}    6 Apr 06 05:33 textfile-copy

subdir/dir-copy:
total 4
525372 -rw-rw-r-- 1 {{USERNAME}} {{USERNAME}} 0 Apr 06 05:36 emptyfile
525371 -rw-rw-r-- 1 {{USERNAME}} {{USERNAME}} 6 Apr 06 05:33 textfile-copy
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

### Rename

Some systems have a `rename` command available. If not, use the `mv` command: `mv file-with-old-name same-file-with-new-name`.

## Delete

As you might expect, the `rm` command works in a similar way to the `cp` and `mv` commands: `rm backup-of-emptyfile` command deletes the `backup-of-emptyfile` file.

Files in different locations can also be deleted: `rm subdir/textfile-copy`.

You can use the `rm` command to delete entire directories, including their contents: `rm -r subdir/dir-copy` command deletes the `dir-copy` directory and its contents.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ rm backup-of-emptyfile
{{USERNAME}}@{{HOSTNAME}}:~$ rm subdir/textfile-copy
{{USERNAME}}@{{HOSTNAME}}:~$ rm -r subdir/dir-copy
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

::: note
As emphasised earlier, exercise caution when deleting files. There is no automatic backup or 'Trash' functionality for files deleted using the `rm` command. In particular, it is easy to make a mistake when deleting directories recursively.
:::

That's it! You can now continue with the [View](06.1-view.md) chapter.

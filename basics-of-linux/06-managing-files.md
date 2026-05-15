# Managing files

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
__HOSTNAME__@__USERNAME__:~$ touch emptyfile
__HOSTNAME__@__USERNAME__:~$ echo Hello > file-with-text
__HOSTNAME__@__USERNAME__:~$ mkdir subdir
__HOSTNAME__@__USERNAME__:~$ cp emptyfile another-empty
__HOSTNAME__@__USERNAME__:~$ cp file-with-text subdir/textfile-copy
__HOSTNAME__@__USERNAME__:~$ cp -R subdir dir-copy
__HOSTNAME__@__USERNAME__:~$ cp emptyfile dir-copy
__HOSTNAME__@__USERNAME__:~$ ls -il dir-copy
total 4
525372 -rw-rw-r-- 1 __USERNAME__ __USERNAME__ 0 Apr  6 05:36 emptyfile
525371 -rw-rw-r-- 1 __USERNAME__ __USERNAME__ 6 Apr  6 05:33 textfile-copy
__HOSTNAME__@__USERNAME__:~$ █
:::

## Move

In terms of usage, moving and copying files are very similar: `mv another-empty backup-of-emptyfile` command changes the name of the `another-empty` file to `backup-of-emptyfile`.

::: service
You can verify that they are the same file by using the `ls -il` command to compare the file's inode number before and after the `mv` command.
:::

It's also possible to move files and directories to a different location while preserving the original name: `mv dir-copy subdir` moves the directory `dir-copy` and its contents under `subdir` directory. Verify the result using the `ls -ilR subdir` command.

::: terminal
__HOSTNAME__@__USERNAME__:~$ mv another-empty backup-of-emptyfile
__HOSTNAME__@__USERNAME__:~$ mv dir-copy subdir
__HOSTNAME__@__USERNAME__:~$ ls -ilR subdir
subdir/:
total 8
525370 drwxrwxr-x 2 __USERNAME__ __USERNAME__ 4096 Apr 06 05:36 dir-copy
525369 -rw-rw-r-- 1 __USERNAME__ __USERNAME__    6 Apr 06 05:33 textfile-copy

subdir/dir-copy:
total 4
525372 -rw-rw-r-- 1 __USERNAME__ __USERNAME__ 0 Apr 06 05:36 emptyfile
525371 -rw-rw-r-- 1 __USERNAME__ __USERNAME__ 6 Apr 06 05:33 textfile-copy
__HOSTNAME__@__USERNAME__:~$ █
:::

### Rename

Some systems have a `rename` command available. If not, use the `mv` command: `mv file-with-old-name same-file-with-new-name`.

## Delete

As you might expect, the rm command works in a similar way to the cp and mv commands: `rm backup-of-emptyfile` command deletes the `backup-of-emptyfile` file.

Files in different locations can also be deleted: `rm subdir/textfile-copy`.

You can use the rm command to delete entire directories, including their contents: `rm -r subdir/dir-copy` command deletes the `dir-copy` directory and its contents.

::: terminal
__HOSTNAME__@__USERNAME__:~$ rm backup-of-emptyfile
__HOSTNAME__@__USERNAME__:~$ rm subdir/textfile-copy
__HOSTNAME__@__USERNAME__:~$ rm -r subdir/dir-copy
__HOSTNAME__@__USERNAME__:~$ █
:::

::: note
As emphasised earlier, exercise caution when deleting files. There is no automatic backup or 'Trash' functionality for files deleted using the 'rm' command. In particular, it is easy to make a mistake when deleting directories recursively.
:::

That's it! You can now continue with the [Edit](06.1-edit.md) chapter.

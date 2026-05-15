# Files and directories

Let's start by creating some files. But first - make sure that you are in your home directory.

## Creating files

Type in a command: `touch emptyfile`.

::: terminal
__USERNAME__@__HOSTNAME__:~$ touch emptyfile
__USERNAME__@__HOSTNAME__:~$ █
:::

Verify that a file was created. For example with the `ls` command.

Then try out a command: `echo Hello World > textfile`. Again, verify that the file called `textfile` was created.

::: terminal
__USERNAME__@__HOSTNAME__:~$ echo Hello World > textfile
__USERNAME__@__HOSTNAME__:~$ ls
emptyfile  my-work  noppe-cli  textfile
__USERNAME__@__HOSTNAME__:~$ █
:::

Create yet another file called `d`.

## Creating directories

Type in a command: `mkdir directory`.

::: terminal
__USERNAME__@__HOSTNAME__:~$ mkdir directory
__USERNAME__@__HOSTNAME__:~$ █
:::

Verify that a directory called `directory` was created.

Then create another directory called `f`.

## Identifying files

List the content of your home directory with the `ls` command.

::: terminal
__USERNAME__@__HOSTNAME__:~$ ls
d  emptyfile  f  my-work  noppe-cli  textfile
__USERNAME__@__HOSTNAME__:~$ █
:::

After some time has passed, it can be difficult to identify files with obscure names. The `file` command can help you to identify the file type.

Let's identify all the files in our home directory.

::: terminal
__USERNAME__@__HOSTNAME__:~$ file d
d: empty
__USERNAME__@__HOSTNAME__:~$ file emptyfile
emptyfile: empty
__USERNAME__@__HOSTNAME__:~$ file f
f: directory
__USERNAME__@__HOSTNAME__:~$ file my-work
my-work: directory
__USERNAME__@__HOSTNAME__:~$ file noppe-cli
noppe-cli: directory
__USERNAME__@__HOSTNAME__:~$ file textfile
textfile: ASCII text
__USERNAME__@__HOSTNAME__:~$ █
:::

## Removing files and directories

Type in a command `rm emptyfile` to remove the `emptyfile`. Verify that the file was removed.

Then, try to remove the directory `f` with a command `rm f`.

::: terminal
__USERNAME__@__HOSTNAME__:~$ rm f
rm: cannot remove 'f': Is a directory
__USERNAME__@__HOSTNAME__:~$ █
:::

Try again with a command `rmdir f`. Verify that the directory was removed.

Next try to remove the directory `my-work` with a command: `rmdir my-work`.

::: terminal
__USERNAME__@__HOSTNAME__:~$ rmdir my-work
rmdir: failed to remove 'my-work': Directory not empty
__USERNAME__@__HOSTNAME__:~$ █
:::

::: beware
It is possible to delete an entire directory (`rm -fr`), including all its files and subdirectories, but let's not just now.
:::

Use the `rm` and `rmdir` commands to clean up the home directory and remove any other files and directories you have created, until only the `my-work` and `noppe-cli` directories remain.

Then let's have a look at [File properties](03.1-file-properties.md).

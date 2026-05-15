# Navigation

In a Linux system, files are organised into a hierarchical structure resembling a tree.

![File "tree"](imgs/navigation-file-tree.png)

The top-level directory is called the root directory and is marked with a slash (`/`).

::: tip
With the `tree` command you can generate a tree view of the file structure.
:::

You can change location within this structure using the `cd` command.

## Change the working directory (cd)

Now, change your location to the root directory: `cd /`.

::: terminal
__USERNAME__@__HOSTNAME__:~$ cd /
__USERNAME__@__HOSTNAME__:/$ █
:::

You can check your current location using the `pwd` command.

## Print name of current/working directory (pwd)

Type in the `pwd` command.

::: terminal
__USERNAME__@__HOSTNAME__:/$ pwd
/
__USERNAME__@__HOSTNAME__:/$ █
:::

You can view the directory contents using the `ls` command.

## List directory contents (ls)

Type in the `ls` command.

::: terminal
__USERNAME__@__HOSTNAME__:/$ ls
app  boot  etc   lib                lib64  mnt  proc    root  sbin  start  tmp  var
bin  dev   home  lib.usr-is-merged  media  opt  readme  run   srv   sys    usr
__USERNAME__@__HOSTNAME__:/$ █
:::

There are a total of 23 entries in the root directory.

## Back home again

Now, let's return to our home directory. 
   a) Type in `cd home`,
   b) use the `pwd` command to check your location,
   c) use the `ls` command to check the contents of the `home` directory.
   d) Type in `cd __USERNAME__` command.
   e) Again, check your location in the directory structure and the content of your home directory.

::: terminal
__USERNAME__@__HOSTNAME__:/$ cd home
__USERNAME__@__HOSTNAME__:/home$ pwd
/home
__USERNAME__@__HOSTNAME__:/home$ ls
ubuntu  __USERNAME__
__USERNAME__@__HOSTNAME__:/home$ cd __USERNAME__
__USERNAME__@__HOSTNAME__:~$ pwd
/home/__USERNAME__
__USERNAME__@__HOSTNAME__:~$ ls
my-work  noppe-cli
__USERNAME__@__HOSTNAME__:~$ █
:::

::: question
1. If you type in a command `cd ..` - what directory will you end up in?
2. If you try to enter user's `ubuntu` home directory - what happens?
:::

Next continue to [the Food for Thought of the Navigation](02.1-food-for-thought.md).

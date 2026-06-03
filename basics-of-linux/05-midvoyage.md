# Midvoyage

By now, you should be able to:
1. navigate the file structure and find your way around it.
2. recognise different file types.
3. discover new system commands and learn how to use them.

::: guidance
The most important thing is that you grasp the concepts of files and file structure.
:::

If any of this seems unclear, I strongly recommend rehearsing and strengthening your understanding of the concept of files and the file hierarchy of Linux operating systems.

::: service
Remember that you are the sole owner of the temporary Linux environment on the right. Explore it and feel free to experiment, for example with the commands below.
:::

## Spellbook

This list shows all the commands that you have used so far.

| Command | Example | Short description | Manual |
|-|-|-|-|
| `exit` | `exit` | cause the shell to exit | [man exit](https://man7.org/linux/man-pages/man1/exit.1p.html) |
| `export` | `export NAME=value` | sets the variable NAME to the value `value` | [man export](https://man7.org/linux/man-pages/man1/export.1p.html) |
| `tree` | `tree` | list contents of directories in a tree-like format | [man tree](https://linux.die.net/man/1/tree) |
| `cd` | `cd directory` | change the working directory | [man cd](https://man7.org/linux/man-pages/man1/cd.1p.html) |
| `pwd` | `pwd` | print name of current/working directory | [man pwd](https://man7.org/linux/man-pages/man1/pwd.1.html) |
| `ls` | `ls` | list directory contents | [man ls](https://man7.org/linux/man-pages/man1/ls.1.html) |
| `touch` | `touch somefile` | change file timestamps | [man touch](https://man7.org/linux/man-pages/man1/touch.1.html) |
| `echo` | `echo Hello World` | display a line of text | [man echo](https://man7.org/linux/man-pages/man1/echo.1.html) |
| `file` | `file /usr/bin/rm` | determine file type | [man file](https://man7.org/linux/man-pages/man1/file.1.html) |
| `mkdir` | `mkdir newdir` | make directories | [man mkdir](https://man7.org/linux/man-pages/man1/mkdir.1.html) |
| `rm` | `rm somefile` | remove files or directories | [man rm](https://man7.org/linux/man-pages/man1/rm.1.html) |
| `rmdir` | `rmdir directory` | remove empty directories | [man rmdir](https://man7.org/linux/man-pages/man1/rmdir.1.html) |
| `mv` | `mv oldname newname` | rename (move) a file | [man mv](https://man7.org/linux/man-pages/man1/mv.1.html) |
| `cat` | `cat somefile` | concatenate and print files | [man cat](https://man7.org/linux/man-pages/man1/cat.1.html) |
| `id` | `id` | print real and effective user and group IDs | [man id](https://man7.org/linux/man-pages/man1/id.1.html) |
| `chmod` | `chmod u+x file` | change file mode bits | [man chmod](https://man7.org/linux/man-pages/man1/chmod.1.html) |
| `dd` | `dd if=/dev/random of=file` | convert and copy a file | [man dd](https://man7.org/linux/man-pages/man1/dd.1.html) |
| `stat` | `stat somefile` | display file or file system status | [man stat](https://man7.org/linux/man-pages/man1/stat.1.html) |
| `ln` | `ln target link` | make links between files | [man ln](https://man7.org/linux/man-pages/man1/ln.1.html) |
| `du` | `du -h` | estimate file space usage | [man du](https://man7.org/linux/man-pages/man1/du.1.html) |
| `whereis` | `whereis rm` | locate the binary, source, and manual page files for a command | [man whereis](https://man7.org/linux/man-pages/man1/whereis.1.html) |
| `gcc` | `gcc main.c -o main` | GNU project C and C++ compiler | [man gcc](https://man7.org/linux/man-pages/man1/gcc.1.html) |
| `env` | `env` | set the environment for command invocation | [man env](https://man7.org/linux/man-pages/man1/env.1.html) |
| `grep` | `grep text fromfile` | search a file for a pattern | [man grep](https://man7.org/linux/man-pages/man1/grep.1.html) |
| `man` | `man rm` | display system documentation | [man man](https://man7.org/linux/man-pages/man1/man.1.html) |
| `cp` | `cp source dest` | copy files and directories | [man cp](https://man7.org/linux/man-pages/man1/cp.1.html) |
| `head` | `head somefile` | output the first part of files | [man head](https://man7.org/linux/man-pages/man1/head.1.html) |
| `tail` | `tail somefile` | output the last part of files | [man tail](https://man7.org/linux/man-pages/man1/tail.1.html) |
| `less` | `less somefile` | opposite of more | [man less](https://man7.org/linux/man-pages/man1/less.1.html) |
| `reset` | `reset` | terminal initialization | [man reset](https://man7.org/linux/man-pages/man1/reset.1.html) |
| `xxd` | `xxd binaryfile` | make a hex dump or do the reverse | [man xxd](https://linux.die.net/man/1/xxd) |
| `strings` | `strings binaryfile` | print the sequences of printable characters in files | [man strings](https://man7.org/linux/man-pages/man1/strings.1.html) |
| `nano` | `nano somefile` | Nano's ANOther editor, inspired by Pico | [man nano](https://linux.die.net/man/1/nano) |
| `vim` | `vim somefile` | Vi IMproved, a programmer's text editor | [man vim](https://linux.die.net/man/1/vim) |
| `source` | `source ~/.bashrc` | execute commands from a file in the current shell | [man source](https://man7.org/linux/man-pages/man1/dot.1p.html) |

Are you ready to continue your adventure? The [next chapter](06-working-with-files.md) awaits!

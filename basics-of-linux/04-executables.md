# Executables

This chapter could have been included as a subchapter of the previous chapter, 'Files and directories', but for now, let's give it its own chapter.

In Linux, executable files are scripts or compiled binaries.

## Script

Let's create the following simple script:

```bash
#!/bin/bash
echo "Hello world"
```

If you know how to use text editors such as Nano or Vim, feel free to help yourself! If not, don't worry. They will be covered in more detail in the chapter [Edit](06.1-edit.md) files.

For now, it is sufficient to type out a command `cat << EOF > scrp` and then the actual script followed by `EOF`.

It should look something like this:

::: terminal
__USERNAME__@__HOSTNAME__:~$ cat << EOF > scrp
&gt; #!/bin/bash
&gt; echo "Hello world"
&gt; EOF
__USERNAME__@__HOSTNAME__:~$ █
:::

Use the `ls` command to verify that you have successfully created a file called `scrp`. Then check what the `file scrp` command prints out.

::: terminal
__USERNAME__@__HOSTNAME__:~$ file scrp
scrp: Bourne-Again shell script, ASCII text executable
__USERNAME__@__HOSTNAME__:~$ █
:::

## Binary 

Let's create a simple C file:

```c
int main(void) {
return 0;
}
```

You can either use a text editor or enter the command `cat << EOF > main.c` as follows:

::: terminal
__USERNAME__@__HOSTNAME__:~$ cat << EOF > main.c
&gt; int main(void) {
&gt; return 0;
&gt; }
&gt; EOF
__USERNAME__@__HOSTNAME__:~$ █
:::

Check out the file type with a `file main.c` command and then compile the file into a binary called `bnry` with gcc: `gcc main.c -o bnry`.

Verify that the compilation has succeeded and that a file called `bnry` has appeared in your home directory. Then use the `file` command to check the info of `bnry`.

::: guidance
If you omit the `-o bnry` from the gcc command, the default output file is called `a.out`.
:::

So, in summary, the view should be as follows:

::: terminal
__USERNAME__@__HOSTNAME__:~$ file main.c
main.c: C source, ASCII text
__USERNAME__@__HOSTNAME__:~$ gcc main.c -o bnry
__USERNAME__@__HOSTNAME__:~$ ls
bnry  main.c  my-work  scrp
__USERNAME__@__HOSTNAME__:~$ file bnry
bnry: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=bd81384dbb49670453331f07c855728653ba4136, for GNU/Linux 3.2.0, not stripped
__USERNAME__@__HOSTNAME__:~$ █
:::

::: service
Did you notice the colour of the entry for <span class="text-green">bnry</span> in the output of the `ls` command? We came across this for the first time in the [File properties](03.1-file-properties.md) chapter.
:::

## Execute

Now, execute the `bnry` file with command `./bnry`. Then try to execute the same file with just `bnry`.

::: guidance
To execute files in the current directory, a [relative path](02.1-food-for-thought.md) reference must be provided before the file name.
:::

Then, let's try executing our `scrp` file. Try out both formats of the command: `./scrp` and `scrp`.

::: terminal
__USERNAME__@__HOSTNAME__:~$ ./bnry
__USERNAME__@__HOSTNAME__:~$ bnry
-bash: bnry: command not found
__USERNAME__@__HOSTNAME__:~$ ./scrp
-bash: scrp: Permission denied
__USERNAME__@__HOSTNAME__:~$ scrp
-bash: scrp: command not found
__USERNAME__@__HOSTNAME__:~$ █
:::

Notice how the executions `./scrp` and `scrp` produced different error messages. The first indicates that the file was found; the latter has the same error as the 'bnry' file.

Add execution [permission](03.1-file-properties.md) for the owner of the scrp file: `chmod u+x scrp` and then try to execute the file again.

::: terminal
__USERNAME__@__HOSTNAME__:~$ chmod u+x scrp
__USERNAME__@__HOSTNAME__:~$ ./scrp
Hello world
__USERNAME__@__HOSTNAME__:~$ █
:::

Remove the execute permission (`u-x`) from the `bnry` file, and then try executing it.

## System executables

You have now created and executed a couple of executable files yourself. The Linux operating system is full of executables that you have been using, such as `ls`, `rm`, `gcc`, `cat`, `rmdir`, `touch` and so on.

You can use the `whereis` command to find the files in the system. This prints the absolute path of the executable, which can then be examined using the `file` command.

First, execute the command `whereis rm`, then `file /usr/bin/rm`. Repeat for as many other system executables as you wish.

::: terminal
__USERNAME__@__HOSTNAME__:~$ whereis rm
/usr/bin/rm
__USERNAME__@__HOSTNAME__:~$ file /usr/bin/rm
/usr/bin/rm: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=c851b88cc2a078328d400214f39f232433195081, for GNU/Linux 3.2.0, stripped
__USERNAME__@__HOSTNAME__:~$ whereis fgrep
/usr/bin/fgrep
__USERNAME__@__HOSTNAME__:~$ file /usr/bin/fgrep
fgrep: POSIX shell script, ASCII text executable
__USERNAME__@__HOSTNAME__:~$ █
:::

The next chapter is about [Arguments](04.1-arguments.md).

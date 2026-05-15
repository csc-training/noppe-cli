# Executables

This chapter could have been included as a subchapter of the previous chapter, 'Files and directories', but for now, let's give it its own chapter.

In Linux, executable files are scripts or compiled binaries.

## Script

Let's create the following simple script:

```bash
#!/bin/bash
echo "Hello world"
```

If you know how to use text editors such as Nano or Vim, feel free to help yourself! If not, don't worry. They will be covered in more detail in the chapter [Edit](06.2-edit.md) files.

For now, it is sufficient to type out a command `cat << EOF > scrp` and then the actual script followed by `EOF`.

It should look something like this:

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ cat << EOF > scrp
&gt; #!/bin/bash
&gt; echo "Hello world"
&gt; EOF
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

Use the `ls` command to verify that you have successfully created a file called `scrp`. Then check what the `file scrp` command prints out.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ file scrp
scrp: Bourne-Again shell script, ASCII text executable
{{USERNAME}}@{{HOSTNAME}}:~$ █
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
{{USERNAME}}@{{HOSTNAME}}:~$ cat << EOF > main.c
&gt; int main(void) {
&gt; return 0;
&gt; }
&gt; EOF
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

Check out the file type with a `file main.c` command and then compile the file into a binary called `bnry` with gcc: `gcc main.c -o bnry`.

Verify that the compilation has succeeded and that a file called `bnry` has appeared in your home directory. Then use the `file` command to check the info of `bnry`.

::: guidance
If you omit the `-o bnry` from the gcc command, the default output file is called `a.out`.
:::

So, in summary, the view should be as follows:

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ file main.c
main.c: C source, ASCII text
{{USERNAME}}@{{HOSTNAME}}:~$ gcc main.c -o bnry
{{USERNAME}}@{{HOSTNAME}}:~$ ls
bnry  main.c  my-work  scrp
{{USERNAME}}@{{HOSTNAME}}:~$ file bnry
bnry: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=bd81384dbb49670453331f07c855728653ba4136, for GNU/Linux 3.2.0, not stripped
{{USERNAME}}@{{HOSTNAME}}:~$ █
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
{{USERNAME}}@{{HOSTNAME}}:~$ ./bnry
{{USERNAME}}@{{HOSTNAME}}:~$ bnry
-bash: bnry: command not found
{{USERNAME}}@{{HOSTNAME}}:~$ ./scrp
-bash: scrp: Permission denied
{{USERNAME}}@{{HOSTNAME}}:~$ scrp
-bash: scrp: command not found
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

Notice how the executions `./scrp` and `scrp` produced different error messages. The first indicates that the file was found; the latter has the same error as the 'bnry' file.

Add execution [permission](03.1-file-properties.md) for the owner of the scrp file: `chmod u+x scrp` and then try to execute the file again.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ chmod u+x scrp
{{USERNAME}}@{{HOSTNAME}}:~$ ./scrp
Hello world
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

Remove the execute permission (`u-x`) from the `bnry` file, and then try executing it.

## System executables

You have now created and executed a couple of executable files yourself. The Linux operating system is full of executables that you have been using, such as `ls`, `rm`, `gcc`, `cat`, `rmdir`, `touch` and so on.

You can use the `whereis` command to find the files in the system. This prints the absolute path of the executable, which can then be examined using the `file` command.

First, execute the command `whereis rm`, then `file /usr/bin/rm`. Repeat for as many other system executables as you wish.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ whereis rm
/usr/bin/rm
{{USERNAME}}@{{HOSTNAME}}:~$ file /usr/bin/rm
/usr/bin/rm: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=c851b88cc2a078328d400214f39f232433195081, for GNU/Linux 3.2.0, stripped
{{USERNAME}}@{{HOSTNAME}}:~$ whereis fgrep
/usr/bin/fgrep
{{USERNAME}}@{{HOSTNAME}}:~$ file /usr/bin/fgrep
fgrep: POSIX shell script, ASCII text executable
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

The next chapter is about [Arguments](04.1-arguments.md).

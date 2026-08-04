# Redirections

The concept of redirection is straightforward, but it is introduced this late in the course because a number of other topics must first be understood in order to utilise and appreciate the need for it properly.

Let's try out these two simple commands: `echo Hello world` and `ls noexist`.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ echo Hello world
Hello world
{{USERNAME}}@{{HOSTNAME}}:~$ ls noexist
ls: cannot access 'noexist': No such file or directory
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

As mentioned in Chapter [4.2 Standard Streams](04.2-standard-streams.md), the normal output of a command is sent to the standard output (`stdout`, file descriptor `1`), while error messages are sent to the standard error output (`stderr`, file descriptor `2`).

Next, try out the following commands next: `echo Hello world 1> hello-fd1`, `echo Hello world 2> hello-fd2`. `ls noexist 1> ls-fd1` and `ls noexist 2> ls-fd2`.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ echo Hello world 1> hello-fd1
{{USERNAME}}@{{HOSTNAME}}:~$ echo Hello world 2> hello-fd2
Hello world
{{USERNAME}}@{{HOSTNAME}}:~$ ls noexist 1> ls-fd1
ls: cannot access 'noexist': No such file or directory
{{USERNAME}}@{{HOSTNAME}}:~$ ls noexist 2> ls-fd2
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

Check the contents of each file using the `cat` command.

::: tip
You can omit the `1` from `1>`, since `stdout` is the default. The number one is written out above to emphasise the connection between redirection and file descriptor numbers.
:::

Next, enter the following command: `ls . noexist`. This prints the contents of the current directory to stdout and the error message to stderr. By default, both are printed to the terminal.

::: note
The `ls` command above takes two arguments: `.` and `noexist`.
:::

Now, let's redirect both streams to their own files while preventing anything from being printed to the terminal: `ls . noexist > ls-out 2> ls-err`.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ ls . noexist
ls: cannot access 'noexist': No such file or directory
.:
hello-fd1  hello-fd2  ls-fd1  ls-fd2  my-work  noppe-cli
{{USERNAME}}@{{HOSTNAME}}:~$ ls . noexist > ls-out 2> ls-err
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

Verify that the `ls-out` and `ls-err` files were created and check their contents.

Both streams can be redirected to the same file using the following command, for example: `ls . noexist > ls-both 2>&1`.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ ls . noexist > ls-both 2>&1
{{USERNAME}}@{{HOSTNAME}}:~$ cat ls-both
ls: cannot access 'noexist': No such file or directory
.:
hello-fd1
hello-fd2
ls-both
ls-err
ls-fd1
ls-fd2
ls-out
my-work
noppe-cli
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

The `2>&1` can be interpreted as meaning 'redirect file descriptor 2 into file descriptor 1'.

::: tip
In Bash, `cmd &> file` redirects both stdout and stderr of 'cmd' to the `file`, which is equivalent to `cmd > file 2>&1`.
:::

## Append

Using `>` for redirection will overwrite any existing file. To append to an existing file, use `>>`. Both formats will create the file if it does not already exist.

Execute the command `echo Hello world >> echo-append` three times in a row.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ echo Hello world >> echo-append
{{USERNAME}}@{{HOSTNAME}}:~$ echo Hello world >> echo-append
{{USERNAME}}@{{HOSTNAME}}:~$ echo Hello world >> echo-append
{{USERNAME}}@{{HOSTNAME}}:~$ cat echo-append 
Hello world
Hello world
Hello world
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

<!--
:::quiz q-linux-16
:::
-->

The append syntax also works when redirecting errors or both streams.

### Input redirection (<)

Although input redirection is rarely necessary in practice, it is helpful to have a basic understanding of the concept. Some commands only operate through input redirection, so you may encounter it at some point when using Linux.

While we're on the topic, let's have some fun with it! Open a text editor (either Nano or Vim) and enter the following:

```txt
touch fruits.txt
echo pineapple > fruits.txt
echo banana >> fruits.txt
echo mango >> fruits.txt
echo orange >> fruits.txt
echo apple >> fruits.txt
```

Save the file as `fruit-maker`.

::: note
Note the distinction from the bash script, though it is minuscule. Omit the shebang from the beginning of the file and do not make it executable.
:::

Then enter the command `bash < fruit-maker`. Verify the result using the `ls` and `cat fruits.txt` commands.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ vim fruit-maker
{{USERNAME}}@{{HOSTNAME}}:~$ bash < fruit-maker
{{USERNAME}}@{{HOSTNAME}}:~$ ls
fruits.txt  my-work  noppe-cli
{{USERNAME}}@{{HOSTNAME}}:~$ cat fruits.txt
pineapple
banana
mango
orange
apple
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

::: tip
Think of the `fruit-maker` file as containing a series of keystrokes that you would need to perform anyway to achieve the desired result.
:::

For example, the `tr` command does not accept a file name as an argument. Try out the following command: `tr a-z A-Z < fruits.txt`. Then try the same command again, but without the `<` character.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ tr a-z A-Z < fruits.txt
PINEAPPLE
BANANA
MANGO
ORANGE
APPLE
{{USERNAME}}@{{HOSTNAME}}:~$ tr a-z A-Z fruits.txt
tr: extra operand ‘fruits.txt’
Try 'tr --help' for more information.
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

Alternatively, pipe the contents of `fruits.txt` into the `tr` command to achieve the same result: `cat fruits.txt | tr a-z A-Z`.

## Pipes

Piping is one of the most powerful features of *NIX operating systems. The Unix philosophy involves connecting the output of one command with the input of another, alongside the idea that 'each program should do one thing well'.

This enables you to combine small commands to create larger entities, providing infinite flexibility and helping you achieve the desired results.

Try entering the following command:

`ps -ef | tail -n +2 | sed -n '3p;5p' | awk '{print $2}' | paste -sd- | bc`

You don't need to fully understand what this command does, but it's a great example of the power of piping.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 09:31 ?        00:00:00 /usr/bin/tini -- /start
root           7       1  0 09:31 ?        00:00:00 caddy run --config /etc/caddy/Caddyfile
root          13       7  0 09:31 ?        00:00:00 ttyd -W -p 7681 login
munge         47       1  0 09:31 ?        00:00:00 /usr/sbin/munged
root          68       1  0 09:31 ?        00:00:00 slurmd
slurm         72       1  0 09:31 ?        00:00:00 slurmctld
slurm         73      72  0 09:31 ?        00:00:00 : slurmscriptd
root          98      13  0 09:31 pts/0    00:00:00 login
user         109      98  0 09:32 pts/0    00:00:00 -bash
user         121     109  0 09:32 pts/0    00:00:00 ps -ef
{{USERNAME}}@{{HOSTNAME}}:~$ ps -ef | tail -n +2 | sed -n '3p;5p' | awk '{print $2}' | paste -sd- | bc
-55
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

It finds the PID numbers and displays the difference between the third (`ttyd` with pid `13`) and fifth (`slurmd` with pid `68`) running commands.

In this example, the number is `-55`, but yours will most likely be different.

::: guidance
It is worth noting that piping commands is not always necessary. Consider the `fruits.txt` file, for example, and imagine that you want to search for the word `banana`. While the command `cat fruits.txt | grep banana` would work, it is better to simply type `grep banana fruits.txt`.
:::

## tee

Enter the command `sort < fruits.txt`. This will sort the entries in the file alphabetically and display the results in the terminal.

Next, enter the command `sort < fruits.txt > sorted.txt`. This time, the results are redirected to a file.

Delete the `sorted.txt` file, then run the command `sort < fruits.txt | tee sorted.txt`. Check that the command's output was displayed **and** that the `sorted.txt` file was created with the desired content.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ sort < fruits.txt | tee sorted.txt
apple
banana
mango
orange
pineapple
{{USERNAME}}@{{HOSTNAME}}:~$ ls
fruits.txt  my-work  noppe-cli  sorted.txt
{{USERNAME}}@{{HOSTNAME}}:~$ cat sorted.txt
apple
banana
mango
orange
pineapple
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

As its name suggests (the physical shape of the letter `T`), the `tee` command splits the standard output so that it can be stored and processed further. Again remove the `sorted.txt` file with the `rm sorted.txt` command and then enter the following command: `sort < fruits.txt | tee sorted.txt | tr a-z A-Z > SORTED.txt`.

Despite using the `tee` command, you will notice that nothing is printed to the terminal window this time. However, the standard output was stored in the `sorted.txt` file, processed further and then stored in the `SORTED.txt` file.

Check the contents of both 'sorted' files.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ sort < fruits.txt | tee sorted.txt | tr a-z A-Z > SORTED.txt
{{USERNAME}}@{{HOSTNAME}}:~$ cat sorted.txt
apple
banana
mango
orange
pineapple
{{USERNAME}}@{{HOSTNAME}}:~$ cat SORTED.txt
APPLE
BANANA
MANGO
ORANGE
PINEAPPLE
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

<!--
:::quiz q-linux-17
:::
-->

You can now move on to the [Food for Thought](08.1-food-for-thought.md) section of the chapter.

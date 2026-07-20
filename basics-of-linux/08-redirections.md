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
echo-fd1  echo-fd2  ls-fd1  ls-fd2  my-work  noppe-cli
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
echo-fd1
echo-fd2
ls-fd1
ls-fd2
ls-both
my-work
noppe-cli
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

The `2>&1` can be interpreted as meaning 'redirect file descriptor 2 into file descriptor 1'.

::: tip
In Bash, you can use the shorthand `&>` instead of `2>&1`.
:::

## Append

Using '>' for redirection will overwrite any existing file. To append to an existing file, use '>>'. Both formats will create the file if it does not already exist.

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

The append syntax also works when redirecting errors or both streams.

### Input redirection (<)

## Pipes

Piping is one of the most powerful features of *NIX operating systems. The Unix philosophy involves connecting the output of one command with the input of another, alongside the idea that 'each program should do one thing well'.

This enables you to combine small commands to create larger entities, providing infinite flexibility and helping you achieve the desired results.

Try entering the following command:

`ps -ef | tail -n +2 | sed -n '3p;5p' | awk '{print $2}' | paste -sd- | bc`

You don't need to fully understand what this command does, but it's a great example of piping. 

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
{{USERNAME}}@{{HOSTNAME}}:~$ ps -ef | tail -n +2 | sed -n '3p;5p' | awk '{print $2}' | paste -sd- | bc`
-55
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

It finds the PID numbers and displays the difference between the third (`ttyd` with pid `13`) and fifth (`slurmd` with pid `68`) running commands.

In this example, the number is `-55`, but yours will most likely be different.

::: guidance
It is worth noting that piping commands is not always necessary. Consider the `fruits.txt` file, for example, and imagine that you want to search for the word `bananas`. While the command `cat fruits.txt | grep bananas` would work, it is better to simply type `grep bananas fruits.txt`.
:::

## tee

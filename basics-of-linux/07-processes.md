# Processes

Run the command: `pstree -p`.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ pstree -p
tini(1)─┬─caddy(7)─┬─ttyd(13)─┬─login(110)───bash(121)───pstree(137)
        │          │          └─{ttyd}(111)
        │          ├─{caddy}(84)
...
        │          └─{caddy}(109)
        ├─munged(57)─┬─{munged}(58)
        │            ├─{munged}(59)
        │            └─{munged}(60)
        ├─slurmctld(81)─┬─slurmscriptd(82)
...
        │               └─{slurmctld}(100)
        └─slurmd(78)
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

The numbering in your document will most likely differ from that in the example.

::: note
The `pstree` command works in the same way as the `tree` command does for directories and files, but for running processes.
:::

Then, run the command: `ps -ef`

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ ps -ef
ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 07:27 ?        00:00:00 /usr/bin/tini -- /start
root           7       1  0 07:27 ?        00:00:00 caddy run --config /etc/caddy/Caddyfile
root          13       7  0 07:27 ?        00:00:00 ttyd -W -p 7681 login
munge         57       1  0 07:27 ?        00:00:00 /usr/sbin/munged
root          78       1  0 07:27 ?        00:00:00 slurmd
slurm         81       1  0 07:27 ?        00:00:00 slurmctld
slurm         82      81  0 07:27 ?        00:00:00 : slurmscriptd
root         110      13  0 07:27 pts/0    00:00:00 login
{{USERNAME}}         121     110  0 07:28 pts/0    00:00:00 -bash
{{USERNAME}}         138     121  0 07:31 pts/0    00:00:00 ps -ef
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

A process is [a program that is being executed](04-executables.md). These programs are organised in a hierarchy based on their process IDs (PID).

## Process identifier (PID)

The first process, init, is assigned a PID of `1`; all other running processes are either direct or indirect descendants of init. Newly launched processes are assigned a PID greater than that of any currently running processes.

Since processes are launched hierarchically, each process has a parent process. The init process has a parent process ID of `0` (PPID).

::: note
More precisely, processes never just appear randomly; they are always initiated by another process.
:::

Type the command `echo $$`. This will display the PID of the current process.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ echo $$
121
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

In this example, it is `121`.

::: question
Can you identify the PID `121` in the example printouts above? What is the name of the process? What is its parent process ID (PPID)? Can you also locate your own PID in the `pstree` and `ps` outputs from your execution?
:::

## Listing processes

You have already used the `pstree` and `ps` commands to list the currently running processes. Please refer to the manual pages for these commands to see the various output options available.

These two commands provide a snapshot of the running processes. To see a live view of running processes, use the `top` command.

::: terminal
top - 09:21:31 up  2:03,  0 user,  load average: 0.00, 0.00, 0.00
Tasks:  10 total,   1 running,   9 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.1 us,  0.2 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
MiB Mem :   7750.2 total,   5593.4 free,    902.9 used,   1507.4 buff/cache     
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   6847.3 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND             
      7 root      20   0 1268012  40824  30228 S   0.3   0.5   0:00.62 caddy
     81 slurm     20   0  816940  10848   7188 S   0.3   0.1   0:05.65 slurmctld
      1 root      20   0    2692   1592   1504 S   0.0   0.0   0:00.10 tini
     13 root      20   0   18732   5336   4444 S   0.0   0.1   0:00.19 ttyd
     57 munge     20   0  203716   4180   3584 S   0.0   0.1   0:00.00 munged
     78 root      20   0   79712   6220   5108 S   0.0   0.1   0:00.00 slurmd
     82 slurm     20   0    7836   2940   2420 S   0.0   0.0   0:00.00 slurmscriptd
    110 root      20   0    6752   4596   3900 S   0.0   0.1   0:00.03 login
    121 {{USERNAME}}      20   0    6052   5336   3720 S   0.0   0.1   0:00.00 bash
    124 {{USERNAME}}      20   0    9388   5660   3428 R   0.0   0.1   0:00.00 top
:::

Press the `q` key to exit the `top` view.

## Running a process

Every time you run a command, a process is launched. Therefore, you have essentially been running processes the whole time.

While some of these processes (i.e. `ls`) last only a very short time, they all receive similar treatment and are assigned their own process ID and parent process ID.

On the other hand, some processes might take a very long time to execute. Let's demonstrate this using the `sleep 1000` command.

The command simply makes the system wait for 1000 seconds, so it takes around 17 minutes to exit. Now, interrupt and terminate the command by pressing `Ctrl+C`.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ sleep 1000
^C
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

But what if you're running an important command that you don't want to end?

::: note
`Ctrl+C`, and later the `Ctrl+Z`, are about sending signals to running processes. `Ctrl+C` sends `SIGINT`, and `Ctrl+Z` sends `SIGTSTP`. You can find out more about this topic in the [Killing a process](07-processes.md#killing-a-process) chapter below.
:::

### Background execution

Run the `sleep 1000` command again, but this time interrupt it with `Ctrl+Z`. This will change the process to a _Stopped_ state. Then use the `bg` command to resume execution in the **background**.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ sleep 1000
^Z
[1]+  Stopped                 sleep 1000
{{USERNAME}}@{{HOSTNAME}}:~$ bg
[1]+ sleep 1000 &
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

Use the `ps` and/or `pstree` commands to verify that the `sleep 1000` command is listed among the running processes.

::: tip
If you know the command will take time to execute, you can move it to background execution directly by adding a `&` sign to the end of the command: `sleep 1000 &`.
:::

Let's have an exercise next.

::: guidance
This exercise requires your undivided attention. Although it gets a bit messy, it provides a comprehensive overview of what to consider when managing processes.
:::

First, enter the command `sleep 1000 &`. Pay attention to the numbers printed out. Then run the command `ls -l &`. Yes, make sure you add the `&` at the end of the `ls` command. Again, pay attention to the output.

Press `Enter ↵` to show the prompt again. Next, copy and paste the following command: `while true; do sleep 2; echo Hello;done &`, and press `Enter ↵` to send it to background execution.

This prints the word `Hello` to the console every two seconds.

**Ignore** the `Hello` text, type `fg` and press `Enter ↵`. Then press `Ctrl+C`.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ sleep 1000 &
[1] 136
{{USERNAME}}@{{HOSTNAME}}:~$ ls -l &
[2] 137
{{USERNAME}}@{{HOSTNAME}}:~$ total 5
drwxr-xr-x 2 {{USERNAME}} {{USERNAME}} 0 Dec  6 13:37 my-work
drwxr-xr-x 2 {{USERNAME}} {{USERNAME}} 0 Dec  6 13:37 noppe-cli

[2]+  Done                    ls --color=auto -l
{{USERNAME}}@{{HOSTNAME}}:~$ while true; do sleep 2; echo Hello;done &
[1] 138
{{USERNAME}}@{{HOSTNAME}}:~$ Hello
Hello
Hello
fg
while true; do
    sleep 2; echo Hello;
done
Hello
Hello
^C
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

The key takeaway from this exercise is as follows:

::: beware
If your command produces output to the `stdout`, [redirect](08-redirections.md) it to a file before launching it in the background.
:::

Other points to note:

- When a process is started in the background, the job ID  (e.g. `[2]`) and process ID (e.g. `137`) are printed on the screen. As can be seen here, the short-lived `ls` command indeed has its own PID too.

- The `bg` command sends the most recently stopped process to the background. The `fg` command restores the most recently backgrounded job to the foreground. In this case, it is the misbehaving printer while loop.

- You can use the `jobs` command to list all background jobs started from the current shell session.

::: note
Any background processes started in the current shell session will terminate when the session ends. To prevent this, use `tmux`, `screen` or an equivalent environment.
:::

## Killing a process

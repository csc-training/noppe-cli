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

Next, we will take a closer look at [listing processes](07.1-listing.md).

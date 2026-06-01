# Introduction

Although you may encounter Linux in desktop environments, it is most likely that you will use it as a remote server.

Server environments are accessed via a command line interface, like the one on the right.

You are here to learn how to use one, so let's get started.

## Logging in

First, log in the Linux machine. The login is `{{USERNAME}}` and `{{PASSWORD}}`:

::: terminal
{{HOSTNAME}} login: {{USERNAME}}
Password:
:::

::: guidance
Please note that nothing is shown when you type in the password. But it is there. Accept your input with `Enter ↵`.
:::

After successful login, you should have the following view:

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ █
:::

## Logging out

Now, it is a good habit to always exit a session if you don't need it anymore.

Type in a command `exit` and press `Enter ↵`.

You managed to log out? Great!

Now log back in and continue to [the CLI chapter](01.1-cli.md).

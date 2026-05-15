# Introduction

Although you may encounter Linux in desktop environments, it is most likely that you will use it as a remote server.

Server environments are accessed via a command line interface, like the one on the right.

The Linux environment on the right is a functional Linux operating system that runs in a container. This means that you can perform the same actions as on most other Linux systems, but _without risking any damage to the operating system_.

However, this also means that the operating state or modified files (or files you create) are not stored, when the environment is restarted.

## Logging in

First, log in the Linux machine. The login is `__USERNAME__` and `__PASSWORD__`:

::: terminal
__HOSTNAME__ login: __USERNAME__
Password:
:::

::: guidance
Please note that nothing is shown when you type in the password. But it is there. Accept your input with an enter.
:::

After successful login, you should have the following view:

::: terminal
__USERNAME__@__HOSTNAME__:~$ █
:::

## Logging out

Now, it is a good habit to always exit a session if you don't need it anymore.

Type in a command `exit` and press enter.

You managed to log out? Great!

Now log back in and continue to [the Food for Thought of the Introduction](01.1-food-for-thought.md).

# Getting Started

This is a Noppe powered command-line learning environment.

The Linux environment on the right is a functional Linux operating system that runs in a container. This means that you can perform the same actions as on most other Linux systems, but _without risking any damage to the operating system_.

However, this also means that the operating state or modified files (or files you create) are not stored, when the environment is restarted.

## Logging in

The login is `{{USERNAME}}` and `{{PASSWORD}}`.

## Environment

The home directory contains the `my-work` and `noppe-cli` directories by default. The `my-work` directory is mounted on permanent storage when the application is used in a Noppe workspace by the teacher. The `noppe-cli` directory contains learning materials and is cloned from the CSC training GitHub repository.

The current Linux version running in the container is Ubuntu 24.04 LTS, but you can verify the exact version using the command `cat /etc/os-release`.

### search

The search functionality is harnessed as a 'grep exercise'.

The material is available as plain text in md files in the `noppe-cli` directory. Use the [grep command](basics-of-linux/06.1-view.md#grep) to search for topics or keywords that interest you.

For example, entering the command: `grep '\bgrep\b' basics-of-linux/*.md` will locate all md files containing the word `grep` in [Basics of Linux](basics-of-linux/00-toc.md) material.

To see only the titles containing the word 'grep', use the command `grep -i "^#.*grep" basics-of-linux/*.md`.

# In education

If you would like to use this environment in a more controlled way for teaching purposes and have the `my-work` permanent storage enabled, for example, consider using the Noppe Workspaces as a teacher. Further information is available on the CSC Docs website: [Noppe Guide for teachers and collaborators](https://docs.csc.fi/cloud/noppe/guide_for_teachers/).

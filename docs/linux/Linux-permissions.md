---
layout: default
title: Linux Permissions
parent: Linux
nav_order: 3
---

# Linux permissions on files and directories

Permissions specify what a particular person may or may not do with respect to a file or directory. This system provide security at the file system level. Here is the [Ryan's tutorial on linux permissions][tutorial-permissions].

A chart to remember how linux permissions work.

![linux-permissions](../../assets/images/mode.png)

## Note on the creation of new file and directory

`chmod g+s <directory>`

When using `chmod`, setting directories `g+s` makes all new files and directories created in said directory have their group set to the directory's group. This is especially useful for the project space of the laboratory to make sure files stay set to the laboratory's group

[tutorial-permissions]: https://ryanstutorials.net/linuxtutorial/permissions.php

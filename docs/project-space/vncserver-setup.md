---
layout: default
title: Setup your VNC server
parent: Working On The Project Space
nav_order: 1
---

This tutorial explain you how to connect to `guillimin` with a graphical desktop interface.

# Setup of your VNC server

You need to do the steps in this section only one time. Go to the next [section](../vncserver-launch) if you have already done this.

# Install VNC client

Install the VNC client [TigerVNC][tigervnc] on your computer. The `client` software is able to connect your computer to another computer.

# VNC init

Log into the visualization node, and type `vncserver`. It will ask for a password. This password is used to access the virtual desktop you create on the server.

`vncserver`

The command `vncserver` you just type already created a server. You won't need it so you should kill it properly. Type `vncserver -list` to find out the `X DISPLAY #` and then execute `vncserver -kill :<display number>`. Most of the time it's `vncserver -kill :1`.

Example:
```
$ vncserver -list

TigerVNC server sessions:

X DISPLAY #	PROCESS ID
:6		25607

$ vncserver -kill :6
Killing Xvnc process ID 25607

$ vncserver -list

TigerVNC server sessions:

X DISPLAY #	PROCESS ID

```

# Copy the scripts from the guillimin team

`cp -a /software/workshop/vnc ~/`

This copy the scripts made by the guillimin team to setup a VNC sessions. This will create a new `vnc` folder in your home directory.

[tigervnc]: http://tigervnc.org/

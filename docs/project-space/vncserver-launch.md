---
layout: default
title: Working with VNC server
parent: Working On The Project Space
nav_order: 2
---

This tutorial explain you how to connect to `guillimin` with a graphical desktop interface.

# Setup of your environment

You should have already done this [setup](../vncserver-setup) before using vncserver.

# Introduction

The goal is to setup a `vncserver` on the visualization node of the server, create a ssh tunnel from your computer and connect to this node with the vnc client.

![vnc-schema]({{site.baseurl}}/assets/images/vnc-schema.png)

[More info here][usermeeting-vnc], it begins slide 14.

# Launching a server with the helper script

## xstartup file

First You should have a file `~/.vnc/xstartup` with this content :

```
#!/bin/sh
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
mate-session &
```

## server creation

From the visualization node, launch a vncserver with the `vl_vncserver` script.

```
$ vl_vncserver -h

Script to use on the visualization login node of the Villeneuve Lab
 -1- Launch this script from the visualization login node
 -2- Create the ssh tunnel from your local computer by copy-pasting
     the ssh command
 -3- Open TigerVNC from your local computer using `localhost:159XX`
     Replace XX by the correct display number

Usage: vl_vncserver -t <time limit in hour(s)>
```

### Example for a session a 3 hours

```bash
cbedetti@lg-3r03-n01:~ $ vl_vncserver -t 3

> The vncserver will be available for 3 hour(s)
> Open a new terminal on your local machine and create the ssh tunnel :
> ssh -L 15902:lg-3r03-n01:5902 cbedetti@guillimin1.calculquebec.ca
```

## server check

You can check the vncservers already running with `vncserver -list`

## closing your session

For good practice, if you are done before the time you requested, use the `killSleep.sh` script provided by the guillimin team in the `~/vnc` folder to end your session :)

`~/vnc/killSleep.sh`

[usermeeting-vnc]: http://www.hpc.mcgill.ca/downloads/user_meetings/McGillHPC-UsersMeeting-VNC-X2Go-XQuartz-20170413.pdf

---
layout: default
title: Connect to a server with a graphical desktop
nav_exclude: true
---

# This page is old and kept only for archive

This tutorial explain you how to connect to `guillimin` with a graphical desktop interface.

# Setup of your environment

You need to do the steps in this section only one time. Go to the next [section](./Connect-to-a-server-with-a-graphical-desktop#setup-of-a-vnc-session) if you have already done this.

### Install VNC client

Install the VNC client [TigerVNC][tigervnc] on your computer. The `client` software is able to connect your computer to another computer.

### VNC init

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

### Copy the scripts from the guillimin team

`cp -a /software/workshop/vnc ~/`

This copy the scripts made by the guillimin team to setup a VNC sessions. This will create a new `vnc` folder in your home directory.

# Setup of a VNC session

The goal is to setup a `vncserver` on one of the worker node of the server, create a ssh tunnel from your computer and connect to the worker node with the vnc client.

If you login on the server and type `vncserver` directly, a server will be create on a login node. Login nodes are not powerfull and your VNC session will be very slow, so don't do that.

![vnc-schema](/assests/images/vnc-schema.png)

### setup `vncserver` on one of the worker node

Log into guillimin as usual.

`ssh <your_username>@guillimin.hpc.mcgill.ca`

Submit the script of the guillimin team to setup a VNC session

`qsub ~/vnc/vncserver.sh`

Check the state of your job. Wait for your vnc job to be in the running (R) state.

`showq -r -u <your_username>`

When your job is in a running state, you have to find two data:
1. `worker_node`: the address of the worker node
2. `XY`: the port number

#### 1. `worker_node`

It is the `MHOST` column when you run `showq -r -u <your_username>`. In the next example, it is `hb-2r03-n25`

```
$ showq -r -u <your_username>

active jobs------------------------
JOBID               S  PAR  EFFIC  XFACTOR  Q  USERNAME    GROUP            MHOST PROCS   REMAINING            STARTTIME

5661495             R  gm-   1.21      1.0 no  <your_username> xxx-111-      hb-2r03-n25    12    11:57:57  Mon May  7 17:21:07
```

#### 2. `XY`

To find this information, list files inside `~/.vnc` folder.

```
$ ls -lrt .vnc/
total 1152
-rw-------  1 <your_username> xxx-111-01     8 May  7 16:51 passwd
-rwxr-xr-x  1 <your_username> xxx-111-01   654 May  7 16:51 xstartup
-rw-r--r--  1 <your_username> xxx-111-01  4848 May  7 16:52 lg-1r17-n02:1.log
-rw-r--r--  1 <your_username> xxx-111-01     4 May  7 17:21 hb-2r03-n25:1.pid
-rw-r--r--  1 <your_username> xxx-111-01  3488 May  7 17:21 hb-2r03-n25:1.log
```

Find the newest line with your worker node, `hb-2r03-n25:1` here. The port is the number after `:`. Here, it is `1` so  the port number `XY` will be `01`.

### SSH tunnel

Now that we have all the information, we can create the connection (SSH tunnel) between your computer and the worker node. **Open a new terminal window on your computer**. Replace `worker_node`, `XY` and `<your_username>` by the right informations.

`ssh -L 159XY:worker_node:59XY <your_username>@guillimin.hpc.mcgill.ca`

### Helper script

`vl_vnc_tunnel_command`

Run this script after the `qsub` command. When the vncserver is running it will output the ssh tunnel command. It won't work correctly if you open several vnc sessions at the same time.

### VNC client

Open the VNC client on your computer. In the identification at the top, enter: `localhost:159XY` (in this example `localhost:15901`). It will ask you for a password. This is the one you created in the first section.

Once the authentication worked, simply enter your guillimin credentials (username and password) and you can work on this interface for the time you submitted the VNC job.

For good practice, if you are done before the time you requested, use the `killSleep.sh` script provided by the guillimin team in the `~/vnc` folder to end your session :) 

[More info here][usermeeting-vnc], it begins slide 14.

[tigervnc]: http://tigervnc.org/
[usermeeting-vnc]: http://www.hpc.mcgill.ca/downloads/user_meetings/McGillHPC-UsersMeeting-VNC-X2Go-XQuartz-20170413.pdf

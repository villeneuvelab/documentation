---
layout: default
title: Working with VNC server
parent: Working On The Project Space
nav_order: 2
---

This tutorial explain you how to connect to `beluga` with a graphical desktop interface.

This page is summary of the Compute Canada VNC documentation. Follow this link for more [information][cc-vnc].

# Setup of your environment

You should have already done this [setup](../vncserver-setup) before using vncserver.

# Introduction

The goal is to setup a `vncserver` on the visualization node of the server, create a ssh tunnel from your computer and connect to this node with the vnc client.

![vnc-schema]({{site.baseurl}}/assets/images/vnc-schema.png)

[More info here][usermeeting-vnc], it begins slide 14.

# Launching a server with the helper script

## server creation

From a worker node, launch a vncserver with the `vl_vncserver` script.

```
$ vl_vncserver -h

Usage: vl_vncserver -t <time limit in hour(s)>

Script to use during an interactive job on beluga
    -1- Reserve a node on which running vncserver.
        salloc -c 4 --mem 16000M --account=ctb-villens
    -2- Launch this script from the worker node
    -3- Create the ssh tunnel from your local computer by copy-pasting
        the ssh command
    -4- Open TigerVNC from your local computer using localhost:159XX
        Replace XX by the correct display number
```

## Example for a session of 3 hours

- Reserve a worker node

```bash
cbedetti@beluga2:~ $ salloc -c 4 --mem 16000M --account=ctb-villens

> salloc: Pending job allocation 156301
> salloc: job 156301 queued and waiting for resources
> salloc: job 156301 has been allocated resources
> salloc: Granted job allocation 156301
> salloc: Waiting for resource configuration
> salloc: Nodes blg8610 are ready for job
```

- Start the vncserver  with `vl_vncserver`

```bash
cbedetti@blg8610:~ $ vl_vncserver -t 3

> The vncserver will be available for 3 hour(s)
> Open a new terminal on your local machine and create the ssh tunnel :
> ssh -L 15902:blg8610:5902 cbedetti@beluga.calculquebec.ca
```

- Create the ssh tunnel (copy-paste the output ssh command in a new terminal)
- Open TigerVNC and fill the right number

![TigerVNC-img]({{site.baseurl}}/assets/images/tigervnc-launch.png)

## Deactivate screensaver

For stability issues, deactivate the screensaver : System > Preferences > Look and Feel > Screensaver

![screensaver-img]({{site.baseurl}}/assets/images/screensaver.png)

## server check

You can check the vncservers already running with `vncserver -list`

[usermeeting-vnc]: http://www.hpc.mcgill.ca/downloads/user_meetings/McGillHPC-UsersMeeting-VNC-X2Go-XQuartz-20170413.pdf
[cc-vnc]: https://docs.computecanada.ca/wiki/VNC

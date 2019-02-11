---
layout: default
title: Neuroimaging Softwares
parent: Working On The Project Space
nav_order: 1
---

# Access neuroimaging softwares

When you are logged into the lab cluster, you can use the `module` function to easily access softwares already installed.

How to use `module` : [Compute Canada documentation][modules-doc]

## Login node : guillimin-p3

**Note : matlab toolboxes are now loaded through `module`. You should rename `~/matlab/startup.m` to `~/matlab/startup.m.backup` to avoid compatibility issues.**

ssh address: `guillimin-p3.calculquebec.ca`

Each time you connect to the server, type these lines to load the `VilleneuveLab` module. This module contain a series of default softwares.

```
source /software/soft.computecanada.ca.sh
export VL_QUARANTINE_DIR="/sf1/project/yai-974-aa/quarantine"
module use ${VL_QUARANTINE_DIR}/modulefiles
module load VilleneuveLab
```

When beluga will be online (~January 2019), you'll need to remove the first line

### Optional

To automatically load the default softwares, it is possible to add the following lines at the end of your `~/.bashrc` file. This file is loaded each time you connect to guillimin.

```
if [ -z "$BASHRC_READ" ]; then
   export BASHRC_READ=1
   # Place the previous commands here
fi
```

**Due to an issue within `/software/soft.computecanada.ca.sh` this will break the loading if you use `tmux` or the VNC server. Just comment the line `export BASHRC_READ=1`. This will be fixed when beluga comes online**

## Visualization login node

ssh address : `guillimin1.calculquebec.ca`

From this node, you can launch the vncserver with `vl_vncserver`

```
$ vl_vncserver -h

Script to use on the visualization login node of the Villeneuve Lab
 -1- Launch this script from the visualization login node
 -2- Create the ssh tunnel from your local computer
 -3- Open RealVNC / TigerVNC from your local computer

Usage: vl_vncserver -t <time limit in hour(s)>
```

You should have a file `~/.vnc/xstartup` with this content :

```
#!/bin/sh
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
/usr/bin/mate-session &
```

You can check the vncserver already running with `vncserver -list`

## Old login node : guillimin

**This way to proceed is deprecated and will be deactivate when beluga comes online**

ssh address : `guillimin.calculquebec.ca`

Each time you connect to the server, type these lines:

```
module use /sf1/project/yai-974-aa/local/modulefiles
module load VilleneuveLab
```

[modules-doc]: https://docs.computecanada.ca/wiki/Utiliser_des_modules/en

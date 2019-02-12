---
layout: default
title: Neuroimaging Softwares
parent: Working On The Project Space
nav_order: 3
---

# Access neuroimaging softwares

When you are logged into the lab cluster, you can use the `module` function to easily access softwares already installed.

How to use `module` : [Compute Canada documentation][modules-doc]

## Loading the default modules

**Note : matlab toolboxes are now loaded through `module`. You should rename `~/matlab/startup.m` to `~/matlab/startup.m.backup` to avoid compatibility issues.**

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

## Loading the default modules the old way

**This way is deprecated and will be deactivate when beluga comes online**

Each time you connect to the server, type these lines:

```
module use /sf1/project/yai-974-aa/local/modulefiles
module load VilleneuveLab
```

[modules-doc]: https://docs.computecanada.ca/wiki/Utiliser_des_modules/en

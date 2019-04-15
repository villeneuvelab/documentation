---
layout: default
title: Neuroimaging Softwares
parent: Working On The Project Space
nav_order: 3
---

# Access neuroimaging softwares

When you are logged into the lab cluster, you can use the `module` function to easily access softwares already installed.

How to use `module` : [Compute Canada documentation][modules-doc]

# Loading the default modules on beluga

Each time you connect to the server, type these lines to load the `VilleneuveLab` module. This module contain a bundle of default softwares install in the quarantine

```
export VL_QUARANTINE_DIR="/project/ctb-villens/quarantine"
module use ${VL_QUARANTINE_DIR}/modulefiles
module load VilleneuveLab
```

# Loading the default modules on guillimin

Each time you connect to the server, type these lines to load the `VilleneuveLab` module. This module contain a bundle of default softwares.

```
source /software/soft.computecanada.ca.sh
export VL_QUARANTINE_DIR="/sf1/project/yai-974-aa/quarantine"
module use ${VL_QUARANTINE_DIR}/modulefiles
module load VilleneuveLab
```

## Optional

To automatically load the default softwares, it is possible to add the following lines at the end of your `~/.bashrc` file. This file is loaded each time you connect to guillimin.

```
if [ -z "$BASHRC_READ" ]; then
   export BASHRC_READ=1
   # Place the previous commands here
fi
```

For a better default to check your running jobs, you could add this alias at the end of your `~/.bashrc` file.

`alias showme='squeue -u $USER -o "%i %j %T %M %l %R %Z" | column -t'`

Note
{: .label .label-red }

**Due to an issue within `/software/soft.computecanada.ca.sh` this will break the loading if you use `tmux` or the VNC server. Just comment the line `export BASHRC_READ=1` if you are in this case. This will be fixed when beluga comes online**

# Python3 environment

A multi purpose python3 environment exists on the server for running scripts interactively. You can use it with `module load PythonenvVilleneuve`.

It should not be used to run within jobs. For that, create your own environment to control your modules version. See [Compute Canada documentation][python-doc] for more information.

# Loading the default modules the old way

Deprecated
{: .label .label-red }

**This way is deprecated and will be deactivate when beluga comes online**

Each time you connect to the server, type these lines:

```
module use /sf1/project/yai-974-aa/local/modulefiles
module load VilleneuveLab
```

[modules-doc]: https://docs.computecanada.ca/wiki/Utiliser_des_modules/en
[python-doc]: https://docs.computecanada.ca/wiki/Python

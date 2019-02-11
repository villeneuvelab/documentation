---
layout: default
title: Files Organization
parent: Working On The Project Space
nav_order: 2
---

## Main directories

- `dataset`: Sets of neuroimaging and/or behavioural data
- `quarantine`: Softwares directory
- `users`: Users directory
- `projects`: Shared directory for multi-users projects

## dataset

Each directory contains a dataset, read and write permissions are set for each folder.  See [projects section](#projects) for more information managing linux permissions.

General example of the dataset folder where `DIAN` folder is only accessible for specific users:

```
- dataset
  - DIAN 🔒
  - HCP
    - sourcedata
    - derivatives
      - freesurfer
      - niak
  - PreventAD
    - Young
      - sourcedata
      - derivatives
        - freesurfer
        - niak
    - Old_PAD
    - Old_HC
    - Old_MCI
```

#### Brain Imaging Data Struture

We try to follow the Brain Imaging Data Structure ([BIDS][bids-specs]: http://bids.neuroimaging.io/#download) in each folder. Please follow the link to learn more about this structure.

Quickly, here is an example of BIDS dataset:

```
- HCP
  - sourcedata        > DICOM files
  - sub-A00           > NIfTI and json files for A00 subject
  - sub-A01           > NIfTI and json files for A01 subject
  - sub-A02           > NIfTI and json files for A02 subject
  - derivatives       > derivatives data like `niak` pipeline
    - freesurfer
    - niak
  - participants.tsv  > participants informations
```

## quarantine

This directory contains softwares installed for the Villeneuve laboratory.

To automatically load the default softwares, see [Here](./Neuroimaging-softwares)

See `module avail` to print exhaustive list of softwares available on `guillimin`

Using the function module : [ComputeCanada documentation][CC-modules]

#### Matlab

Several versions of matlab & spm are installed. Please have a look with the commands `module avail <software_name>` or `module spider <software_name>`

## users

Each user gets his own directory to perform their research. Some space restriction will be set in the future internally at the lab.

You can check [disk space policy][mcgillHPC-disk-space]. For your home and scratch file directories, please use the command `myquota`.  For the Villeneuve Lab project directory, please use the command `prquota`.

**`myquota` and `prquota` are not available within `/software/soft.computecanada.ca.sh`. This will be fixed when beluga comes online**

#### Recommandations

- your directory should be your login on Compute Canada
- make sure your directory is under Villeneuve Lab group
  - `chgrp -R yai-974-01 <your-user-directory>`
- make sure each file and sub-directory will be create under this group
  - `chmod g+s <your-user-directory>`

## projects

When several users work on a project, You can created a directory for each project and manage permissions.

- To check the permissions of your directory
  - `ls -l` or `getfacl <your-project-directory>`
- Example of changing the access of your directory
  - remove read access from other: `chmod o-r <your-project-directory>`
  - add all access to group: `chmod g+rwx <your-project-directory>`
- It's possible to add access to a specific user only
  - `setfacl -m u:<user-login>:rwx <your-project-directory>`

[Tutorial on linux permissions](./Linux-permissions), here is a chart to remind you how linux permissions work.

![linux-permissions](/assets/images/mode.png)

#### Recommandations

- make sure your directory is under Villeneuve Lab group
  - `chgrp -R yai-974-01 <your-project-directory>`
- make sure each sub-directory will be created under this group
  - `chmod g+s <your-project-directory>`

[bids-specs]: http://bids.neuroimaging.io/#download
[CC-modules]: https://docs.computecanada.ca/wiki/Utiliser_des_modules/en
[mcgillHPC-disk-space]: http://www.hpc.mcgill.ca/index.php/starthere/81-doc-pages/87-disk-space


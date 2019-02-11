---
layout: default
title: Cluster Description
parent: VilleneuveLab Cluster
nav_order: 2
---

The cluster has seven Huawei nodes :

- one login node
- five worker nodes
- one visualization login node

You can access the login nodes with : `ssh <username>@<login node address>`

More information about access through ssh : [McGill HPC Documentation][mcgillHPC-access]

## Login node

The login node is accessible at : `guillimin-p3.calculquebec.ca`

## Worker nodes

Specification of the worker nodes :

| address | mem | core | mem/core |
| --- | --- | --- | --- |
| hw-3r03-n21 | 128G total | 32 cores | 4 GB/core |
| hw-3r03-n22 | 128G total | 32 cores | 4 GB/core |
| hw-3r03-n23 | 128G total | 32 cores | 4 GB/core |
| hw-3r03-n24 | 128G total | 32 cores | 4 GB/core |
| hw-3r03-n25 | 128G total | 32 cores | 4 GB/core |

## Visualization login node

The visualization login node is accessible at : `guillimin1.calculquebec.ca`


[mcgillHPC-access]: http://www.hpc.mcgill.ca/index.php/starthere/81-doc-pages/85-guillimin-access

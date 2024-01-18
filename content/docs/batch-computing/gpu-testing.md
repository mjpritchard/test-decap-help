---
aliases: /article/4951-gpu-testing
date: 2020-11-24 10:46:34
description: GPU testing
slug: gpu-testing
title: GPU testing
---

This article provides preliminary details on how to test a job on the LOTUS
GPU cluster.

{{<alert type="info">}}
Access to the GPU cluster is restricted to users who are
members of the **lotus_gpu** account. Please contact [JASMIN support
](mailto:support@jasmin.ac.uk) to request access to the account.
{{</alert>}}

## GPU cluster

The JASMIN GPU cluster is composed of 3 GPU hosts. Two hosts with two GPUs 2 x
GV100GL while one host has four GPUs 4 x GV100GL. GPU RAM is 32 GB  
  
The SLURM batch queue is `lotus_gpu` with Maximum runtime of 168 hours and the
default runtime is 1 hour

## How to test a GPU job

Testing a job on the JASMIN GPU cluster can be carried out in an interactive
mode by launching a pseudo-shell terminal SLURM job from JASMIN scientific
servers:

```
srun --gres=gpu:1 --partition=lotus_gpu --account=lotus_gpu --pty /bin/bash
cpu-bind=MASK - gpuhost592, task  0  0 [140444]: mask 0xfffffffff set 
[freddy@gpuhost592 ~]
```

The GPU host gpuhost592 is allocated for this interactive session on LOTUS

Note that for batch mode, a GPU job is submitted using the SLURM command
'sbatch':

```
sbatch --gres=gpu:1 --partition=lotus_gpu --account=lotus_gpu mygpujob.sbatch
```

or by adding the following SLURM directives to the preamble of the job script file:

```
#SBATCH --partition=lotus_gpu
#SBATCH --account=lotus_gpu
#SBATCH --gres=gpu:1
```


## Software Installed on the GPU cluster

  
DGX2/Pearl setup has been implemented on all 3 nodes. The hosts include:  
  
\- CUDA drivers 10.1, and CUDA libraries 10.0 and 10.1  
  
\- CUDA DNN (Deep Neural Network Library)  
  
\- NVIDIA container runtime (see notes below)  
  
\- NGC client (GPU software hub for NVIDIA)  
  
\- Singularity 3.4.1 - which supports NVIDIA/GPU containers

\- SCL Python 3.6



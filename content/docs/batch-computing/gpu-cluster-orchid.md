---
aliases: /article/5068-gpu-cluster-orchid
date: 2023-05-26 14:25:07
description: Orchid GPU cluster
slug: gpu-cluster-orchid
title: Orchid GPU cluster
type: docs
---

This article provides details on JASMIN's GPU
cluster, named **Orchid**.

## Request access to Orchid

Access to the GPU cluster is controlled by being a member of the Slurm account
`orchid`. You can request access to this via the link below which will
direct you to the ORCHID service page on the JASMIN accounts portal:

https://accounts.jasmin.ac.uk/services/additional_services/orchid/

**Note:** In the supporting info on the request form, please provide details
on the software and the workflow that you will use/run on the GPU cluster (or
the interactive GPU node)

## Test a GPU job

Testing a job on the JASMIN Orchid GPU cluster can be carried out in an
interactive mode by launching a pseudo-shell terminal SLURM job from a JASMIN
scientific server e.g. sci2:

{{<command user="user" host="sci2">}}
srun --gres=gpu:1 --partition=orchid --account=orchid --pty /bin/bash
(out)srun: job 24096593 queued and waiting for resources
(out)srun: job 24096593 has been allocated resources
{{</command>}}
{{<command user="user" host="gpuhost16">}}
## you are now on gpuhost16
{{</command>}}
    

The GPU node gpuhost016 is allocated for this interactive session on LOTUS

Note that for batch mode, a GPU job is submitted using the SLURM command
'sbatch':

{{<command user="user" host="sci2">}}
sbatch --gres=gpu:1 --partition=orchid --account=orchid gpujobscript.sbatch
{{</command>}}

or by adding the following preamble in the job script file
```bash
#SBATCH --partition=orchid
#SBATCH --account=orchid
#SBATCH --gres=gpu:1
```

Note 1: `gpuhost015 `and `gpuhost016`are the two largest nodes with 64 CPUs and
8 GPUs.

Note 2: **CUDA Version: 11.6**

Note 3: The SLURM batch queue 'orchid' has a maximum runtime of 24 hours and
the default runtime is 1 hour. The maximum number of CPU cores per user is
limited to 8 cores. If the limit is exceeded then the job is expected to be in
a pending state with the reason being **QOSGrpCpuLimit**

## GPU interactive node

There is also an interactive GPU node `gpuhost001.jc.rl.ac.uk` (same spec as
Orchid) that you can ssh into it from the JASMIN login server to prototype and
test your GPU code prior to using the batch GPU cluster Orchid

    
{{<command user="user" host="login1">}}    
ssh -A gpuhost001.jc.rl.ac.uk
{{</command>}}
{{<command user="user" host="gpuhost001">}}    
## you are now on gpuhost001
{{</command>}}

## Software Installed on the GPU cluster (to be updated)
  
- CUDA drivers 10.1, and CUDA libraries 10.0, 10.1 and 11.4  
- CUDA DNN (Deep Neural Network Library)  
- NVIDIA container runtime (see notes below)  
- NGC client (GPU software hub for NVIDIA)  
- Singularity 3.7.0 - which supports NVIDIA/GPU containers
- SCL Python 3.6

The SLURM queue is `orchid` with maximum runtime of 24 hours and
default runtime 1 hour.

## GPU cluster spec

The JASMIN GPU cluster is composed of 16 GPU nodes: 
- 14 x standard GPU nodes with 4 GPU Nvidia A100 GPU cards each
- 2 x large GPU nodes with 8 Nvidia A100 GPU cards

{{< image src="img/docs/gpu-cluster-orchid/file-NZmhCFPJx9.png" caption="ORCHID GPU cluster" >}}

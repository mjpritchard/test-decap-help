---
author: Alex Manning
title: Dask Gateway
tags:
- notebook
- lotus
---

## Introduction

[Dask Gateway](https://gateway.dask.org/) is a service which manages [dask](https://dask.org) clusters for users.
On JASMIN, it creates a dask cluster in {{<link "../batch-computing/lotus-overview.md">}}LOTUS{{</link>}}, our batch computing cluster. It automatically creates a dask for you, scheduling Slurm jobs to create dask schedulers and workers as appropriate.

Before using dask gateway on JASMIN, you first need to apply for the `dask` service on the JASMIN accounts portal.

{{<button href="https://accounts.jasmin.ac.uk/services/additional_services/dask/">}}Apply here{{</button>}}

## Creating a dask cluster

### In the JASMIN Notebooks service

In the {{<link "jasmin-notebooks-service">}}JASMIN notebooks service{{</link>}}, authentication to dask-gateway happends automatically. You can use the snippet below to create a cluster and get a dask client which you can use:

```python
import dask_gateway

# Create a connection to dask-gateway.
gw = dask_gateway.Gateway("https://dask-gateway.jasmin.ac.uk", auth="jupyterhub")

# Inspect and change the options if required before creating your cluster.
options = gw.cluster_options()
options.worker_cores = 2

# Create a dask cluster, or, if one already exists, connect to it.
# This stage creates the scheduler job in SLURM, so may take some time.
# While your job queues.
clusters = gw.list_clusters()
if not clusters:
    cluster = gw.new_cluster(options, shutdown_on_close=False)
else:
    cluster = gw.connect(clusters[0].name)

# Create at least one worker, and allow your cluster to scale to three.
cluster.adapt(minimum=1, maximum=3)

# Get a dask client.
client = cluster.get_client()

#########################
### DO DASK WORK HERE ###
#########################

# When you are done and whish to release your cluster:
cluster.shutdown()
```

### Elsewhere on JASMIN
(eg. on the `sci` machines)

{{<alert type="info">}}
It is not necessary to do this if you only want to use dask in the JASMIN notebook service.
{{</alert>}}

At the current time, it is still necessary to use the notebooks service to generate an API token to allow you to connect to the gateway server.

{{<alert type="danger">}}
It is very important that your API token is not shared between users and remains secret. With it, another user can submit dask jobs to lotus as you, and they could exploit this to see anything in your jasmin account.
{{</alert>}}

#### Setup

1. Make a dask configuration folder in your home directory

{{<command user="user" host="sci1">}}
mkdir -p ~/.config/dask
{{</command>}}

2. Create a configuration file for dask-gateway

{{<command user="user" host="sci1">}}
touch ~/.config/dask/gateway.yaml
{{</command>}}

3. Change the permissions on the file so that only you can read it

{{<command user="user" host="sci1">}}
chmod 600 ~/.config/dask/gateway.yaml
{{</command>}}

4. Head to https://notebooks.jasmin.ac.uk/hub/token , put a note in the box to remind yourself what this token is for, press the **big orange button** then {{<mark>}}copy{{</mark>}} then {{<mark>}}token{{</mark>}}.

5. Paste the following snippet into `~/.config/dask/gateway.yaml`, replace the part in brackets with the API token you just copied.

```yaml
gateway:
  address: https://dask-gateway.jasmin.ac.uk
  auth:
    type: jupyterhub
    kwargs:
      api_token: replaceWithYourSecretAPIToken
```

6. You're done. You can now use dask gateway from the command line.

## Access the dask dashboard

Currently the dask dashboard is not accessible from a browser outside the JASMIN firewall. If your browser fails to load the dashboard link returned, please use our {{<link "graphical-linux-desktop-access-using-nx">}}graphical desktop service{{</link>}} to run a Firefox browser inside the firewall to view your dashboard.

## Use a custom python environment

By default the jasmin notebooks service and dask gateway use the latest version of the `jaspy` software environment. However, often users would like to use their own software environments.

### Understanding the problem

When dask gateway greates a dask cluster for a user, it runs a setup command to activate a conda environment or python `venv`.
To have dask use your packages, you need to create a custom environment which you can pass to dask gateway to activate.

However, for techical reasons, it is not currently possible to use the same virtual environment in both the notebook service and on jasmin. So you will need to make two environments, one for your notebook to use and one for dask to use.

{{<alert type="info">}}
It is VERY important that these environments have the same packages installed in them, and that the packages are exactly the same version in both environments.

If you do not keep packages and versions in-sync you can expect many confusing errors.
{{</alert>}}

If you use a self-containted conda enironment this is not a problem, and you can use this as a kernel in the notebooks service and on the `sci` machines. You can skip to {{<link "#putting-it-all-together">}}Putting it all together{{</link>}} below.

### Creating a virtual environment for dask.

- Login to the JASMIN sci machines.
- Activate jaspy

{{<command>}}
module load jaspy
{{</command>}}

- Create your environment in the normal way

{{<command>}}
python -m venv name-of-environment
{{</command>}}

- Activate the environment

{{<command>}}
source name-of-environment/bin/activate
{{</command>}}

- Install dask and dask gateway and dependencies: without this step your environment will not work with dask.

{{<command>}}
pip install dask-gateway dask lz4
{{</command>}}

### Creating a virtual environment for the notebooks service

- Follow the instructions {{<link "creating-a-virtual-environment-in-the-notebooks-service">}}here{{</link>}} to create a virtual environment.
- Install dask and dask gateway and dependencies: without this step your environment will not work with dask.

{{<command>}}
pip install dask-gateway dask lz4
{{</command>}}

### Putting it all together

- Set your notebook virtual environment as the kernel for the notebook in question as shown in the instructions linked above.
- Set `options.worker_setup` to a command which will activate your dask virtual environment. For example

```bash
options.worker_setup = "source /home/users/example/name-of-environment/bin/activate"
```

- If you have an existing dask cluster, close it and ensure all lotus jobs are stopped before recreating it using the new environment.

## Code Examples

Examples of code and notebooks which can be used to test the JASMIN dask gateway service are [available on GitHub](https://github.com/cedadev/jasmin-daskgateway/tree/main/examples).

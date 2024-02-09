---
aliases: /article/4859-centos7-sci-login-xfer-servers
description: CentOS7 Login, Sci and Xfer servers
title: CentOS7 Login, Sci and Xfer servers
weight: 110
draft: true
---

{{<alert type="info">}}
This article was used to describe the new servers introduced as part of the RHEL -> CentOS7 migration in 2020/2021. It is now superceded.
{{</alert>}}

This article describes the CentOS7 versions of the 3 familiar
types of JASMIN server. These are:

- CentOS7 Login servers
- CentOS7 Scientific analysis (sci) servers
- CentOS7 Data transfer (xfer) servers 

## Login servers

The new CentOS7 login (bastion or gateway) servers are available to access
resources within JASMIN. Users with the `jasmin-login` access role
can access the following servers using SSH:

**Table 1** : Centos7 Login servers

Login server name  
|---|  
`login1.jasmin.ac.uk` |
`login2.jasmin.ac.uk` | 
`login3.jasmin.ac.uk` |  
`login4.jasmin.ac.uk` |  
  
See also NX login servers which are part of the [graphical linux desktop]({{<ref "graphical-linux-desktop-access-using-nx" >}}) service.

You should use these servers as your default route into JASMIN.
Additional servers in this series will follow in due course.  
These login servers provide a table displayed at login showing the
list of available sci servers and their current load and number of logged-in
users. Please make use of these to select the most appropriate sci server.

[Further details of the login servers]({{< ref "login-servers" >}})

## Scientific analysis servers

CentOS7 Scientific analysis servers are now available (see **Table 2** ).
These can be used by users with the `jasmin-login` access role to test
workflows/tasks that:

1. Use the [new software environments](https://drive.google.com/file/d/1gD9C0TZyNITibgDhlv3pRzgd4JjzVfBW/view)
2. Do not make use of the software `/apps/contrib` (which has only been tested for RHEL6 operating systems)
3. Do not make use of the software available under the `module` environment (which has only been tested for RHEL6 operating systems) except the modules `jaspy` and `jasmin-sci`
4. A job submitted to the new batch scheduler SLURM will run on a CentOS7 node in the LOTUS cluster.

**Table 2:** List of CentOS7 Scientific analysis servers

Server name  
--- |
`sci1.jasmin.ac.uk`  |
`sci2.jasmin.ac.uk`  |
`sci3.jasmin.ac.uk`  |
`sci4.jasmin.ac.uk`  |
`sci5.jasmin.ac.uk`  |
`sci6.jasmin.ac.uk`  |
`sci8.jasmin.ac.uk`  |
  
[Further details of the sci servers]({{< ref "sci-servers" >}}).

## Transfer servers

CentOS7 transfer (xfer) servers are now available (see Table 3). These can
be used by users with the `jasmin-login` access role and are functionally the
same as their predecessors.

**Table 3:** Centos7 xfer servers

Server name  | Details
---  | --- |
`xfer1.jasmin.ac.uk`  |
`xfer2.jasmin.ac.uk`  |
`xfer3.jasmin.ac.uk` | (special access rules similar to `login2`, but requires additional access role, apply [here](https://accounts.jasmin.ac.uk/services/additional_services/xfer-sp))  
`hpxfer[12].jasmin.ac.uk` | (physical, high-performance transfer servers,require `hpxfer` access role)  |
  
[Further details of the xfer servers]({{< ref "transfer-servers" >}})

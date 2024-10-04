---
aliases: /article/4414-data-transfer-hpxfer
description: 'Access to certain high-performance data transfer methods'
title: 'hpxfer access role'
---

{{<alert type="danger">}}
This article is deprecated, since the `hpxfer` is no longer needed for
the new Rocky 9 services introduced Autumn 2024.

However, until the older machines (`hpxfer[12]` & `gridftp1`) are taken out of service,
the role is still required for access to those.
{{</alert>}}

This article explains about access to high-performance data transfer services.

## Applying for access

Some data transfer services are hosted in the JASMIN Data Transfer Zone (a special area of JASMIN's network, located optimally for connections to the outside world via {{<link href="https://www.jisc.ac.uk/janet" cue="true">}}JANET{{</link>}}) for increased performance. However, to
maintain security in this zone, access to some services is controlled via an additional access
role `hpxfer`. If you have a login account already, you can apply here for
this additional role:

{{< button href="https://accounts.jasmin.ac.uk/account/login/?next=/services/additional_services/hpxfer/" >}}Apply for hpxfer{{< /button >}}

## Additional information required

If you will be connecting from your home institution directly via ssh or ssh-
based gridftp to one of the servers in the JASMIN Data Transfer Zone, the
specific IP address of your machine will need to be added to an allow-list.
Please supply this as part of the application process above.

However, this should not be necessary if you are accessing the server from a
remote server which is already allowed.

{{<alert type="info">}}If your **only** reason for applying for `hpxfer` is in order to use the **Globus** service on JASMIN, this is no longer required. You only need this role for accessing the hpxfer servers or for using certificate-based gridftp with the `globus-url-copy` command.
{{</alert>}}

**Inward** pulls of data (to JASMIN) are possible by logging in to
`hpxfer[1,2].jasmin.ac.uk` **via the login servers** and pulling data from
external data sources. So if you're not sure what IP address to use when
applying for access above, it is OK to quote the IP address of
`login1.jasmin.ac.uk`, i.e. `130.246.130.28` as a "dummy" value if you will
only be accessing them via this route, and not directly from outside.

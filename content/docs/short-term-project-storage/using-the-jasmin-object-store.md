---
aliases: /article/4847-using-the-jasmin-object-store
date: 2021-12-07 09:42:33
description: Using the JASMIN Object Store
slug: using-the-jasmin-object-store
title: Using the JASMIN Object Store
---

This article describes how to use the JASMIN high-performance object storage.

## What is object storage?

An [object store](https://en.wikipedia.org/wiki/Object_storage) is a data
storage system that manages data as objects referenced by a globally unique
identifier, with attached metadata. This is a fundamental change from
traditional file systems that you may be used to, as there is no directory
hierarchy - the objects exist in a single flat domain. These semantics allow
the object store to scale out much more easily than a traditional shared file
system.

The other fundamental change is that the data is no longer accessed by
mounting a file system onto a host and referencing a file path (where
authentication is "can I log in to the host"). Instead, the data is accessed
over HTTP, with authentication using HTTP headers. This has many benefits, the
biggest of which is that we can make the object store available outside of the
JASMIN firewall, for example to the JASMIN External Cloud. Data can be read
**and written** in the same way, using the same tools, from inside and outside
JASMIN. Contrast this with Group Workspaces, where you must be logged in to a
JASMIN host in order to write data using the file system, and data is only
accessible externally in a readonly way using HTTP or OPeNDAP.

Object stores are seen as the most efficient (and cheapest!) way to store and
access data from the cloud, and all the major cloud providers support some
variant of object store. The JASMIN object store is [S3
compatible](https://www.scality.com/topics/what-is-s3-compatible-storage/) \-
S3 is the object store for Amazon Web Services (AWS), and has become a de-
facto standard interface for object stores. This means that all the same tools
that work with AWS S3 will also work with the JASMIN object store.

## Accessing the object store

The JASMIN object store is organised into **tenancies**. These are shared
areas of the object store, similar in concept to Group Workspaces, and are
requested by users, usually Group Workspace Managers. Several users can have
access to a tenancy, and so they can be used collaboratively.

To join an existing object store tenancy, navigate to the "Services" section
in the JASMIN Accounts Portal and select the "Object store" category. Select a
tenancy and submit a request to join. This request will then be considered by
the manager of the tenancy and either accepted or rejected.

{{<image src="img/docs/using-the-jasmin-object-store/file-kHfcUlqbAf.png" caption="">}}

For details on how to request and manage an object
store tenancy, please see the help article "JASMIN Object Store for Managers"
(forthcoming).

## Creating an access key and secret

Authentication with the object store uses an access key and secret that are
separate to your JASMIN username and password. You can generate an access key
and secret using the Caringo portal. This portal is not currently available
outside of JASMIN - you will need to use a graphical session on JASMIN to
access a Firefox browser running on a JASMIN system.

**The recommended way to do this is using the** [NX Graphical Desktop
service]({{< ref "graphical-linux-desktop-access-using-nx" >}}). You can start Firefox from
the "Activities" menu once you have logged in to your graphical desktop on one
of the `nx-login*` servers (so no need to make an onward connection to a `sci`
server).

An alternative option is to using X11 Forwarding on your SSH connection:

    
```bash
ssh -AY <user>@sciX.jasmin.ac.uk firefox
```    

Once you have Firefox open, navigate to

```bash
http://my-os-tenancy-o.s3.jc.rl.ac.uk:81/_admin/portal
```

but replace `my-os-tenancy-o` with your tenancy name.

You will see a login screen where you
should enter your JASMIN username and password:

{{<image src="img/docs/using-the-jasmin-object-store/file-4dszwvVbge.png" caption="">}}

If you receive a "HTTP ERROR 500 java..." error, it is likely that you haven't
added the port (81) to the address.  
  
Upon successfully entering the username and password of a user who belongs to
the tenancy, you will see a dashboard. To create an access key and secret,
click on the cog icon and select "Tokens":

{{<image src="img/docs/using-the-jasmin-object-store/file-sazR2YE8xn.png" caption="">}}

On the tokens page, click "Add":

{{<image src="img/docs/using-the-jasmin-object-store/file-tiUnM6oyq6.png" caption="">}}

In the dialogue that pops up, enter a description for the token and set an
expiration date. Make sure to click "S3 Secret Key" - this will expose an
additional field containing the secret key. **Make sure you copy this and
store it somewhere safe - you will not be able to see it again!** This value
will be used whenever the "S3 secret key" is required.

{{<image src="img/docs/using-the-jasmin-object-store/file-8ezAbSQY56.png" caption="">}}

Once the token is created, it will appear in the list. The "Token" should be
used whenever the "S3 access key" is required:

{{<image src="img/docs/using-the-jasmin-object-store/file-QSg6RtIAv8.png" caption="">}}

# Accessing data in the object store

## URLs for internal and external access

Although the data is exactly the same in both cases, a slightly different URL
must be used depending on whether you are accessing the object store from the
JASMIN managed cloud servers or from the JASMIN External Cloud.

From inside JASMIN, including LOTUS and the Scientific Analysis servers, 
`my-os-tenancy-o.s3.jc.rl.ac.uk` should be used, with the `http://`` prefix.

From the JASMIN External Cloud, and from locations external to JASMIN, `my-os-tenancy-o.s3-ext.jc.rl.ac.uk` should be
used - note the `https://` prefix and additional `-ext`.

(Where `my-os-tenancy-o` needs to be replaced with your tenancy name)

## Using s3cmd

`s3cmd` is a command line tool provided by Amazon to work with S3 compatible
Object Storage. It is installed on JASMIN, both on the sci-machines and on
LOTUS. It is a little more complicated to use than the MinIO client, but is
more powerful and flexible. For full details on `s3cmd`, see the [s3tools.org
website](http://s3tools.org).

To configure `s3cmd` to use the JASMIN object store, you need to create and
edit a `~/.s3cfg` file. To access the `my-os-tenancy-o` tenancy (where "my-os-
tenancy-o" needs to be replaced with your tenancy name), the following should
be in the `~/.s3cfg `file:

```
access_key = <access key generated above>
host_base = my-os-tenancy-o.s3.jc.rl.ac.uk
host_bucket = my-os-tenancy-o.s3.jc.rl.ac.uk
secret_key = <secret key generated above>
use_https = False
signature_v2 = False
``` 

or, from an external tenancy or locations outside of JASMIN:

```
access_key = <access key generated above>
host_base = my-os-tenancy-o.s3-ext.jc.rl.ac.uk
host_bucket = my-os-tenancy-o.s3-ext.jc.rl.ac.uk
secret_key = <secret key generated above>
use_https = True
signature_v2 = False
``` 

To see which commands can be used with s3cmd, type:

```bash
s3cmd -h
```

To list a tenancy's buckets:

```bash
s3cmd ls
```    

To list the contents of a bucket:

```bash
s3cmd ls s3://<bucket_name>
```    

Make a new bucket:

```bash
s3cmd mb s3://<bucket_name>
```

`s3cmd` uses PUT and GET nomenclature for copying files to and from the object
store.  
To copy a file to a bucket in the object store:

```bash
s3cmd put <file name> s3://<bucket_name>
```

To copy a file from a bucket in the object store to the file system:

```bash
s3cmd get s3://<bucket_name>/<object_name> <file_name>
```

For more commands and ways of using `s3cmd`, see the [s3tools
website](https://s3tools.org/s3cmd).

## Using the MinIO client

The MinIO Client is a command line tool to connect to object stores (among
other types of file storage) and interface with it as you would with a UNIX
filesystem. As such, many of the UNIX file management commands found in
standard installations of the OS are found within this client ( `ls`, `cat`,
`cp`, `rm` for example).

There are a number of ways to install this client as shown in the [quickstart
guide](https://docs.min.io/docs/minio-client-quickstart-guide.html). Methods
include: docker, Homebrew for macOS, wget for Linux and instructions for
Windows. Follow these steps to get the client installed on the relevant
system.

MinIO Client is not installed on JASMIN, but users can download and install it
to their own user space, following the instructions for "64-bit Intel" (linux-
amd64) in the MinIO quickstart guide. Below is an example to install it into
the `bin` directory in your user space

```bash
mkdir ~/bin
wget https://dl.min.io/client/mc/release/linux-amd64/mc ~/bin
chmod u+x ~/bin/mc
```

You can then add the `~/bin` directory to the PATH environment variable in
your `~/.bashrc` file to allow `mc` to be accessed from anywhere on JASMIN.

```bash
# User specific aliases and functions
PATH=$PATH:$HOME/bin
```

To configure the client with the JASMIN object store, create an access key and
secret as documented above and insert them into the command:

```bash
mc config host add [ALIAS] [S3-ENDPOINT] [TOKEN] [S3 SECRET KEY]
```

The ALIAS is the name you'll reference the object store when using the client.
To demonstrate, if the alias was set to "jasmin-store", displaying a specific
bucket in the object store would be done in the following way:

```bash
mc ls jasmin-store/my-bucket
```

The commands available in the client are documented in the quickstart guide
(linked above). Copying an object from one place to another is very similar to
a UNIX filesystem:

```bash
mc cp jasmin-store/my-bucket/object-1 jasmin-store/different-bucket/
```

## From Python

One method of accessing the object store from Python is using
[s3fs](https://s3fs.readthedocs.io/en/latest/index.html). This library builds
on
[botocore](https://botocore.amazonaws.com/v1/documentation/api/latest/index.html)
but abstracts a lot of the complexities away. There are three main types of
object in this library:
[S3FileSystem](https://s3fs.readthedocs.io/en/latest/api.html#s3fs.core.S3FileSystem),
[S3File](https://s3fs.readthedocs.io/en/latest/api.html#s3fs.core.S3File) and
[S3Map](https://s3fs.readthedocs.io/en/latest/api.html#s3fs.mapping.S3Map).
The filesystem object is used to configure a connection to the object store.
Note: it's **strongly** recommended to store the endpoint, token and secret
outside of the Python file, either using environment variables or an external
file. This object can be used for lots of the operations which can be done
MinIO:

    
```python
with open('jasmin_object_store_credentials.json') as f:
    jasmin_store_credentials = json.load(f)

    jasmin_s3 = s3fs.S3FileSystem(
        anon=False, secret=jasmin_store_credentials['secret'],
        key=jasmin_store_credentials['token'],
        client_kwargs={'endpoint_url': jasmin_store_credentials['endpoint_url']}
    )

    my_object_size = jasmin_s3.du('my-bucket/object-1')
```

Please note in the example above, the `jasmin_object_store_credentials.json`
file would look along the lines of:

    
```json
{
    "token": "<access key generated above>",
    "secret": "<secret key generated above>",
    "endpoint_url": "http://my-os-tenancy-o.s3.jc.rl.ac.uk"
}
```

or, from an external tenancy or locations outside of JASMIN:

```json
{
    "token": "<access key generated above>",
    "secret": "<secret key generated above>",
    "endpoint_url": "https://my-os-tenancy-o.s3-ext.jc.rl.ac.uk"
}
```

S3File is used for dealing with individual files on the object store within
Python. These objects can read and written to and from the store:

```python
file_object = s3fs.S3File(jasmin_s3, 'my-bucket/object-1', mode='rb')
# refresh can be set to True to disable metadata caching
file_metadata = file_object.metadata(refresh=False)

# Writing data to variable in Python
file_object.write(data)
# Data will only be written to the object store if flush() is used. This can be executed in S3FS source code if the buffer >= the blocksize
file_object.flush()
```

S3Map is very useful when using [xarray](http://xarray.pydata.org/en/stable/)
to open a number of data files (netCDF4 for example), and turn them into the
zarr format ready to be stored as objects on the store. The function for this
can store a `.zarr` file in a POSIX filesystem, or can be streamed directly to
an object store. These datasets can then be opened back into Python:

    
```python
xarray.open_mfdataset(filepath_list, engine=netcdf4)
s3_store = s3fs.S3Map('my-bucket/zarr-data', s3=jasmin_s3)
dataset.to_zarr(store=s3_store, mode='w')

# Reopening the dataset from object store using xarray
xarray.open_zarr(s3_store, consolidated=True)
```



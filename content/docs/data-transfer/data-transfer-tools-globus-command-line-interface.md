---
aliases: /article/4480-data-transfer-tools-globus-command-line-interface
categories:
- Data Transfer
collection: jasmin-documentation
date: 2022-02-16 10:03:32
description: 'Data Transfer Tools: Using the Globus Command-Line Interface'
slug: data-transfer-tools-globus-command-line-interface
title: 'Data Transfer Tools: Using the Globus Command-Line Interface'
---

This article describes

- how to transfer data using the Globus Command Line Interface. It covers:
  - how an end-user can set up their host (laptop, desktop or home directory on their departmental server) with the Globus Command-Line Interface (CLI)
  - examples of common tasks using the CLI

It is not necessary to use the Globus CLI on a JASMIN server: it is a tool
that you can use anywhere (for example your own desktop/laptop) to interact
with the Globus service, to orchestrate a transfer between 2 endpoints. The
CLI is not centrally installed on JASMIN, and does not need to be in the same
place as either of the 2 endpoints involved in the transfer. The fact that one
of those endpoints is the JASMIN Globus Endpoint does not mean that you need
to be on JASMIN to orchestrate the transfer: you could use the CLI on your own
laptop/desktop, even if the 2 endpoints were 2 institutional Globus endpoints
on opposite sides of the world. You could of course decide to install the CLI
in your home directory on JASMIN if that were useful as part of your
processing/data transfer workflow.

The [Globus CLI is fully documented here](https://docs.globus.org/cli/) with
[examples](https://docs.globus.org/cli/examples/). It provides a command-line
interface for managed transfers via the Globus cloud-based transfer service,
which usually achieves the best possible transfer rate over a given route
compared to other methods. Typically this will be significantly faster than
can be achieved over scp, rsync or sftp transfers, particularly if the
physical network path is long.

The Globus CLI is designed for use either interactively within an interactive
shell or in scripts. An alternative [Python software development kit
(SDK)](https://globus-sdk-python.readthedocs.io/en/stable/) is also available
and should be considered for more sophisticated workflows.

Alternatively, the Globus web interface at <https://app.globus.org> can be
used as an easy-to-use interface to orchestrate transfers interactively.

Whichever method is used: CLI, SDK or web interface, transfers are invoked as
asynchronous, managed tasks which can then be monitored, and if need be set to
retry automatically until some pre-set deadline.

## Prerequisites

- Linux environment with normal user privileges, **or**
- Mac environment with ability to install applications, **or**
- Windows environment with ability to install applications
- Python environment for that platform, with ability to create virtual environments (to enable installation of additional packages)
- For use of the JASMIN Globus endpoint: 
  - An active JASMIN user account, with “jasmin-login” role. and “hpxfer” privileges.
- You may also wish to [set up your own Globus endpoint using Globus Connect Personal]({{< ref "data-transfer-tools-globus-connect-personal" >}}), though this is not needed for these examples.

## Initial Setup

### Get a Globus ID

Go to<https://www.globusid.org/login> or see <https://docs.globus.org/how-
to/get-started/>

### Set up the Globus CLI on your machine

Make a Python virtual environment and activate it:

    
    
    $ python3 -m venv ./venv
    $ source ./venv/bin/activate
    

Download the Globus CLI and install it into the virtual environment ( `venv`).

    
    
    $ pip install globus-cli
    

Try the `globus login` command. The first time you run this, you will be
prompted to authorise the Globus CLI to carry out operations on behalf of your
Globus ID. The URL will open in your default browser, where you should
authenticate with your Globus ID credentials. If you prefer, you can
copy/paste the URL from the command-line to a browser of your choice. Either
way, you then need to click "Allow" in the browser window, then copy/paste the
resulting "Native App Authorization Code" back to the terminal window where
you issued the `globus login` command:

    
    
    $ globus login --no-local-server
    Please authenticate with Globus here:
    ------------------------------------
    https://auth.globus.org/v2/oauth2/authorize?client_id=abc1234-9c3c-4ad42-be31-8d6c87101239014&redirect_uri=https%3A%2F%2Fauth.globus.org%2Fv2%2Fweb%2Fauth-code&scope=openid+profile+email+urn%3Aglobus%3Aauth%3Ascope%3Aauth.globus.org%3Aview_identity_set+urn%3Aglobus%3Aauth%3Ascope%3Atransfer.api.globus.org%3Aall+urn%3Aglobus%3Aauth%3Ascope%3Agroups.api.globus.org%3Aall+urn%3Aglobus%3Aauth%3Ascope%3Asearch.api.globus.org%3Aall&state=_default&response_type=code&access_type=offline&prompt=login
    ------------------------------------
    
    Enter the resulting Authorization Code here:
    

You should then see the following:

    
    
    You have successfully logged in to the Globus CLI!
    
    You can check your primary identity with
      globus whoami
    
    For information on which of your identities are in session use
      globus session show
    
    Logout of the Globus CLI with
      globus logout
    

You can now use the Globus CLI commands as listed by the following command:

    
    
    $ globus  --help
    Usage: globus [OPTIONS] COMMAND [ARGS]...
    
      Interact with Globus from the command line
    
      All `globus` subcommands support `--help` documentation.
    
      Use `globus login` to get started!
    
      The documentation is also online at https://docs.globus.org/cli/
    
    Options:
      -v, --verbose                  Control level of output
      -h, --help                     Show this message and exit.
      -F, --format [unix|json|text]  Output format for stdout. Defaults to text
      --jmespath, --jq TEXT          A JMESPath expression to apply to json
                                     output. Takes precedence over any specified '
                                     --format' and forces the format to be json
                                     processed by this expression
      --map-http-status TEXT         Map HTTP statuses to any of these exit codes:
                                     0,1,50-99. e.g. "404=50,403=51"
    
    Commands:
      bookmark        Manage endpoint bookmarks
      collection      Manage your Collections
      delete          Submit a delete task (asynchronous)
      endpoint        Manage Globus endpoint definitions
      get-identities  Lookup Globus Auth Identities
      group           Manage Globus Groups
      list-commands   List all CLI Commands
      login           Log into Globus to get credentials for the Globus CLI
      logout          Logout of the Globus CLI
      ls              List endpoint directory contents
      mkdir           Create a directory on an endpoint
      rename          Rename a file or directory on an endpoint
      rm              Delete a single path; wait for it to complete
      search          Use Globus Search to store and query for data
      session         Manage your CLI auth session
      task            Manage asynchronous tasks
      transfer        Submit a transfer task (asynchronous)
      update          Update the Globus CLI to its  latest version
      version         Show the version and exit
      whoami          Show the currently logged-in identity

## Examples

  1. **Find an endpoint**

We will use the `globus endpoint search` subcommand. Find help on the
particular options for that with

    
    
    $ globus endpoint search --help
    Usage: globus endpoint search [OPTIONS] [FILTER_FULLTEXT]
    
      Search for Globus endpoints with search filters. If --filter-scope is set to
      the default of 'all', then FILTER_FULLTEXT is required.
    
      If FILTER_FULLTEXT is given, endpoints which have attributes (display name,
      legacy name, description, organization, department, keywords) that match the
      search text will be returned. The result size limit is 100 endpoints.
    
    Options:
      --filter-scope [all|administered-by-me|my-endpoints|my-gcp-endpoints|recently-used|in-use|shared-by-me|shared-with-me]
                                      The set of endpoints to search over.
                                      [default: all]
      --filter-owner-id TEXT          Filter search results to endpoints owned by
                                      a specific identity. Can be the Identity ID,
                                      or the Identity Username, as in
                                      "go@globusid.org"
      --limit INTEGER RANGE           The maximum number of results to return.
                                      [default: 25; 1<=x<=1000]
      -v, --verbose                   Control level of output
      -h, --help                      Show this message and exit.
      -F, --format [unix|json|text]   Output format for stdout. Defaults to text
      --jmespath, --jq TEXT           A JMESPath expression to apply to json
                                      output. Takes precedence over any specified
                                      '--format' and forces the format to be json
                                      processed by this expression
      --map-http-status TEXT          Map HTTP statuses to any of these exit
                                      codes: 0,1,50-99. e.g. "404=50,403=51"
    

Search for the endpoints matching the search term "tutorial" and owned by the
Globus ID "go@globusid.org":

    
    
    $ globus endpoint search "tutorial" --filter-owner-id go@globusid.org
    ID                                   | Owner           | Display Name              
    ------------------------------------ | --------------- | --------------------------
    ddb59aef-6d04-11e5-ba46-22000b92c6ec | go@globusid.org | Globus Tutorial Endpoint 1
    ddb59af0-6d04-11e5-ba46-22000b92c6ec | go@globusid.org | Globus Tutorial Endpoint 2
    

(The 2 globus tutorial endpoints actually "see" the same filesystem, so we'll
just use the first one)

For convenience, let's set environment variables representing the ID of this
endpoint:

    
    
    $ export ep1=ddb59aef-6d04-11e5-ba46-22000b92c6ec
    
    $ echo $ep1
    ddb59aef-6d04-11e5-ba46-22000b92c6ec
    

We'll also find another endpoint, this time a public test endpoint which can
be used for performance testing:

    
    
    $ globus endpoint search "star dtn"
    ID                                   | Owner              | Display Name                         
    ------------------------------------ | ------------------ | -------------------------------------
    57218f41-3200-11e8-b907-0ac6873fc732 | esnet@globusid.org | ESnet Read-Only Test DTN at Starlight
    

Set `stardtn` to the ID of this endpoint:

    
    
    $ export stardtn=57218f41-3200-11e8-b907-0ac6873fc732
    

> **NOTE: None of the endpoints mentioned so far require authentication in
> order to use them. This makes demonstrating basic functionality simpler, but
> we'll look at how to activate an endpoint which requires authentication,
> later.**

  2. **Listing files at a path on an endpoint**

Use the `endpoint ls` command to list the contents of the `stardtn` endpoint,
at the path `/data1`

    
    
    <code><div>$ globus ls $stardtn:/data1
    500GB-in-large-files/
    50GB-in-medium-files/
    5GB-in-small-files/
    5MB-in-tiny-files/
    Climate-Huge/
    Climate-Large/
    Climate-Medium/
    Climate-Small/
    bebop/
    logs/
    write-testing/
    100G.dat
    100M.dat
    10G.dat
    10M.dat
    1G.dat
    1M.dat
    500G.dat
    50G.dat
    50M.dat
    

These are files and directories containing dummy data which can be used for
test purposes.

  3. **Copy a file from one endpoint to another**

Let's transfer the file `1M.dat` from the `stardtn` endpoint to `ep1`:

    
    
    $ globus transfer $stardtn:/data1/1M.dat $ep1:/~/1M.dat
    Message: The transfer has been accepted and a task has been created and queued for execution
    Task ID: dfb36cd8-7d39-11ec-891f-939ceb6dfaf1
    

The transfer task is a separate activity and does not require any connection
from the CLI client to either of the 2 endpoints: the Globus transfer service
manages the transfer for us. We can check on the progress of this transfer
task with:

    
    
    $ globus task show dfb36cd8-7d39-11ec-891f-939ceb6dfaf1
    Label:                        None
    Task ID:                      dfb36cd8-7d39-11ec-891f-939ceb6dfaf1
    Is Paused:                    False
    Type:                         TRANSFER
    Directories:                  0
    Files:                        1
    Status:                       SUCCEEDED
    Request Time:                 2022-01-24T17:20:07+00:00
    Faults:                       0
    Total Subtasks:               2
    Subtasks Succeeded:           2
    Subtasks Pending:             0
    Subtasks Retrying:            0
    Subtasks Failed:              0
    Subtasks Canceled:            0
    Subtasks Expired:             0
    Subtasks with Skipped Errors: 0
    Completion Time:              2022-01-24T17:20:08+00:00
    Source Endpoint:              ESnet Read-Only Test DTN at Starlight
    Source Endpoint ID:           57218f41-3200-11e8-b907-0ac6873fc732
    Destination Endpoint:         Globus Tutorial Endpoint 1
    Destination Endpoint ID:      ddb59aef-6d04-11e5-ba46-22000b92c6ec
    Bytes Transferred:            1000000
    Bytes Per Second:             587058
    

We can also list the destination endpoint to check that the file has reached
its destination:

    
    
    $ globus ls $ep1:/~/
    1M.dat
    

We can also make a subdirectory with `mkdir`:

    
    
    $ globus mkdir $ep1:/~/mydata/
    The directory was created successfully
    

We can move our `1M.dat` into that directory with a `globus rename` command

    
    
    $ globus rename $ep1 /~/1M.dat /~/mydata/1M.dat
    File or directory renamed successfully
    

We now have a directory `mydata` containing files `1M.dat`:

    
    
    $ globus ls $ep1:/~/mydata/
    1M.dat
    

  4. **Recursively copy a directory and its contents, from one endpoint to another**

Let's copy a directory on the `stardtn` endpoint which contains some small
files, to our destination endpoint `ep1` (The Globus tutorial endpoints only
provide very limited storage space).

The files we want to copy are at the path `/data1/5MB-in-tiny-files/a/a/` on
the `stardtn` endpoint, and are small, as their names suggest:

    
    
    $ globus ls $stardtn:/data1/5MB-in-tiny-files/a/a/
    a-a-1KB.dat
    a-a-2KB.dat
    a-a-5KB.dat
    

Copy the parent directory recursively to `ep1`:

    
    
    $ globus transfer -r $stardtn:/data1/5MB-in-tiny-files/a/a $ep1:/~/star-data
    Message: The transfer has been accepted and a task has been created and queued for execution
    Task ID: 4ae9bab0-7d40-11ec-bef3-a18800fa5978
    

Check destination content:

    
    
    $ globus ls $ep1
    mydata1/
    star-data/
    
    $ globus ls $ep1:/~/star-data
    a-a-1KB.dat
    a-a-2KB.dat
    a-a-5KB.dat
    

We could now delete one of the small files using the `globus delete` command:

    
    
    $ globus delete $ep1:/~/star-data/a-a-2KB.dat
    Message: The delete has been accepted and a task has been created and queued for execution
    Task ID: be4d6934-7d40-11ec-891f-939ceb6dfaf1
    

And list contents again, to verify that it has been deleted:

    
    
    $ globus ls $ep1:/~/star-data
    a-a-1KB.dat
    a-a-5KB.dat
    

  5. **Sync a source directory to a target (repeatable)**

We could now repeat the copying of the source data, but this time using the
`-s` or `--sync-level exists` command so that we only copy the data that is
now missing from the destination. The full set of sync options is
`[exists|size|mtime|checksum]`.

    
    
    $ globus transfer -s exists -r $stardtn:/data1/5MB-in-tiny-files/a/a $ep1:/~/star-data
    Message: The transfer has been accepted and a task has been created and queued for execution
    Task ID: 759a3cac-7d41-11ec-bef3-a18800fa5978
    

This should only copy the data that do not already exist at the desination: We
end up with the same set of files at the destination:

    
    
    $ globus ls $ep1:/~/star-data
    a-a-1KB.dat
    a-a-2KB.dat
    a-a-5KB.dat
    

But we can see that only 2000 bytes were transferred (so we know it only
copied that one file, which is what we wanted):

    
    
    $ globus task show 759a3cac-7d41-11ec-bef3-a18800fa5978
    Label:                        None
    Task ID:                      759a3cac-7d41-11ec-bef3-a18800fa5978
    Is Paused:                    False
    Type:                         TRANSFER
    Directories:                  1
    Files:                        3
    Status:                       SUCCEEDED
    Request Time:                 2022-01-24T18:14:24+00:00
    Faults:                       0
    Total Subtasks:               5
    Subtasks Succeeded:           5
    Subtasks Pending:             0
    Subtasks Retrying:            0
    Subtasks Failed:              0
    Subtasks Canceled:            0
    Subtasks Expired:             0
    Subtasks with Skipped Errors: 0
    Completion Time:              2022-01-24T18:14:58+00:00
    Source Endpoint:              ESnet Read-Only Test DTN at Starlight
    Source Endpoint ID:           57218f41-3200-11e8-b907-0ac6873fc732
    Destination Endpoint:         Globus Tutorial Endpoint 1
    Destination Endpoint ID:      ddb59aef-6d04-11e5-ba46-22000b92c6ec
    Bytes Transferred:            2000
    Bytes Per Second:             60
    

This task could be repeated in a shell script, cron job or even using the
Globus timer functionality, for either a source or destination directory that
is expected to change.

  6. **Activate an endpoint that requires authentication**

Most Globus Connect Server endpoints require activation, which usually
involves both authentication (checking identity) and authorization (checking
that you have the correct permission to carry out a particular activity).

Let's find, then set up an alias to the JASMIN Globus Endpoint. It is owned by
the globus ID `ceda@globusid.org`

    
    
    $ globus endpoint search "jasmin" --filter-owner-id ceda@globusid.org
    ID                                   | Owner             | Display Name                               
    ------------------------------------ | ----------------- | -------------------------------------------
    2b0a1a4c-ee1f-11eb-b467-eb47ba14b5cc | ceda@globusid.org | JASMIN Globus Endpoint (jasmin credentials)
    
    
    export epj=2b0a1a4c-ee1f-11eb-b467-eb47ba14b5cc
    

Let's activate this endpoint, opting to use the MyProxy method, for which we
need our JASMIN account credentials. Include  and you will be prompted for
your account password:

    
    
    $ globus endpoint activate --myproxy --myproxy-username <username> $epj
    Myproxy password: 
    Endpoint activated successfully using a credential fetched from a MyProxy server.
    

Note (1) You can also specify the password in the command using the -P option,
to do this in one action, but this is less secure as your password will be
visible in your system’ command history

If successful, you can now interact with the JASMIN endpoint, for example
listing your home directory:

    
    
    $ globus ls $epj:/~/
    ...
    (file listing)
    ...
    

  7. **Re-activate an endpoint**

You can check if an endpoint is activated like this:

    
    
    $ globus endpoint is-activated $epj
    2b0a1a4c-ee1f-11eb-b467-eb47ba14b5cc is activated
    

This can be used in conjunction with the previous command to re-activate if
necessary. Activation normally lasts 72 hrs (although this may increase in
future, for the JASMIN endpoint).

An alternative method for activating an endpoint is also available using the
--delegate-proxy method, specifying the path to an x509 credential certificate
obtained using the JASMIN SLCS service, as described in this article. In this
case, the activation command would be

    
    
    $ globus endpoint activate --delegate-proxy <credential file> $epj
    Endpoint activated successfully using a proxy credential provided by the client.
    

Activation can therefore be carried out independently of any transfers (via
the CLI or web interface, or by storing a secure but time-limited credential
on the file system), so transfers need not be interrupted. **Do not store your
username or password in the file system to facilitate renewal of your
credential, however: this is insecure.** The lifetime of the credential
(currently 72 hrs but we are working on extending this) should be sufficient
that obtaining the credential for activation of the endpoint can be a "one-
off" manual task which is carried out before any transfer takes place: it does
not need to be part of the transfer workflow itself.

* * *

### Automation

The functionality above can be combined into useful scripts which can perform
useful, repeatable tasks such as:

  * recursively syncing the contents of directories between 2 endpoints

Globus provide 2 implementations of this here:

[Examples of automation using the Globus
CLI](https://github.com/globus/automation-examples), specifically:

  * [cli-sync.sh](https://github.com/globus/automation-examples/blob/master/cli-sync.sh) : bash script using the Globus CLI as demonstrated above
  * [globus_folder_sync.py](https://github.com/globus/automation-examples/blob/master/globus_folder_sync.py) : Python code using the Globus Python software development kit (SDK) 
    * We have not covered the Python SDK here, but this is a useful example of how you could integrate Globus transfer functionality into your own workflows. You would need to install and authorise this first)

Taking the first of these examples, we can adapt it slightly:

1\. Select the JASMIN endpoint at the destination, and set the destination
path. Modify the corresponding variables in the script to these values:

    
    
    DESTINATION_ENDPOINT='2b0a1a4c-ee1f-11eb-b467-eb47ba14b5cc'
    
    
    
    DESTINATION_PATH='/home/users/<username>/sync-demo/'
    

2\. If you haven't already, activate the Python virtual environment where you
have the CLI installed, and login:

    
    
    $ source ~/.globus-cli-venv/bin/activate
    
    
    
    $ globus login
    

3\. Activate the JASMIN endpoint (use one of the methods described in the
article above, for example `--myproxy`

    
    
    $ globus endpoint activate --myproxy --myproxy-username=<username>
    

4\. Run the script to sync the data from the Globus Tutorial Endpoint to the
destination directory

    
    
    $ ./cli-sync.sh
    

You should see output like this, including the unique task ID

    
    
    $ ./cli-sync.sh 
    Checking for a previous transfer
    Last transfer f5db7238-8f06-11ec-8fe0-dfc5b31adbac SUCCEEDED, continuing
    Verified that source is a directory
    Submitted sync from ddb59aef-6d04-11e5-ba46-22000b92c6ec:/share/godata/ to ddb59af0-6d04-11e5-ba46-22000b92c6ec:/~/sync-demo/
    Link:
    https://app.globus.org/activity/04e277f4-8f07-11ec-811e-493dd0cf73a1/overview
    Saving sync transfer ID to last-transfer-id.txt
    

5\. Check on the status of the task. You could do this by

  * following the URL to app.globus.org to view the task under "activities", or

    
    
    $ globus task show <taskid>
    

6\. You could then make some change to either source or destination directory,
and simply re-run the script

    
    
    $ ./cli-sync.sh
    

7\. Experiment by changing the SYNCTYPE. Other options are:

  * see [here for descriptions of the available sync levels](https://docs.globus.org/cli/reference/transfer/#sync_levels): 
    * `EXISTS`
    * `SIZE`
    * `MTYPE`
    * `CHECKSUM`

8\. Schedule automated repeats of the sync operation

You could then consider how to repeat the task automatically. For example:

  * scheduling the running of the cli-sync.sh command on your own machine using cron 
    * Remember: the invocation of the command does NOT need to be done on JASMIN, it can be done wherever you have the CLI installed, for example your local machine.
  * Learn about how to [use timers with Globus](https://www.globus.org/blog/globus-now-supports-recurring-and-scheduled-transfers): these can be set up using the web interface or using an additional CLI [globus-timer-cli](https://pypi.org/project/globus-timer-cli/) which can be installed into the same `virtualenv` as the main globus cli.

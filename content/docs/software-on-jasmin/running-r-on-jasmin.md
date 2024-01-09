---
aliases: /article/5026-running-r-on-jasmin
date: 2023-01-26 15:25:58
description: Running R on JASMIN
slug: running-r-on-jasmin
tags:
- R
- software
- JASMIN
- environment
- packages
- Rscript
title: Running R on JASMIN
---

On the JASMIN `sci` servers and LOTUS, we support the use of **R** through the
"jasr" environment(s), as listed on the [Jaspy page]({{< ref "jaspy-envs">}}).

In order to activate the R environment, you will need to use:

    
    
    module load jasr
    

Note that the Jaspy page lists [all available environments]({{< ref "jaspy-envs" >}}). You can also list the R packages that are available in the
environment by typing:

    
    
    ls $CONDA_PREFIX/lib/R/library/
    	

Once you have activated the environment, you can start R, using:

    
    
    R
    

If you have an R script that you wish to run, you can use the "Rscript"
command, such as:

    
    
    Rscript <myscript>
    

The following shows the options available when using "Rscript":

    
    
    $ Rscript --help
    Usage: /path/to/Rscript [--options] [-e expr [-e expr2 ...] | file] [args]
    
    
    --options accepted are
      --help              Print usage and exit
      --version           Print version and exit
      --verbose           Print information on progress
      --default-packages=list
                          Where 'list' is a comma-separated set
                            of package names, or 'NULL'
    or options to R, in addition to --no-echo --no-restore, such as
      --save              Do save workspace at the end of the session
      --no-environ        Don't read the site and user environment files
      --no-site-file      Don't read the site-wide Rprofile
      --no-init-file      Don't read the user R profile
      --restore           Do restore previously saved objects at startup
      --vanilla           Combine --no-save, --no-restore, --no-site-file
                            --no-init-file and --no-environ
    
    
    'file' may contain spaces but not shell metacharacters
    Expressions (one or more '-e <expr>') may be used *instead* of 'file'
    See also  ?Rscript  from within R
    <br>
    

The version number (currently 4.0.5) is reported when you start R, or if you
type:

    
    
    R --version
    

Here are commands to do a simple plot to a file, which you can use to test
running R either interactively or with "Rscript" as described above.

    
    
    png("myplot.png")
    x <- c(1,2,3,4)
    y <- x*x
    plot(x,y)
    dev.off()
    

(You could use the "display" command on JASMIN to view the output file.)

Here is a minimal example of using the "library" command to load one of the
many add-on libraries that have been installed to supplement the core R
distribution. It uses the "prettyunits" package to convert a number of bytes
to human-readable format.

    
    
    [username@sci3.jasmin.ac.uk ~]$ module load jasr
    [username@sci3.jasmin.ac.uk ~]$ R --quiet
    > library(prettyunits)
    > pretty_bytes(12345678)
    [1] "12.35 MB"
    >
    
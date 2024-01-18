---
aliases: /article/209-idl-and-midl
date: 2022-10-20 15:47:58
description: IDL and MIDL
slug: idl-and-midl
title: IDL and MIDL
---

This article explains how to:

  * use the IDL software on JASMIN 
  * run these tools on the scientific analysis servers and LOTUS
  * make efficient use of the IDL licences
  * use the MIDL software on JASMIN **\- NOW DEPRECATED**

### What is IDL?

[IDL](https://www.harrisgeospatial.com/Software-Technology/IDL) stands for
Interactive Data Language. It is a licensed data manipulation toolkit made
available on JASMIN.

### Availability of IDL on JASMIN

IDL is available on all [scientific analysis servers]({{< ref "sci-servers"
>}}) and [LOTUS](http://help.ceda.ac.uk/category/107-batch-computing-on-
lotus).

To get started with **IDL** , login on one of scientific analysis servers and
run the commands:

    
    
    $ # First add the IDL module 
    $ module load idl  
    
    $ # Then you can run IDL at the command-line 
    $ idl  
    
    IDL Version 8.4 (linux x86_64 m64). (c) 2014, Exelis Visual Information Solutions, Inc. 
    Installation number: 406672. 
    Licensed for use by: Science & Technology Facilities Council 
    
    IDL> print,1+4        
          5
    		

For **help** information about either installation you can type one of these
help commands:

    
    
    $ module help idl  
    ----------- Module Specific Help for 'idl/8.2' --------------------  	
               Adds IDL 8.2 to your environment variables,  
      
    

### Making efficient use of IDL development licences

We have a large pool of run-time licences and a much more limited pool of
development licences. In each case, these consist of floating licences shared
between JASMIN/CEMS machines and LOTUS.

Users are welcome to run multiple instances of IDL code, but for that purpose
please make use of the run-time licences by compiling your code using a single
development session and then running the pre-compiled code using the `-rt`
flag. An example of this is shown in the next section (below).

Please try not to run more than one or two simultaneous IDL development
sessions. However, for licence purposes, each unique combination of username,
hostname, and `$DISPLAY` variable counts as a single session. So for example,
if you run idl (development mode) in one window, then suspend it (ctrl-Z) and
start another development session in the same window, this still is only
counted as one session by the licence server because the username, hostname,
and $DISPLAY are all identical between the two processes. But if you "ssh" in
on two different windows, probably the `$DISPLAY` will differ between the two
windows (e.g. `localhost:10` and `localhost:11`), so if you start idl
development sessions in each window they will require separate licences.

To see what licences you and others are using, you can use the following
sequence of commands:

    
    
    $ module add idl/8.2 
    $ export LM_LICENSE_FILE=27022@sctlic1.esc.rl.ac.uk,27022@sctlic2.esc.rl.ac.uk,27022@sctlic3.esc.rl.ac.uk 
    $ lmstat -a
    		

When interpreting the numbers, note that a single session is counted as 6
licences.

### Using IDL on LOTUS (via the run-time Licences)

IDL run-time licences are available for use on the LOTUS cluster. In order to
specify use of the run-time licences please follow the instructions here. You
need to compile your IDL code in order to run in run-time mode.

**Here is an example program that you might want to compile**

The example program, "foo", depends on some other functions.

    
    
    ======== foo.pro =======
     pro foo  
     print, doubleit(10) end 
    ========================
    		
    
    
    ===== doubleit.pro ===== 
    function doubleit, n   
    return, two() * n 
    end 
    ========================
    		
    
    
    ======= two.pro ======== 
    function two   
    return, 2 
    end 
    ========================
    		

**You must save a compiled version of the code:**

1\. Compile the program:

    
    
    IDL> .compile foo    <=== compiles top-level routine only 
    % Compiled module: FOO.
    		

2.Use resolve_all to compile routines it depends on:

    
    
    IDL> resolve_all     <=== recursively search for and compile modules called 
    % Compiled module: DOUBLEIT. 
    % Compiled module: TWO.
    		

3\. Save all compiled routines to a file:

    
    
    IDL> save, /routines, file='foo.sav'
    		

**To run the program, using a run-time licence only:**

    
    
    $ idl -rt=foo.sav 
    IDL Version 8.4 (linux x86_64 m64). (c) 2014, Exelis Visual Information Solutions, Inc.
    Installation number: 406502. 
    Licensed for use by: Science & Technology Facilities
            20<br>
    		

> NOTE: **Using` -vm=` instead of `-rt=` opens the save file in the IDL
> virtual machine. No run-time licence is required, but a splash screen must
> be dismissed interactively, so it is not suitable for queues on the
> cluster.**

**To see what routines are present in the save file:**

    
    
    IDL> .reset_session     <=== removes any existing compiled modules  
    
    IDL> help               <=== show compiled modules (and variables); there shouldn't be any 
    % At $MAIN$           
    Compiled Procedures:
         $MAIN$  
    
    Compiled Functions:  
    
    IDL> restore,'foo.sav'   <=== load contents of save file  
    
    IDL> help 
    % At $MAIN$          
    Compiled Procedures:
         $MAIN$  FOO                     <=== this was loaded from foo.sav  
    
    Compiled Functions: 
         DOUBLEIT    TWO            <=== so were these
    		

**Passing arguments**

You can also pass arguments in to your code as follows:

In your code, use function `command_line_args`, for example:

    
    
    argsarray = command_line_args(count = nparams)<br>
    		

Call the code with -args flag:

    
    
    idl -rt=foo.sav -args 10 20 30<br>
    		

> `command_line_args` returns a string array, so convert type as required,
> e.g. `n = fix(argsarray[0]) `

### Example usage of IDL Run-time Licences in a MIDL program [NOW DEPRECATED]

 **NOTE: The "midl" module is no longer supported on JASMIN, because the
latest version was dated**

To run MIDL, run the commands:

    
    
    $ # First add the MIDL module $ module load midl    
    
    $ # Then you can run MIDL at the command-line   
    
    $ midl -d   IDL Version 8.2 (linux x86_64 m64). 
    (c) 2012, Exelis Visual Information Solutions, Inc.  
    Installation number: 406672. 
    Licensed for use by: Science & Technology Facilities Council     
    
    A complete list of UKMO IDL routines can be found in $IU_LIB/README.  
    For on-line help on an individual routine, use the man command.  Enter man,'man' for information about this command.  
    *******************************************************************************  
    Met Office Hadley Centre IDL software (c) Crown Copyright  
    Licensed to NCAS and the Department of Meteorology  
    *******************************************************************************   
    % Compiled module: STRREPLACE.  
    % Compiled module: DATATYPE.  
    % Compiled module: BASENAME.  
    % Compiled module: NICE_X_COLORS.  
    
    MIDL> 		

> NOTE: The "-d" argument is required because MIDL only currently runs in
> 64-bit mode.

You will need to include `@idl_startup` in your main program even though
normally midl runs this for you. Here is an example that reads the file
onerec.pp (a copy of which can be found at
/apps/idl_tools/example_files/onerec.pp on JASMIN), and prints some header
info:

    
    
    ======== mytest.pro ======= 
    pro mytest 
    @idlstartup 
    z = ppa('onerec.pp') 
    print, 'LBNPT:', z.lbnpt 
    end 
    ============================
    		

We compile it:

    
    
    $ module add midl 
    $ midl -d 
    MIDL> .compile mytest 
    MIDL> resolve_all, /continue_on_error 
    MIDL> save, /routines, file='mytest.sav' 
    MIDL> exit
    		

Before running, you may also need to set the following environment variable so
that you have access to shared libraries when not running the "midl" script
directly:

    
    
    export WAVE_SHARED_PATH=$MIDL_DIR/ukmo_idl/dlm/Linux64<br>
    		

Then run it:

    
    
    $ idl -rt=mytest.sav 
    [...] 
    % PPALIST: File ./onerec.pp contains 1 fields 
    LBNPT:          192<br>
    		

Note, the `/continue_on_error` is needed because the routines `info` and
`compare` are missing. We suspect that these routines may be present in WAVE
but missing in IDL. Most likely the calls are not executed in any case,
particularly if your code completes successfully when run "normally" using a
development licence. If you add the following dummy code to the end of
`mytest.pro` then the `/continue_on_error` is not necessary:

    
    
    pro info 
    end 
    
    function compare 
    end<br>
    		

Note that in order to make this work, we made a small local tweak to the MIDL
installation on JASMIN. If you wish to copy this procedure using a MIDL
deployment elsewhere (using MIDL version 20140411), you may need to do the
same, or else `.compile` will fail on routines that contain `@idlstartup`.
Here is the patch.

    
    
    --- ukmo_idl/lib/defpp.orig     2016-06-06 19:00:45.793486745 +0100 
    +++ ukmo_idl/lib/defpp  2016-06-06 19:00:49.857537573 +0100 
    @@ -153,7 +153,8 @@
      ;; LPJC Always force 256 colours on Linux  
      IF wave_max_colors NE 256 AND !version.os EQ 'Linux' THEN BEGIN $ 
            wave_max_colors=256 & $ 
    -       PRINT,'WARNING - Ignoring $WAVE_MAX_COLORS and providing 256 cell colour tables' 
    +       PRINT,'WARNING - Ignoring $WAVE_MAX_COLORS and providing 256 cell colour tables' & $ 
    +ENDIF 
     defsysv, '!Max_colors', wave_max_colors    
    
     wave_allow_private_cols=LONG(GETENV('WAVE_ALLOW_PRIVATE_COLS'))<br>
    		



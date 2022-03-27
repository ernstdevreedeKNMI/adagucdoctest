Troubleshooting
===============

The service returns an internal service error
---------------------------------------------

-   Check if the apache server is able to execute CGI scripts, check if
    the CGI script has execute permissions. Below a test script can be
    used to check whether the apache server is configured correctly:
    ```
    \#!/bin/bash
    echo "Content-type: text/html"
    echo ''
    echo Hello World!
    ```

Performance issues
------------------

When ADAGUC performs slow it can have several issues related to
filesystems, databases, cpu, memory, networks and datafile
organizations. ADAGUC can be compiled with the flag -DMEASURE\_TIME
enabled. This can be enabled by compiling with the environment
variable:
```
export ADAGUCCOMPILERSETTINGS="-Wall -DMEMLEAKCHECK -DMEASURETIME"
```

This enables timing of several components in detail and can give insight
where the bottleneck is. The timing information is written to the
standard logfile.

-   Postgres connection speed can sometimes greatly be improved when
    setting in the PostGres config file postgresql.conf
    ```
    log\_hostname = off
    ```


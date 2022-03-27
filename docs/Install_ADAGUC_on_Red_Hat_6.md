Install ADAGUC on Red Hat 6
===========================

Required packages for the Adaguc server software
------------------------------------------------

-   gcc compiler suite with g**.
-   mercurial
-   libproj-devel
-   libgd-devel
-   libcurl-devel
-   libfreetype2-devel
-   libpng-devel
-   zlib-devel
-   libxml2-devel
-   lpq-devel (postgres)
-   sqlite-devel
-   python-isodate \# Optional: needed for some python scripts handling
    time dimensions

For Red Hat 6.2 with EPEL repositories (compiling netcdf and hdf5 not
needed in this case):
```
yum install gcc gcc-c** mercurial libpng-devel zlib-devel libxml2-devel
\\
gd-devel netcdf-devel hdf5-devel proj-devel postgresql-devel
udunits2-devel \\
gdal-devel cairo-devel httpd postgresql-server sqlite-devel
```

Required software libraries:
----------------------------

-   hdf5 1.8.7 or newer
-   netcdf-4.1.3 or newer

### Compile instructions for hdf5

Download source code from http://www.hdfgroup.org/downloads
```
tar -xzvf hdf5-1.8.x.tar.gz
cd hdf5-1.8.x
./configure --prefix=&lt;installdir&gt;
make
make test
make install
```

### Compile instructions for netcdf4

Download source code for C library from
http://www.unidata.ucar.edu/software/netcdf
```
tar -xzvf netcdf-4.x.y.tar.gz
cd netcdf-4.x.y
./configure --prefix=&lt;installdir&gt; --with-hdf5=&lt;installdir&gt;
--with-udunits --enable-netcdf-4 --enable-cxx-4 --enable-shared
CPPFLAGS=-I&lt;installdir&gt;/include LDFLAGS=-L&lt;installdir&gt;/lib
make
make check
make install
```

### Compile instructions for gdal

Download source code from http://download.osgeo.org/gdal/
```
tar -xzvf gdal-1.8.1
cd gdal-1.8.1
./configure --prefix=&lt;installdir&gt; LDFLAGS="-ludunits2"
make
make install
```

Compile the adaguc sourcecode
-----------------------------

The source code is kept in a Mercurial repository at
http://dev.knmi.nl/hg/adagucserver

Fetch the source code from the repository into a directory named
adagucserver with the follwing GIT command:
```
git clone https://github.com/KNMI/adaguc-server
```

The software can be built by invoking the compile.sh script in the
adagucserver directory. If any compile or link time information is
needed this can be passed to the compile.sh script through the CPPFLAGS
and the LDFLAGS environment variables. For example:
```
export CPPFLAGS="-I/home/user/software/install/include
-I/home/user/othersoftware/install/include"
export LDFLAGS="-L/home/user/software/install/lib/
-L/home/user/othersoftware/install/lib/"
```

The compile.sh script builds the adagucserver executable and the
h5ncdump utility in the bin subdirectory of the adagucserver source code
directory. The executable has to be moved manually to the directory from
where it will be invoked by the CGI script.

Create a CGI script in the http server's cgi directory
------------------------------------------------------

The adagucserver is invoked through a CGI script by the web server
(usually an Apache web server). Find out where CGI-scripts can be stored
on your system (determined by the Apache configuration) and create a CGI
script for the web service

The CGI script can have the following form:

```
\#!/bin/bash

1.  LD\_LIBRARY\_PATH not needed when netcdf and hdf5 installed through
    yum.
    export
    LD\_LIBRARY\_PATH=&lt;installdir&gt;/lib/:\$LD\_LIBRARY\_PATH
    export ADAGUC\_CONFIG=&lt;installdir&gt;/config/exampleconfig.xml
    export ADAGUC\_LOGFILE=&lt;installdir&gt;/logs/exampleconfig.log
    export
    ADAGUC\_ERRORFILE=&lt;installdir&gt;/logs/exampleconfig.errlog
    &lt;adagucserverlocation&gt;/adagucserverEC/adagucserver

returnCode=\$?
if \[ "\$returnCode" != "0" \]; then
echo "Content-type: text/html"
echo ""
echo "Message:&lt;br&gt;"
echo rv: \$returnCode
if \[ "\$returnCode" == "143" \]; then echo "= Application was killed";
fi;
echo "&lt;br&gt;"
echo "/Message:&lt;br&gt;"
fi
```

It is important to notice that this CGI script usually runs under the
user id (uid) of the Apache web server. Therefore the directory where
the logfiles reside (ADAGUC\_LOGFILE and ADAGUC\_ERRORFILE) must be
writable for the web server's user id and the files if they already
exist must be writable for the web server's uid.
The config file (ADAGUC\_CONFIG) and it's path should also be readable
for the web server's uid.

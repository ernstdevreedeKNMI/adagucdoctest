Install ADAGUC on KNMI Fedora workstations
==========================================

Quick install ADAGUCServer
--------------------------

1.  cd \# Home dir
2.  git clone https://github.com/KNMI/adaguc-server
3.  cd \~/adaguc-server
4.  bash compile.sh
5.  cp ~/adaguc-server/data/cgi-bin/adaguc.testdata.cgi~/public\_html/
6.  chmod +x \~/public\_html/adaguc.testdata.cgi
7.  export
    ADAGUC\_TMP=~/tmp/;mkdir\ -p\ \$ADAGUC\_TMP;export\ ADAGUC\_PATH=~/adaguc-server/;
    \~/adaguc-server/adagucserverEC/adagucserver --updatedb --config
    "\$ADAGUC\_PATH/data/config/adaguc.testdata.xml"
8.  ADAGUCServer is now accessible in your webbrowser via:
    http://yourmachine.knmi.nl/\~yourusername/adaguc.testdata.cgi?
9.  Set ADAGUC\_ONLINERESOURCE in \~/public\_html/adaguc.testdata.cgi to
    this URL.
10. If you are using a viewer hosted on a different machine, then add
    the CORS headers (see below)
11. This URL can be explored in an ADAGUC viewer with access to your
    host via "Add Layers"~~&gt;"Add Custom WMS Service"~~&gt;Enter your
    URL in the box and press "Enter".
    -   Or directly via at
        http://birdexp02.knmi.nl/plieger/adagucviewer/\#addlayer('http://bhw485.knmi.nl:8080/cgi-bin/adaguc.testdata.cgi?','testdata')
12. GetMap looks like
    -   http://birdexp02.knmi.nl/cgi-bin/plieger/adaguc.testdata.cgi?SERVICE=WMS&amp;SERVICE=WMS&amp;VERSION=1.3.0&amp;REQUEST=GetMap&amp;LAYERS=testdata&amp;WIDTH=1000&amp;HEIGHT=750&amp;CRS=EPSG%3A4326&amp;BBOX=30,-30,75,30&amp;STYLES=testdata%2Fnearest&amp;FORMAT=image/png&amp;TRANSPARENT=TRUE
    -   or with styling and extra layers:
        http://birdexp02.knmi.nl/cgi-bin/plieger/adaguc.testdata.cgi?SERVICE=WMS&amp;SERVICE=WMS&amp;VERSION=1.3.0&amp;REQUEST=GetMap&amp;LAYERS=baselayer,testdata,overlay&amp;WIDTH=1000&amp;HEIGHT=750&amp;CRS=EPSG%3A4326&amp;BBOX=30,-30,75,30&amp;STYLES=,testdata%2Fshadedcontour&amp;FORMAT=image/png&amp;TRANSPARENT=TRUE
13. Complete!

### CORS headers

Add the following lines before the call to adagucserver (which is on the
last line)
```
echo "Access-Control-Allow-Origin: \*"
echo "Access-Control-Allow-Methods: GET"
```

### Setup autowms

1.  mkdir \~/public\_html/adaguc.conf.d
2.  cp "\${ADAGUC\_PATH}/data/config/adaguc.autoresource.xml"
    \~/public\_html/adaguc.conf.d
3.  Create autowms endpoint in \~/public\_html/adaguc.autoresource.cgi
4.  chmod +x \~/public\_html/adaguc.autoresource.cgi
    \#

```
\#!/bin/bash
export ADAGUC\_PATH=\~/adaguc-server/ \# Replace with the location where
you installed ADAGUC
export ADAGUC\_TMP=\~/tmp/
HOME=\`echo \~\`
USER=\`basename \${HOME}\`

export
ADAGUC\_CONFIG="\${HOME}/public\_html/adaguc.conf.d/adaguc.autoresource.xml"
export ADAGUC\_DATARESTRICTION="FALSE"
export ADAGUC\_LOGFILE="\${ADAGUC\_TMP}/adaguc.autoresource.log"
export ADAGUC\_ERRORFILE="\${ADAGUC\_TMP}/adaguc.autoresource.errlog"
export ADAGUC\_FONT="\${ADAGUC\_PATH}/data/fonts/FreeSans.ttf"
export
ADAGUC\_ONLINERESOURCE="http://\${HTTP\_HOST}/\~\${USER}/adaguc.autoresource.cgi?"

\#export LD\_LIBRARY\_PATH=:\$LD\_LIBRARY\_PATH \# LD\_LIBRARY\_PATH not
needed when netcdf and hdf5 installed through yum.
\#export PROJ\_LIB=/data/build/share/proj/ \# Optional, needed when
custom proj.4 library is installed.

echo "Access-Control-Allow-Origin: \*"
echo "Access-Control-Allow-Methods: GET"

\${ADAGUC\_PATH}/adagucserverEC/adagucserver
```

Quick install ADAGUCViewer
--------------------------

1.  cd \~/public\_html
2.  git clone https://github.com/KNMI/adaguc-viewer
3.  Visit
    http://&lt;yourmachine&gt;.knmi.nl/\~&lt;yourusername&gt;/adagucviewer
4.  Complete!

Adjust adagucviewer/config.js to add your own services, or just use "Add
Layers"~~&gt;"Add Custom WMS Service"~~&gt;Enter your URL in the box and
press "Enter".

Setup postgresql - only needed when having problems with sqlite:
----------------------------------------------------------------

1\) In your bash resource file edit the PGDATA environment variable to
point to a directory of your choice:

edit file: \~/.bashrc
```
export PGDATA=\${HOME}/postgresdb
```

2\) Initialize the database by executing the program initdb

```
initdb
```

3\) The database is running as local user, some settings need to be
changed for this in:

edit file: \${PGDATA}/postgresql.conf
```
\#add:
unix\_socket\_directories='/tmp'
```

4\) Start the database server
```
pg\_ctl -D \$PGDATA -l \$PGDATA/log start
```

5\) Create a database
```
createdb adagucdb -h localhost
```

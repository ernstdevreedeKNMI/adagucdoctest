Installation
============

1) Full installation instructions on Ubuntu LTS 16.04.2:
--------------------------------------------------------

Instructions on how to install adaguc-services, adaguc-viewer and
adaguc-server on ubuntu can be found here:

https://dev.knmi.nl/projects/adagucserver/wiki/Install\_Adaguc\_on\_Ubuntu

These are also used to create the preinstalled virtual machine.

2) Docker
---------

See the [Docker](Docker.md) page.

3) Quick install ADAGUCServer
-----------------------------

When all prerequisites are met (Required libraries and a web server
supporting CGI scripts), ADAGUC server can be installed in the following
way:

1.  cd \# Home dir
2.  git clone https://github.com/KNMI/adaguc-server
3.  cd \~/adagucserver
4.  bash compile.sh
5.  cp \~/adagucserver/data/cgi-bin/adaguc.testdata.cgi &lt;your cgi-bin
    directory&gt;
6.  chmod +x &lt;your cgi-bin directory&gt;adaguc.testdata.cgi
7.  ADAGUCServer is now accessible in your webbrowser via:
    http://&lt;your
    host&gt;/cgi-bin/adaguc.testdata.cgi?service=WMS&amp;REQUEST=GetCapabilities
8.  This URL can be explored in an ADAGUC viewer with access to your
    host via "Add Layers"~~&gt;"Add Custom WMS Service"~~&gt;Enter your
    URL in the box and press "Enter"
9.  GetMap looks like
    http://bhw485.knmi.nl:8080/cgi-bin/adaguc.testdata.cgi?SERVICE=WMS&amp;&SERVICE=WMS&amp;VERSION=1.3.0&amp;REQUEST=GetMap&amp;LAYERS=testdata&amp;WIDTH=1585&amp;HEIGHT=1075&amp;CRS=EPSG%3A4326&amp;BBOX=30.894567523974764,-27.842459360000003,72.34692747602523,33.27567136&amp;STYLES=testdata%2Fnearestcontour&amp;FORMAT=image/png&amp;TRANSPARENT=TRUE&amp;
10. Complete!

Note: If CURL,GDAL and POSTGRESQL are missing, you can still compile by
adding the following line before step 5:
```export ADAGUCCOMPONENTS="-DADAGUC\_USE\_SQLITE"```
This only uses SQLITE, without CURL, GDAL and POSTGRESQL, e.g. WMS ONLY!
If you have all prerequisites, leave this out.

4) Quick install ADAGUCViewer
-----------------------------

1.  cd &lt;your documentroot directory&gt;
2.  git clone https://github.com/KNMI/adaguc-viewer
3.  Visit http://&lt;your host&gt;/adagucviewer
4.  Complete!
    Adjust adagucviewer/config.js to add your own services, or just use
    "Add Layers"~~&gt;"Add Custom WMS Service"~~&gt;Enter your URL in
    the box and press "Enter".

5) Complete installation instructions for other OS's
----------------------------------------------------

### Installation on Ubuntu

There is a detailed description available for installing Adaguc on
Ubuntu, this has been used to create the virtual machine available from
\[\[Preinstalled\_virtual\_environment\]\]

-   [Install Adaguc on Ubuntu](Install Adaguc on Ubuntu.md)

### Installation on Fedora, KNMI workstations

-   [Install ADAGUC on KNMI Fedora workstations](Install ADAGUC on KNMI Fedora workstations.md)

### Installation on Red Hat 6 (related systems: Scientific Linux, Fedora)

-   [Install ADAGUC on Red Hat 6](Install ADAGUC on Red Hat 6.md)

Shell script and configuration file examples
--------------------------------------------

1.  Shell script templates can be found here:
    https://dev.knmi.nl/projects/adagucserver/repository/show/data/cgi-bin
    The shell script template needs to be put in your cgi-bin directory.
    It sets environment variables and calls the adaguc executable. Make
    sure it has the right permissions: readable and executable by the
    webserver. See [Overview](Overview.md) for details.
2.  For sample config scripts you can look here:
    https://dev.knmi.nl/projects/adagucserver/repository/show/data/config

ADAGUC installation environment variables
-----------------------------------------

Before you do compile.sh, you can set the environment variable
ADAGUCCOMPONENTS to select which components to include. Possible
components are:

1.  ~~DADAGUC\_USE\_GDAL~~ Compile with GDAL, enables the Web Coverage
    Service
2.  ~~DADAGUC\_USE\_POSTGRESQL~~ Compile with PostgreSQL, supports the
    PostGresql database
3.  ~~DADAGUC\_USE\_SQLITE~~ Supports the SQLITE database
4.  ~~DENABLE\_CURL~~ Compile with CURL, used for cascaded WMS services.
5.  ~~DADAGUC\_USE\_KDCMONGODB~~ Compile KDC MongoDB support (boost and
    mongodb client required)
6.  ~~DADAGUC\_USE\_WEBP~~ Compile Google WEBP support for exporting
    images, needs package libweb-dev installed

By default -DENABLE\_CURL -DADAGUC\_USE\_GDAL -DADAGUC\_USE\_SQLITE
-DADAGUC\_USE\_POSTGRESQL are enabled.

You can select the ones you which via de environment variable
ADAGUCCOMPONENTS. For example if you want a WMS without GDAL, PostgreSQL
(No WCS!), you can set:
```
export ADAGUCCOMPONENTS="-DADAGUC\_USE\_SQLITE -DENABLE\_CURL" \# No
GDAL or PostgreSQL: WMS Only
```

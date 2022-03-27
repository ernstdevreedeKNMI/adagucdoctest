Preinstalled virtual environment with ADAGUC Viewer and ADAGUC Server
=====================================================================

For the workshop a preinstalled virtual machine is available. This
machine has apache-tomcat, postgres, adaguc-services, adaguc-server,
adaguc-viewer and apache httpd with php and cgi support installed.

-   http://geoservices.knmi.nl/adagucworkshop/adaguc-xubuntu-2017.ova
    (8.5Gb)
-   http://geoservices.knmi.nl/adagucworkshop/adaguc-xubuntu-2018.ova
    (8.5Gb) - update of the 2017 VM with latest version according to
    instructions written below.

**The installation instructions can be found here:
\[\[Install\_Adaguc\_on\_Ubuntu\]\]**

The following repositories are used:

-   https://github.com/KNMI/adaguc-services - Java application for
    running adaguc-server from tomcat or as a spring boot application
-   https://github.com/KNMI/adaguc-server - C** server for serving WMS,
    WCS and OpenDAP
-   https://github.com/KNMI/adaguc-viewer - Javascript web client for
    connecting to WMS
-   https://github.com/KNMI/adaguc-datasets - Example dataset
    configurations

Installation of the virtual image
---------------------------------

1.  The virtual image can be downloaded from
    http://geoservices.knmi.nl/adagucworkshop/adaguc-xubuntu-2017.ova
    (8.5 Gb, when unpacked 20 Gb)
2.  Install Oracle Virtualbox with the corresponding extension pack from
    https://www.virtualbox.org/wiki/Downloads
3.  Start Virtualbox, click File -&gt; Import appliance. In the
    settings, set the memory as high as possible, by default it is set
    to 2048Mb, but 4096Mb is recommended.
4.  In the VM, just start firefox and the adaguc-viewer will show as
    default page
5.  From the viewer, the AutoWMS plugin can be opened via clicking on
    the big gear and selecting AutoWMS from the list. A window on the
    right opens, displaying all files and folders available.

The VM exposes port 80 and 8080 to localhost, which means that links
should work outside of the VM on the host as well.
Use the password "adaguc" to obtain sudo rights

Update the VM to the 2018 version
---------------------------------

For the 2018 Workshop, you need to update the ADAGUC software suite. You
do not need to upgrade the VM to the latest Ubuntu.

Update adaguc-dataset examples
```
\#
cd /data/adaguc-datasets
git pull
\#
```

Update adaguc-server
```
\#Install libraries for testing purposes
echo "adaguc" | sudo -S apt-get update -y
sudo apt-get install python-lxml python-netcdf4 -y

\#Pull and build adaguc-server
cd /src/KNMI/adaguc-server/
git checkout .
git pull
bash compile.sh
bash runtests.sh

\#Re-scan all datasets
sudo mkdir /adaguc /servicehealth
sudo chown adaguc: /servicehealth
sudo ln -s /src/KNMI/adaguc-server/ /adaguc/adaguc-server-master
sudo ln -s /src/KNMI/adaguc-server/data/config/adaguc.vm.xml
/adaguc/adaguc-server-config.xml

dropdb adaguc
createdb adaguc
bash /src/KNMI/adaguc-server/Docker/adaguc-server-updatedatasets.sh

\#
```

Update adaguc-services
```
cd /src/KNMI/adaguc-services/
rm -rf target
git pull
mvn package
cp target/adaguc-services-\*.war
/src/apache-tomcat-8.0.44/webapps/adaguc-services.war
cd /src/apache-tomcat-8.0.44/bin
. ../setenv.sh
bash shutdown.sh && sleep 1 && bash startup.sh

\#
```

Update adaguc-viewer which is running in standard APACHE HTTP server
with PHP as backend
```
cd /var/www/html/adaguc-viewer
git checkout .
git pull
echo "xml2jsonrequestURL =
'http://localhost/adaguc-viewer/webmapjs\_php/xml2jsonrequest.php?';"
\\
"autowmsURL = 'http://localhost:8080/adaguc-services/autowms?';" \\
"getFeatureInfoApplications.push({name:'AutoWMS',iconCls:'button\_getfeatureinfo'});"
&gt;&gt; ./config.js

firefox http://localhost/adaguc-viewer/

\#Apply the same steps for the adaguc-viewer which is running in APACHE
TOMCAT with adaguc-services as backend

cd /src/apache-tomcat-8.0.44/webapps/adaguc-viewer/
git checkout .
git pull
echo "xml2jsonrequestURL = '/adaguc-services/xml2json?';" \\
"autowmsURL = '/adaguc-services/autowms?';" \\
"getFeatureInfoApplications.push({name:'AutoWMS',iconCls:'button\_getfeatureinfo'});"
&gt;&gt; ./config.js

firefox http://localhost:8080/adaguc-viewer/

1.  Please note: You can add "getFeatureInfoApplications.open =
    'AutoWMS';" to make the viewe open the AutoWMS viewer by default.

\#
```

Optionally Update docker. Only needed if you would like to build the
docker yourself
```
sudo apt-get update
sudo apt-get install \\
apt-transport-https \\
ca-certificates \\
curl \\
software-properties-common
curl ~~fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key
add~~
sudo add-apt-repository \\
"deb \[arch=amd64\] https://download.docker.com/linux/ubuntu \\
\$(lsb\_release -cs) \\
stable"
sudo apt-get update
sudo apt install -y docker-ce=17.12.0\~ce-0\~ubuntu

sudo groupadd docker
sudo usermod -aG docker \$USER
sudo systemctl enable docker

sudo curl -L
"https://github.com/docker/compose/releases/download/1.23.1/docker-compose-\$(uname
~~s)~~\$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version

1.  Reboot
    docker system prune -a

```

Install aws-cli
```
\#
sudo apt install python-pip
pip install awscli
aws s3 ls noaa-goes16/ --no-sign-request
\#
```

Important directories and files
-------------------------------

-   /src/KNMI/adaguc-server - Git repo where adaguc-server is installed,
    compiled with gcc, and location where default configuration files
    are stored. Compiled with "bash compile.sh"
-   /src/KNMI/adaguc-services - Git repo where adaguc-services is
    installed, build with maven and deployed in webapps dir
-   /src/config/adaguc-services-config-tomcat.xml - Adaguc-services
    configuration file. Note: this is the tomcat web application to run
    adaguc-server.
-   /src/KNMI/adaguc-server/data/config/adaguc.vm.xml - Adaguc-server
    configuration file, this file is in the adaguc-server repository on
    github
-   /src/log - Log file directory
-   /src/tomcatstarter.sh - Tomcat startup script
-   /src/crontab - Crontab to start tomcat
-   /src/apache-tomcat-8.0.44 - http://localhost:8080/ - Home of apache
    tomcat
    -   /src/apache-tomcat-8.0.44/webapps/adaguc-viewer - Adaguc viewer
        served with Apache tomcat. Specific configuration settings are
        appended to config.js:
    -   /src/apache-tomcat-8.0.44/webapps/adaguc-services
-   /data/adaguc-autowms - Location where NetCDF files can be stored and
    are automatically available in a WMS via the source= kvp
    (http://localhost:8080/adaguc-services/adagucserver?source=&lt;URL
    Encoded NetCDF file location)
-   /data/adaguc-datasets - Location where Adaguc dataset configurations
    are stored. Examples below.
-   /var/www/html - http://localhost/ - Documentroot of Apache http
    server
    -   /var/www/html/adaguc-viewer - Adaguc viewer served with Apache
        HTTP
-   /var/www/cgi-bin
    -   /var/www/cgi-bin/adaguc-datasets.cgi - OpenDAP server demo
        http://localhost/cgi-bin/adaguc-datasets.cgi/opendap/opendapdataset/RADNL\_OPER\_R**\_25PCPRR\_L3\_KNMI.nc
-   http://localhost:8080/adaguc-services/adagucserver? - Adaguc server
    via adaguc-services and apache tomcat
-   http://localhost/cgi-bin/adaguc-datasets.cgi? - Adaguc server via
    CGI and apache HTTP server

Adaguc viewer
-------------

The viewer is located at:
http://localhost:8080/adaguc-viewer/

The AutoWMS plugin can be opened via clicking on the big gear and
selecting AutoWMS from the list. A window on the right opens, displaying
all files and folders available.

Example NetCDF files
--------------------

To update example NetCDF files, please run:
```
cd /data/adaguc-autowms/testsets
./update.sh
```
This will load new files from the KDC. (https://data.knmi.nl)

Links to dataset configuration examples:
----------------------------------------

\* These example configuration datasets are hosted at
https://github.com/KNMI/adaguc-datasets

\* They can be linked into the service by doing:
http://localhost:8080/adaguc-services/adagucserver?dataset=&lt;dataset
name&gt;

\* See [Dataset](Dataset.md) for details on how ADAGUC datasets work.

\* adaguc-datasets can be updated from github by doing:

****\* ```
cd /data/adaguc-datasets/
git pull
```

Radar - RADNL\_OPER\_R**\_25PCPRR\_L3:

-   https://github.com/KNMI/adaguc-datasets/blob/master/RADNL\_OPER\_R**\_25PCPRR\_L3.xml
-   /data/adaguc-datasets/RADNL\_OPER\_R**\_25PCPRR\_L3.xml
-   UpdateDB command: ```
    export ADAGUC\_PATH=/src/KNMI/adaguc-server/
    export ADAGUC\_TMP=/tmp
    cd /src/KNMI/adaguc-server
    ./bin/adagucserver --updatedb --recreate --config
    /src/KNMI/adaguc-server/data/config/adaguc.vm.xml,/data/adaguc-datasets/RADNL\_OPER\_R**\_25PCPRR\_L3.xml

\# The postgres DB can be checked by doing
psql "user=adaguc password=adaguc host=localhost dbname=adaguc"
select \* from radnl\_oper\_r**\_25pcprr\_l3\_knmi\_time;
```

-   http://localhost:8080/adaguc-services/adagucserver?dataset=RADNL\_OPER\_R**\_25PCPRR\_L3&amp;service=wms&amp;request=getcapabilities
-   http://localhost:8080/adaguc-viewer/?srs=EPSG%3A3857&amp;bbox=90859.44342245569,6226189.307935331,1154637.6754393307,7127898.264872712&amp;service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fdataset%3DRADNL\_OPER\_R*25PCPRR\_L3%26service%3Dwms%26request%3Dgetcapabilities&amp;layer=RADNL\_OPER\_R*\_\_25PCPRR\_L3\_COLOR%24image%2Fpng%24true%24default%241%240&amp;selected=0&amp;dims=time\$2015-06-05T14:30:00Z&amp;baselayers=streetmap\$ne\_10m\_admin\_0\_countries\_simplified

Himawari - adaguc.tiled:

-   https://github.com/KNMI/adaguc-datasets/blob/master/adaguc.tiled.xml
-   https://github.com/KNMI/adaguc-datasets/blob/master/createtiles.sh
-   http://localhost:8080/adaguc-viewer/?srs=EPSG%3A3857&amp;bbox=6762555.090573601,-13593065.064726355,23783741.93277877,834901.3773220861&amp;service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fdataset%3Dadaguc.tiled%26service%3Dwms%26request%3Dgetcapabilities&amp;layer=himawari%24image%2Fpng%24true%24auto%2Frgba%241%240&amp;selected=0&amp;dims=time\$2016-11-14T05:20:00Z&amp;baselayers=streetmap\$ne\_10m\_admin\_0\_countries\_simplified

TU Delft / RWS traffic demo - tud\_traffic:

-   https://github.com/KNMI/adaguc-datasets/blob/master/tud\_traffic.xml
-   http://localhost:8080/adaguc-viewer/?srs=EPSG%3A3857&amp;bbox=451744.4333238476,6776586.21799177,611732.3280491524,6912199.55668723&amp;service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fdataset%3Dtud\_traffic%26service%3Dwms%26request%3Dgetcapabilities&amp;layer=flow%24image%2Fpng%24true%24verkeer-inp%2Flinearinterpolation%241%240&amp;selected=0&amp;dims=time\$2017-03-14T02:34:00Z&amp;baselayers=streetmap\$ne\_10m\_admin\_0\_countries\_simplified

Last 100 earthquakes in NL -
urn\_xkdc\_ds\_nl.knmi\_*aardbevingen\_nederland\_2*

-   https://github.com/KNMI/adaguc-datasets/blob/master/urn\_xkdc\_ds\_nl.knmi\_*aardbevingen\_nederland\_2*.xml
-   http://localhost:8080/adaguc-viewer/?srs=EPSG%3A3857&amp;bbox=400399.7979274943,6474456.81428726,1102190.704937506,7069328.12082674&amp;service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fdataset%3Durn\_xkdc\_ds\_nl.knmi\_*aardbevingen\_nederland\_2*%26service%3Dwms%26request%3Dgetcapabilities&amp;layer=magnitude%24image%2Fpng%24true%24magnitude2%2Fpoint%241%240&amp;selected=0&amp;baselayers=streetmap\$ne\_10m\_admin\_0\_countries\_simplified

Actual 10 minute data from KNMI automated weather stations (Run cd
/data/adaguc-autowms/testsets && ./update.sh first to get actual data
from KDC) - urn\_xkdc\_ds\_nl.knmi\_*Actuele10mindataKNMIstations\_1*

-   https://github.com/KNMI/adaguc-datasets/blob/master/urn\_xkdc\_ds\_nl.knmi\_*Actuele10mindataKNMIstations\_1*.xml
-   cd /data/adaguc-autowms/testsets && ./update.sh
-   http://localhost:8080/adaguc-viewer/?srs=EPSG%3A3857&amp;bbox=115014.02310656349,6516171.689027924,1043717.2040101484,7303384.616828946&amp;service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fdataset%3Durn\_xkdc\_ds\_nl.knmi\_*Actuele10mindataKNMIstations\_1*%26service%3Dwms%26request%3Dgetcapabilities&amp;layer=ta%24image%2Fpng%24true%24temperature%2Fpoint%241%240&amp;selected=0&amp;baselayers=streetmap\$ne\_10m\_admin\_0\_countries\_simplified

Climatology of automated weather stations 1950-present -
urn\_xkdc\_ds\_nl.knmi\_*etmaalgegevensKNMIstations\_1*:

-   https://github.com/KNMI/adaguc-datasets/blob/master/urn\_xkdc\_ds\_nl.knmi\_*etmaalgegevensKNMIstations\_1*.xml
-   http://localhost:8080/adaguc-viewer/?srs=EPSG%3A3857&amp;bbox=324927.13877182454,6525820.151768202,1026718.0457818363,7120691.458307682&amp;service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fdataset%3Durn\_xkdc\_ds\_nl.knmi\_*etmaalgegevensKNMIstations\_1*%26service%3Dwms%26request%3Dgetcapabilities&amp;layer=TG%24image%2Fpng%24true%24temperature%2Fpoint%241%240&amp;selected=0&amp;&baselayers=streetmap\$ne\_10m\_admin\_0\_countries\_simplified

Demo dataset - dataset\_a:

-   https://github.com/KNMI/adaguc-datasets/blob/master/dataset\_a.xml
-   http://localhost:8080/adaguc-viewer/?srs=EPSG%3A3857&amp;bbox=-1525732.9191845017,4347867.331868552,2916439.836328308,8113263.954353271&amp;service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fdataset%3Ddataset\_a%26service%3Dwms%26request%3Dgetcapabilities&amp;layer=testdata%24image%2Fpng%24true%24testdata%2Fshadedcontour%241%240&amp;selected=0&amp;baselayers=streetmap\$ne\_10m\_admin\_0\_countries\_simplified

Masking via DataPostProcessor - datapostproc\_mask:

-   https://github.com/KNMI/adaguc-datasets/blob/master/datapostproc\_mask.xml
-   http://localhost:8080/adaguc-viewer/?srs=EPSG%3A3857&amp;bbox=-1173869.3693216557,3855193.0924690864,4635645.38671054,9058257.909556046&amp;service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2F%2Fwms%3FDATASET%253Ddatapostproc\_mask%26&amp;layer=masked%24image%2Fpng%24true%24auto%2Fnearest%241%240&amp;selected=0&amp;dims=time\$2014-04-30T00:00:00Z,elevation\$0&amp;baselayers=streetmap\$ne\_10m\_admin\_0\_countries\_simplified

Viewer examples
---------------

The viewer has several examples located at
http://localhost/adaguc-viewer/examples/

To see current radar images, go to:

-   http://localhost/adaguc-viewer/examples/animateradar\_latest.php

Opendap Server
--------------

Besides being an OpenDAP client, adaguc-server has the capability to
serve OpenDAP by itself. It can serve a set of files and concatenate
those virtually over dimensions, e.g. aggregations are possible. To
demonstrate this go to:

ncview
http://localhost:8080/adaguc-services/adagucopendap/RADNL\_OPER\_R**\_25PCPRR\_L3/

You can .das or .dds as extension

You can also dump a header of the file:
```
ncdump -h
http://localhost:8080/adaguc-services/adagucopendap/RADNL\_OPER\_R**\_25PCPRR\_L3/
```

**To view an OpenDAP URL with ncview, do:**
```
ncview
http://localhost:8080/adaguc-services/adagucopendap/RADNL\_OPER\_R**\_25PCPRR\_L3/
```

**To view an OpenDAP URL with adaguc-server, do**

http://localhost:8080/adaguc-services/adagucserver?source=http://localhost:8080/adaguc-services/adagucopendap/RADNL\_OPER\_R**\_25PCPRR\_L3/&amp;service=wms&amp;request=getcapabilities

In the viewer:
http://localhost:8080/adaguc-viewer/?srs=EPSG%3A4326&amp;bbox=-0.10856446,46.581272685142864,10.96501046,58.28762331485714&amp;service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fsource%3Dhttp%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucopendap%2FRADNL\_OPER\_R**\_25PCPRR\_L3%2F%26service%3Dwms%26request%3Dgetcapabilities&amp;layer=precipitation%24image%2Fpng%24true%24auto%2Fnearest%241%240&amp;selected=0&amp;dims=time\$2015-06-05T15:55:00Z&amp;baselayers=naturalearth2\$ne\_10m\_admin\_0\_countries\_simplified

Adaguc as OpenDAP client
------------------------

-   http://localhost:8080/adaguc-services/adagucserver?source=&lt;URL
    Encoded OpenDAP URL&gt;
-   You can explore http://opendap.knmi.nl/


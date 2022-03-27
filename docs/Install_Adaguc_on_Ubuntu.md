Install Adaguc Server and Adaguc Viewer on Ubuntu LTS 16.04.2
=============================================================

The following repositories are used:
------------------------------------

-   https://github.com/KNMI/adaguc-services - Java application for
    running adaguc-server from tomcat or as a spring boot application
-   https://github.com/KNMI/adaguc-server - C** server for serving WMS,
    WCS and OpenDAP
-   https://github.com/KNMI/adaguc-viewer - Javascript web client for
    connecting to WMS

This procedure was followed to create the ADAGUC VM image:

Install packages
----------------

```
sudo apt-get -y install vim kate kwrite konsole g** m4 ncview curl git

sudo apt-get -y install postgresql postgresql-server-dev-all
postgresql-client postgresql-client-common postgresql-contrib

(in ubuntu 18 libbggd-dev replaces libgd2-xpm-dev, so for ubuntu 18 do:
sudo apt-get -y install libcurl4-openssl-dev libcairo2-dev libxml2-dev
libgd-dev libudunits2-dev udunits-bin netcdf-bin libnetcdf-dev
libhdf5-dev libproj-dev libgdal-dev
and skip the following line, for ubuntu 16 execute only the following
line)
sudo apt-get -y install libcurl4-openssl-dev libcairo2-dev libxml2-dev
libgd2-xpm-dev libudunits2-dev udunits-bin netcdf-bin libnetcdf-dev
libhdf5-dev libproj-dev libgdal-dev

sudo apt-get -y install default-jre default-jdk maven

sudo apt-get -y install chromium-browser
```

Setup postgresql
----------------

```
sudo service postgresql start
sudo -u postgres createuser --superuser adaguc
sudo -u postgres psql postgres -c "ALTER USER adaguc PASSWORD
'adaguc';"
sudo -u postgres psql postgres -c "CREATE DATABASE adaguc;"
echo "\\q" | psql "dbname=adaguc user=adaguc password=adaguc
host=localhost"
if \[ \${?} -eq 0 \];then
echo "Postgres database setup correctly"
fi
```

Install tomcat
--------------

```
sudo mkdir -p /src/
sudo chown -R \$USER: /src
cd /src/
curl -L
https://archive.apache.org/dist/tomcat/tomcat-8/v8.0.44/bin/apache-tomcat-8.0.44.tar.gz
&gt; apache-tomcat-8.0.44.tar.gz
tar -xzvf apache-tomcat-8.0.44.tar.gz

printf "export CATALINA\_HOME=\\"/src/apache-tomcat-8.0.44\\"\\n\\
export CATALINA\_BASE=\\"/src/apache-tomcat-8.0.44\\"\\n\\
export
ADAGUC\_SERVICES\_CONFIG=/src/config/adaguc-services-config-tomcat.xml\\n\\
export JAVA\_HOME=\\"/usr\\"\\n\\
CONTENT\_ROOT=-Dtds.content.root.path=/src/apache-tomcat-8.0.44/content\\n\\
JAVA\_PREFS\_ROOTS=\\"-Djava.util.prefs.systemRoot=\$CATALINA\_HOME/content/thredds/javaUtilPrefs
-Djava.util.prefs.userRoot=\$CATALINA\_HOME/content/thredds/javaUtilPrefs\\"\\n\\
NORMAL=\\"-d64 -Xmx4096m -Xms512m -server -ea\\"\\n\\
HEAP\_DUMP=\\"-XX:+HeapDumpOnOutOfMemoryError\\"\\n\\
HEADLESS=\\"-Djava.awt.headless=true\\"\\n\\
JAVA\_OPTS=\\"\$CONTENT\_ROOT \$NORMAL \$MAX\_PERM\_GEN \$HEAP\_DUMP
\$HEADLESS \$JAVA\_PREFS\_ROOTS\\"\\n\\
export JAVA\_OPTS" &gt; /src/apache-tomcat-8.0.44/setenv.sh

```

Install adaguc-services
-----------------------

```
sudo mkdir -p /src/KNMI
sudo chown -R \$USER: /src
mkdir -p /src/config
sudo mkdir -p /data
sudo chown -R \$USER: /data
mkdir -p /data/adaguc-services-base
mkdir -p /data/adaguc-services-space
mkdir -p /src/log/
cd /src/KNMI
git clone https://github.com/KNMI/adaguc-services
cd /src/KNMI/adaguc-services
git checkout 1.0.13
mvn package
cp ./target/adaguc-services-\*.war
/src/apache-tomcat-8.0.44/webapps/adaguc-services.war

1.  Configure adaguc-services
    printf "&lt;?xml version=\\"1.0\\" encoding=\\"UTF-8\\"?&gt;\\n\\
    &lt;adaguc-services&gt;\\n\\
    &lt;external-home-url&gt;http://localhost:8080/adaguc-services/&lt;/external-home-url&gt;\\n\\
    &lt;basedir&gt;/data/adaguc-services-base&lt;/basedir&gt;\\n\\
    &lt;userworkspace&gt;/data/adaguc-services-space&lt;/userworkspace&gt;\\n\\
    &lt;server&gt;\\n\\
    &lt;port&gt;8080&lt;/port&gt;\\n\\
    &lt;/server&gt;\\n\\
    &lt;security&gt;\\n\\
    &lt;keystore&gt;/src/keystore.jks&lt;/keystore&gt;\\n\\
    &lt;keystorepassword&gt;password&lt;/keystorepassword&gt;\\n\\
    &lt;keystoretype&gt;JKS&lt;/keystoretype&gt;\\n\\
    &lt;keyalias&gt;tomcat&lt;/keyalias&gt;\\n\\
    &lt;/security&gt;\\n\\
    &lt;adaguc-server&gt;\\n\\
    &lt;adagucexecutable&gt;/src/KNMI/adaguc-server/bin/adagucserver&lt;/adagucexecutable&gt;\\n\\
    &lt;export&gt;ADAGUC\_PATH=/src/KNMI/adaguc-server/&lt;/export&gt;\\n\\
    &lt;export&gt;ADAGUC\_CONFIG=/src/KNMI/adaguc-server/data/config/adaguc.vm.xml&lt;/export&gt;\\n\\
    &lt;export&gt;ADAGUC\_DATARESTRICTION=FALSE&lt;/export&gt;\\n\\
    &lt;export&gt;ADAGUC\_FONT=/src/KNMI/adaguc-server/data/fonts/FreeSans.ttf&lt;/export&gt;\\n\\
    &lt;export&gt;ADAGUC\_LOGFILE=/src/log/adaguc-server.log&lt;/export&gt;\\n\\
    &lt;/adaguc-server&gt;\\n\\
    &lt;autowms&gt;\\n\\
    &lt;enabled&gt;true&lt;/enabled&gt;\\n\\
    &lt;autowmspath&gt;/data/adaguc-autowms/&lt;/autowmspath&gt;\\n\\
    &lt;datasetpath&gt;/data/adaguc-datasets/&lt;/datasetpath&gt;\\n\\
    &lt;/autowms&gt;\\n\\
    &lt;/adaguc-services&gt;" &gt;
    /src/config/adaguc-services-config-tomcat.xml

```

Install adaguc-viewer
---------------------

```
cd /src/apache-tomcat-8.0.44/webapps
git clone https://github.com/KNMI/adaguc-viewer/
printf "\\n\\
xml2jsonrequestURL = '/adaguc-services/xml2json?'\\n\\
autowmsURL = '/adaguc-services/autowms?';\\n\\
" &gt;&gt; adaguc-viewer/config.js
```

Install adaguc-server
---------------------

```
sudo mkdir -p /src/KNMI
sudo chown -R \$USER: /src
sudo mkdir -p /data/
sudo chown -R \$USER: /data
mkdir /data/adaguc-autowms
mkdir /data/adaguc-datasets
cd /src/KNMI
git clone https://github.com/KNMI/adaguc-server
cd /src/KNMI/adaguc-server
bash compile.sh
cp /src/KNMI/adaguc-server/data/datasets/testdata.nc
/data/adaguc-autowms/
cp /src/KNMI/adaguc-server/data/config/datasets/dataset\_a.xml
/data/adaguc-datasets/

```

Automate Start tomcat
---------------------

```
echo -e '\#!/bin/bash
t=\`ps -ef | grep apache-tomcat-8 | grep adaguc | grep -v grep\`
if \[ ! -z "\$t" -a "\$t" != " " \]; then
echo "Tomcat is running"
else
echo "Tomcat is not running, starting it"
. /src/apache-tomcat-8.0.44/setenv.sh
/src/apache-tomcat-8.0.44/bin/startup.sh
sleep 2
fi' &gt; /src/tomcatstarter.sh
chmod +x /src/tomcatstarter.sh
/src/tomcatstarter.sh

echo -e '@reboot /src/tomcatstarter.sh &gt; /dev/null 2&gt;&1' &gt;
/src/crontab
crontab /src/crontab

```

Check if it is working
----------------------

Visit for files in /data/adaguc-autowms:

-   http://localhost:8080/adaguc-viewer/?service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fservice%3Dwms%26request%3Dgetcapabilities%26source%3Dtestdata.nc
    Visit for datasets in /data/adaguc-datasets:
-   http://localhost:8080/adaguc-viewer/?service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fservice%3Dwms%26request%3Dgetcapabilities%26dataset%3Ddataset\_a

Update datasets
---------------

Dataset configurations [Dataset](Dataset.md) can be configured via path
/src/KNMI/adaguc-server/data/config/datasets. Data configured in these
dataset configurations need to be scanned via an updatedb command:

```

1.  Update of dataset
    /src/KNMI/adaguc-server/data/config/datasets/dataset\_a.xml
    export ADAGUC\_TMP=/tmp
    export ADAGUC\_PATH=/src/KNMI/adaguc-server/
    /src/KNMI/adaguc-server/bin/adagucserver --updatedb --config
    /src/KNMI/adaguc-server/data/config/adaguc.vm.xml,dataset\_a.xml

```

------------------------------------------------------------------------

**Please note:** The previous instructions for installing adaguc using
Apache CGI and PHP can be found here:
\[\[Install\_Adaguc\_on\_Ubuntu\_Old\]\]

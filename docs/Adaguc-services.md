Adaguc-services
===============

Adaguc-services is a spring boot application to run adaguc-server
without traditional Apache HTTP and CGI modules. It can run standalone
or it can be deployed within an existing apache tomcat server.
Adaguc-services will be the platform for easy deployable Web Processing
Services with a built in OpenDAP server and built in per user security
system compatible with the Earth System Grid Federation and
climate4impact.

-   Self supporting system
-   Provides WMS from a file system, based on NetCDF, HDF5, GeoJSON, PNG
-   Synchronizes automatically with data folder, auto update and
    cleaning
-   Dataset / product configuration is external: outside environment
-   Software stack can be containerized with Docker for easy deployment.
-   Aggregates logging to relevant and smaller log information

![](Adaguc-Services-WMS-Docker.png)

Repository
----------

https://github.com/KNMI/adaguc-services

Environment variables
---------------------

Configuration file is located at environment variable
ADAGUC\_SERVICES\_CONFIG
```
export
ADAGUC\_SERVICES\_CONFIG=/src/config/adaguc-services-config-tomcat.xml
```

Configuration file:
-------------------

The configuration file allows for environment variable substitution.
{ENV.ENVVARNAME} will be replaced with the environment variable
ENVVARNAME.

```
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;adaguc-services&gt;
&lt;external-home-url&gt;http://localhost:8080/adaguc-services/&lt;/external-home-url&gt;
&lt;basedir&gt;/data/adaguc-services-base&lt;/basedir&gt;
&lt;userworkspace&gt;/data/adaguc-services-space&lt;/userworkspace&gt;
&lt;server&gt;
&lt;port&gt;8080&lt;/port&gt;
&lt;/server&gt;
&lt;security&gt;
&lt;keystore&gt;/src/keystore.jks&lt;/keystore&gt;
&lt;keystorepassword&gt;password&lt;/keystorepassword&gt;
&lt;keystoretype&gt;JKS&lt;/keystoretype&gt;
&lt;keyalias&gt;tomcat&lt;/keyalias&gt;
&lt;/security&gt;
&lt;adaguc-server&gt;
&lt;adagucexecutable&gt;/src/KNMI/adaguc-server/bin/adagucserver&lt;/adagucexecutable&gt;
&lt;export&gt;ADAGUC\_PATH=/src/KNMI/adaguc-server/&lt;/export&gt;
&lt;export&gt;ADAGUC\_CONFIG=/src/KNMI/adaguc-server/data/config/adaguc.vm.xml&lt;/export&gt;
&lt;export&gt;ADAGUC\_DATARESTRICTION=FALSE&lt;/export&gt;
&lt;export&gt;ADAGUC\_FONT=/src/KNMI/adaguc-server/data/fonts/FreeSans.ttf&lt;/export&gt;
&lt;export&gt;ADAGUC\_LOGFILE=/src/log/adaguc-server.log&lt;/export&gt;
&lt;/adaguc-server&gt;
&lt;autowms&gt;
&lt;enabled&gt;true&lt;/enabled&gt;
&lt;autowmspath&gt;/data/adaguc-autowms/&lt;/autowmspath&gt;
&lt;datasetpath&gt;/data/adaguc-datasets/&lt;/datasetpath&gt;
&lt;/autowms&gt;
&lt;/adaguc-services&gt;
```

With PyWPS:
-----------

When using PyWPS, best is to run adaguc-services as a spring boot
application, e.g. without tomcat. This enables by default the Java Key
Store for runing the services over HTTPS, including two way SSL / x509
client authentication.

-   Build with mvn package
-   Start this with java -jar &lt;nameofbuiltpackage&gt;.jar
-   Configure with:

```
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;adaguc-services&gt;

&lt;external-home-url&gt;https://compute-test.c3s-magic.eu:9000&lt;/external-home-url&gt;

&lt;basedir&gt;{ENV.HOME}/adaguc-services-base&lt;/basedir&gt;

&lt;userworkspace&gt;{ENV.HOME}/adaguc-services-space&lt;/userworkspace&gt;

&lt;server&gt;
&lt;port&gt;9000&lt;/port&gt;
&lt;/server&gt;

&lt;security&gt;
&lt;truststorepassword&gt;changeit&lt;/truststorepassword&gt;
&lt;truststore&gt;{ENV.HOME}/config/esg-truststore.ts&lt;/truststore&gt;
&lt;trustrootscadirectory&gt;{ENV.HOME}/.globus/certificates/&lt;/trustrootscadirectory&gt;
&lt;keystore&gt;{ENV.HOME}/impactportal/c4i\_keystore.jks&lt;/keystore&gt;
&lt;keystorepassword&gt;password&lt;/keystorepassword&gt;
&lt;keystoretype&gt;JKS&lt;/keystoretype&gt;
&lt;keyalias&gt;tomcat&lt;/keyalias&gt;
&lt;/security&gt;

&lt;adaguc-server&gt;
&lt;adagucexecutable&gt;{ENV.HOME}/src/adaguc-server/bin/adagucserver&lt;/adagucexecutable&gt;
&lt;export&gt;ADAGUC\_PATH={ENV.HOME}/src/adaguc-server/&lt;/export&gt;
&lt;export&gt;ADAGUC\_CONFIG={ENV.HOME}/src/adaguc-server/data/config/adaguc.docker.xml&lt;/export&gt;
&lt;export&gt;ADAGUC\_DATARESTRICTION=FALSE&lt;/export&gt;
&lt;export&gt;ADAGUC\_LOGFILE={ENV.HOME}/adaguc-services-tmp/adaguc.autoresource.log&lt;/export&gt;
&lt;export&gt;ADAGUC\_FONT={ENV.HOME}/src/adaguc-server/data/fonts/FreeSans.ttf&lt;/export&gt;
&lt;/adaguc-server&gt;

&lt;pywps-server&gt;
&lt;pywpsexecutable&gt;{ENV.HOME}/src/pywps-pywps-3.2.5/wps.py&lt;/pywpsexecutable&gt;
&lt;pywpsconfigtemplate&gt;{ENV.HOME}/impactportal/pywps.cfg&lt;/pywpsconfigtemplate&gt;
&lt;pywpsoutputdir&gt;{ENV.HOME}/wpsoutputs&lt;/pywpsoutputdir&gt;
&lt;pywpsprocessesdir&gt;{ENV.HOME}/wpsprocesses/impactwps&lt;/pywpsprocessesdir&gt;
&lt;tmp&gt;{ENV.HOME}/adaguc-services-tmp&lt;/tmp&gt;
&lt;export&gt;ADAGUC\_CONFIG={ENV.HOME}/impactportal/adagucserver.xml&lt;/export&gt;
&lt;export&gt;ADAGUC\_PATH={ENV.HOME}/src/adagucserver/&lt;/export&gt;
&lt;export&gt;ADAGUC\_TMP={ENV.HOME}/adaguc-services-tmp/&lt;/export&gt;
&lt;export&gt;ADAGUC\_LOGFILE={ENV.HOME}/adaguc-services-tmp/adagucserver-wps.log&lt;/export&gt;
&lt;export&gt;ADAGUC\_DATARESTRICTION=FALSE&lt;/export&gt;
&lt;!-~~&lt;export&gt;PATH={ENV.HOME}/src/adagucserver/bin/:{ENV.HOME}/conda/bin/:{ENV.HOME}/conda/bin/:{ENV.HOME}/conda/bin/:{ENV.HOME}/bin:{ENV.HOME}/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin&lt;/export&gt;-~~&gt;
&lt;!-~~&lt;export&gt;PATH=/home/c3smagic/code/KNMI/wps\_prov/climexp:/home/c3smagic/code/KNMI/adagucserver/bin/:/home/c3smagic/conda/bin/:/home/c3smagic/conda/bin/:/home/c3smagic/conda/bin/:/home/c3smagic/bin:/home/c3smagic/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin&lt;/export&gt;-~~&gt;
&lt;export&gt;PATH=/home/c3smagic/code/maartenplieger/adaguc-server/bin/:{ENV.HOME}/conda/bin/:{ENV.HOME}/conda/bin/:{ENV.HOME}/conda/bin/:{ENV.HOME}/bin:{ENV.HOME}/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin&lt;/export&gt;
&lt;export&gt;PYWPS\_TEMPLATES={ENV.HOME}/src/pywps-pywps-3.2.5/pywps/Templates&lt;/export&gt;
&lt;export&gt;PORTAL\_OUTPUT\_PATH={ENV.HOME}/wpsoutputs/&lt;/export&gt;
&lt;export&gt;USE\_FONTCONFIG=False&lt;/export&gt;
&lt;/pywps-server&gt;

&lt;/adaguc-services&gt;

```

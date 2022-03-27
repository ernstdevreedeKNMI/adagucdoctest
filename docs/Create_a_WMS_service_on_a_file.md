Create a WMS service on a file
==============================

The best way to create a new ADAGUC service is by using a template of an
existing configuration file. You can adjust the configuration to match
the requirements for the new service.

Prerequisites
-------------

-   ADAGUC server
-   Postgres database

There are three things to adjust or update when creating a new service,
1) files, 2) configuration and 3) the database.

1\) Files:

-   Create a new XML configuration file, based on an existing template,
    e.g. /data/services/config/newservice.xml
-   Create a new CGI file, and adjust it to point to the configuration
    file, e.g. /data/www/cgi-bin/demo/newservice.cgi

Make sure that the cgi is executable, if not you can use chmod +x
/data/www/cgi-bin/demo/newservice.cgi

2\) Configuration items: (see [Configuration](Configuration.md))

-   OnlineResource - Let the onlineresource point to the location where
    the service is accessible from the net. Don't forget the '?' token
    on the end of the URL.
-   Title and Abstract of the service
-   Layer-~~&gt;FilePath~~ Change or create a new layer pointing to the
    data you would like to visualize
-   Layer-~~&gt;Variable~~ Choose the variable you want to visualize

3\) Update the database:
```
/data/software/adagucserver/bin/adagucserver --updatedb --config
/data/services/config/newservice.xml
```

If no errors are given, you can check the new service by requesting it's
getcapabilities document:

http://localhost/cgi-bin/demo/newservice.cgi?service=wms&amp;request=getcapabilities

You can also import the URL
http://localhost/cgi-bin/demo/newservice.cgi? via 'Add data' into the
viewer to view the service.

CGI Template to use for new files:
```
\#!/bin/bash

export LD\_LIBRARY\_PATH=/data/build/lib/:\$LD\_LIBRARY\_PATH
export PROJ\_LIB=/data/build/share/proj/
export ADAGUC\_CONFIG=/data/services/config/config.xml
export ADAGUC\_LOGFILE=data/log/server.log
export ADAGUC\_ERRORFILE=/data/log/server.errlog
export ADAGUC\_FONT=/data/fonts/FreeSans.ttf
export ADAGUC\_DATARESTRICTION="FALSE"

/data/build/bin/adagucserver
```

XML Template to use when creating new services:
```

&lt;?xml version="1.0" encoding="UTF-8" ?&gt;
&lt;Configuration&gt;

&lt;!-- General settings --&gt;
&lt;Path value="/data/software/adagucserver/data"/&gt;
&lt;TempDir value="/data/tmp/"/&gt;
&lt;OnlineResource
value="http://localhost/cgi-bin/demo/newservice.cgi?"/&gt;
&lt;DataBase parameters="dbname=adagucdemo host=127.0.0.1 user=adaguc
password=adaguc"/&gt;

&lt;!-- WMS settings --&gt;
&lt;WMS&gt;
&lt;Title&gt;NewService&lt;/Title&gt;
&lt;Abstract&gt;This service demonstrates how the ADAGUC server can be
used to create OGC services.&lt;/Abstract&gt;
&lt;RootLayer&gt;
&lt;Title&gt;ADAGUC NewService&lt;/Title&gt;
&lt;Abstract&gt;&lt;/Abstract&gt;
&lt;/RootLayer&gt;
&lt;TitleFont
location="/data/software/adagucserver/data/fonts/FreeSans.ttf"
size="19"/&gt;
&lt;SubTitleFont
location="/data/software/adagucserver/data/fonts/FreeSans.ttf"
size="10"/&gt;
&lt;DimensionFont
location="/data/software/adagucserver/data/fonts/FreeSans.ttf"
size="7"/&gt;
&lt;ContourFont
location="/data/software/adagucserver/data/fonts/FreeSans.ttf"
size="7"/&gt;
&lt;GridFont
location="/data/software/adagucserver/data/fonts/FreeSans.ttf"
size="5"/&gt;
&lt;WMSFormat name="image/png" format="image/png"/&gt;
&lt;/WMS&gt;

&lt;!-- WCS settings --&gt;
&lt;WCS&gt;
&lt;Title&gt;BTD\_DATA&lt;/Title&gt;
&lt;Label&gt;wcsLabel&lt;/Label&gt;
&lt;WCSFormat name="netcdf" driver="NetCDF"
mimetype="Content-Type:application/netcdf"
options="WRITE\_GDAL\_TAGS=FALSE,WRITE\_LONLAT=FALSE,WRITE\_BOTTOMUP=FALSE,ZLEVEL=2,FORMAT=NC4C"/&gt;
&lt;WCSFormat name="aaigrid" driver="AAIGrid"
mimetype="Content-Type:text/plain" /&gt;
&lt;WCSFormat name="geotiff" driver="GTiff"
mimetype="Content-Type:text/plain" /&gt;

&lt;/WCS&gt;

&lt;!-- Projections --&gt;
&lt;Projection id="EPSG:3411" proj4="+proj=stere +lat\_0=90 +lat\_ts=70
+lon\_0=-45 +k=1 +x\_0=0 +y\_0=0 +a=6378273 +b=6356889.449 +units=m
+no\_defs"/&gt;
&lt;Projection id="EPSG:3412" proj4="+proj=stere +lat\_0=-90
+lat\_ts=-70 +lon\_0=0 +k=1 +x\_0=0 +y\_0=0 +a=6378273 +b=6356889.449
+units=m +no\_defs"/&gt;
&lt;Projection id="EPSG:3575" proj4="+proj=laea +lat\_0=90 +lon\_0=10
+x\_0=0 +y\_0=0 +ellps=WGS84 +datum=WGS84 +units=m +no\_defs"/&gt;

&lt;Projection id="EPSG:3857" proj4="+proj=merc +a=6378137 +b=6378137
+lat\_ts=0.0 +lon\_0=0.0 +x\_0=0.0 +y\_0=0 +k=1.0 +units=m
+nadgrids=`null +wktext  +no_defs"/&gt;
  &lt;Projection id="EPSG:4258" proj4="+proj=longlat +ellps=GRS80 +no_defs"/&gt;
  &lt;Projection id="EPSG:4326" proj4="+proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs"/&gt;
  &lt;Projection id="CRS:84" proj4="+proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs"/&gt;
  &lt;Projection id="EPSG:25831" proj4="+proj=utm +zone=31 +ellps=GRS80 +units=m +no_defs"/&gt;
  &lt;Projection id="EPSG:25832" proj4="+proj=utm +zone=32 +ellps=GRS80 +units=m +no_defs"/&gt;
  &lt;Projection id="EPSG:28992" proj4="+proj=sterea +lat_0=52.15616055555555 +lon_0=5.38763888888889 +k=0.9999079 +x_0=155000 +y_0=463000 +ellps=bessel +towgs84=565.4171,50.3319,465.5524,-0.398957388243134,0.343987817378283,-1.87740163998045,4.0725 +units=m +no_defs"&gt;
  &lt;/Projection&gt;
  &lt;Projection id="EPSG:7399" proj4="+proj=moll +lon_0=0 +x_0=0 +y_0=0 +ellps=WGS84 +units=m +no_defs "/&gt;
  &lt;Projection id="EPSG:50001" proj4="+proj=stere +lat_ts=60.0 +lat_0=90 +lon_0=-111.0 +k_0=1.0 +x_0=3020946.0 +y_0=7622187.0 +units=m +ellps=WGS84 +datum=WGS84 +no_defs "&gt;
    &lt;LatLonBox minx="-2000000"  miny="-2000000" maxx="10000000" maxy="8500000"/&gt;
  &lt;/Projection&gt;
  &lt;Projection id="EPSG:54030" proj4="+proj=robin +lon_0=0 +x_0=0 +y_0=0 +ellps=WGS84 +datum=WGS84 +units=m +no_defs "/&gt;
  &lt;Projection id="EPSG:32661" proj4="+proj=stere +lat_0=90 +lat_ts=90 +lon_0=0 +k=0.994 +x_0=2000000 +y_0=2000000 +ellps=WGS84 +datum=WGS84 +units=m +no_defs"/&gt;
  &lt;Projection id="EPSG:40000" proj4="+proj=stere +ellps=WGS84 +lat_0=90 +lon_0=0 +no_defs"/&gt;
  &lt;Projection id="EPSG:900913" proj4=" +proj=merc +a=6378137 +b=6378137 +lat_ts=0.0 +lon_0=0.0 +x_0=0.0 +y_0=0 +k=1.0 +units=m +nadgrids=`null
+no\_defs"/&gt;

&lt;!-~~Legends -~~&gt;
&lt;Legend name="multicolor" type="colorRange"&gt;
&lt;palette index="000" red="143" green="133" blue="186"/&gt;
&lt;palette index="006" red="079" green="072" blue="149"/&gt;
&lt;palette index="012" red="000" green="057" blue="128"/&gt;
&lt;palette index="018" red="000" green="084" blue="157"/&gt;
&lt;palette index="024" red="000" green="112" blue="184"/&gt;
&lt;palette index="030" red="000" green="139" blue="208"/&gt;
&lt;palette index="036" red="000" green="158" blue="205"/&gt;
&lt;palette index="042" red="001" green="168" blue="186"/&gt;
&lt;palette index="048" red="045" green="183" blue="185"/&gt;
&lt;palette index="054" red="000" green="153" blue="161"/&gt;
&lt;palette index="060" red="000" green="125" blue="143"/&gt;
&lt;palette index="066" red="000" green="113" blue="109"/&gt;
&lt;palette index="072" red="001" green="089" blue="047"/&gt;
&lt;palette index="078" red="000" green="109" blue="051"/&gt;
&lt;palette index="084" red="040" green="154" blue="067"/&gt;
&lt;palette index="090" red="118" green="184" blue="086"/&gt;
&lt;palette index="096" red="149" green="195" blue="107"/&gt;
&lt;palette index="102" red="175" green="203" blue="082"/&gt;
&lt;palette index="108" red="197" green="213" blue="080"/&gt;
&lt;palette index="120" red="222" green="219" blue="000"/&gt;
&lt;palette index="126" red="241" green="229" blue="031"/&gt;
&lt;palette index="132" red="255" green="240" blue="063"/&gt;
&lt;palette index="138" red="255" green="244" blue="129"/&gt;
&lt;palette index="144" red="255" green="246" blue="177"/&gt;
&lt;palette index="150" red="255" green="241" blue="196"/&gt;
&lt;palette index="156" red="255" green="231" blue="171"/&gt;
&lt;palette index="162" red="253" green="213" blue="144"/&gt;
&lt;palette index="168" red="250" green="193" blue="114"/&gt;
&lt;palette index="174" red="247" green="170" blue="066"/&gt;
&lt;palette index="180" red="239" green="127" blue="001"/&gt;
&lt;palette index="186" red="235" green="105" blue="009"/&gt;
&lt;palette index="192" red="232" green="079" blue="019"/&gt;
&lt;palette index="198" red="228" green="046" blue="024"/&gt;
&lt;palette index="204" red="227" green="000" blue="027"/&gt;
&lt;palette index="210" red="209" green="000" blue="024"/&gt;
&lt;palette index="216" red="189" green="010" blue="029"/&gt;
&lt;palette index="222" red="152" green="027" blue="033"/&gt;
&lt;palette index="228" red="102" green="038" blue="036"/&gt;
&lt;palette index="234" red="080" green="041" blue="036"/&gt;
&lt;palette index="240" red="080" green="041" blue="036"/&gt;
&lt;/Legend&gt;

&lt;Legend name="rainbow" type="colorRange"&gt;
&lt;palette index="0" red="0" green="0" blue="255"/&gt;
&lt;palette index="80" red="0" green="255" blue="255"/&gt;
&lt;palette index="120" red="0" green="255" blue="0"/&gt;
&lt;palette index="160" red="255" green="255" blue="0"/&gt;
&lt;palette index="240" red="255" green="0" blue="0"/&gt;
&lt;/Legend&gt;

&lt;Legend name="no2" type="colorRange"&gt;
&lt;palette index="0" red="0" green="0" blue="190"/&gt;
&lt;palette index="5" red="0" green="0" blue="255"/&gt;
&lt;palette index="17" red="0" green="255" blue="255"/&gt;
&lt;palette index="40" red="0" green="255" blue="0"/&gt;
&lt;palette index="81" red="255" green="255" blue="0"/&gt;
&lt;palette index="156" red="255" green="0" blue="0"/&gt;
&lt;palette index="190" red="255" green="0" blue="160"/&gt;
&lt;palette index="240" red="255" green="0" blue="160"/&gt;
&lt;/Legend&gt;

&lt;!-- Style configuration --&gt;
&lt;Style name="rainbow"&gt;
&lt;Legend fixedclasses="true" tickinterval="500"
tickround="1"&gt;rainbow&lt;/Legend&gt;
&lt;Min&gt;0.0&lt;/Min&gt;
&lt;Max&gt;3500&lt;/Max&gt;
&lt;NameMapping name="nearest" title="Rainbow colors" abstract="Drawing
images with rainbow colors"/&gt;
&lt;/Style&gt;
&lt;Style name="no2"&gt;
&lt;Legend fixedclasses="true" tickinterval="500"
tickround="1"&gt;no2&lt;/Legend&gt;
&lt;Min&gt;0.0&lt;/Min&gt;
&lt;Max&gt;3500&lt;/Max&gt;
&lt;RenderMethod&gt;nearest,bilinear&lt;/RenderMethod&gt;
&lt;NameMapping name="nearest" title="NO2 colors" abstract="Drawing
images with NO2 colors"/&gt;
&lt;NameMapping name="bilinear" title="NO2 colors smooth"
abstract="Drawing images with NO2 colors and bilinear
interpolation"/&gt;
&lt;/Style&gt;

&lt;!-- Layer configuration --&gt;
&lt;Layer type="database"&gt;
&lt;FilePath
filter=""&gt;/data/services/data/myfile.nc&lt;/FilePath&gt;
&lt;Variable&gt;var&lt;/Variable&gt;
&lt;Styles&gt;rainbow&lt;/Styles&gt;
&lt;/Layer&gt;

&lt;!-- End of configuration /--&gt;
&lt;/Configuration&gt;

```

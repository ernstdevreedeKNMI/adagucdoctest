Create a WMS service with multiple layers
=========================================

You can add new layers to your WMS service by adding more [Layer](Layer.md)
elements. For example:

```

&lt;?xml version="1.0" encoding="UTF-8" ?&gt;
&lt;Configuration&gt;

&lt;!-- General settings --&gt;
&lt;Path value="/data/software/adagucserver/data"/&gt;
&lt;TempDir value="/data/tmp/"/&gt;
&lt;OnlineResource
value="http://localhost/cgi-bin/demo/pytroll.cgi?"/&gt;
&lt;DataBase parameters="dbname=adagucdemo host=127.0.0.1 user=adaguc
password=adaguc"/&gt;

&lt;!-- WMS settings --&gt;
&lt;WMS&gt;
&lt;Title&gt;OMI\_Pytroll\_DEMO\_SERVICE&lt;/Title&gt;
&lt;Abstract&gt;This service demonstrates how the ADAGUC server can be
used to create OGC services.&lt;/Abstract&gt;
&lt;RootLayer&gt;
&lt;Title&gt;ADAGUC Pytroll Demo Service&lt;/Title&gt;
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
&lt;Title&gt;DEMO\_SERVICE&lt;/Title&gt;
&lt;Label&gt;wcsLabel&lt;/Label&gt;
&lt;WCSFormat name="NetCDF3" driver="ADAGUC"
mimetype="Content-Type:text/plain" options="FORCENC3=TRUE"/&gt;
&lt;WCSFormat name="NetCDF4" driver="ADAGUC"
mimetype="Content-Type:text/plain"/&gt;
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
  &lt;Projection id="EPSG:4258"   proj4="+proj=longlat +ellps=GRS80 +no_defs"/&gt;
  &lt;Projection id="EPSG:4326"   proj4="+proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs"/&gt;
  &lt;Projection id="EPSG:25831"  proj4="+proj=utm +zone=31 +ellps=GRS80 +units=m +no_defs"/&gt;
  &lt;Projection id="EPSG:25832"  proj4="+proj=utm +zone=32 +ellps=GRS80 +units=m +no_defs"/&gt;
  &lt;Projection id="EPSG:28992"  proj4="+proj=sterea +lat_0=52.15616055555555 +lon_0=5.38763888888889 +k=0.9999079 +x_0=155000 +y_0=463000 +ellps=bessel +units=m +no_defs"/&gt;
  &lt;Projection id="EPSG:32661"  proj4="+proj=stere +lat_0=90 +lat_ts=90 +lon_0=0 +k=0.994 +x_0=2000000 +y_0=2000000 +ellps=WGS84 +datum=WGS84 +units=m +no_defs"/&gt;
  &lt;Projection id="EPSG:40000"  proj4="+proj=stere +ellps=WGS84 +lat_0=90 +lon_0=0 +no_defs"/&gt;
  &lt;Projection id="EPSG:900913" proj4=" +proj=merc +a=6378137 +b=6378137 +lat_ts=0.0 +lon_0=0.0 +x_0=0.0 +y_0=0 +k=1.0 +units=m +nadgrids=`null
+no\_defs"/&gt;
&lt;Projection id="EPSG:102100" proj4="+proj=merc +a=6378137 +b=6378137
+lat\_ts=0.0 +lon\_0=0.0 +x\_0=0.0 +y\_0=0 +k=1.0 +units=m
+nadgrids=@null +wktext +no\_defs"/&gt;

&lt;!-~~Legends -~~&gt;

&lt;Legend name="rainbow" type="colorRange"&gt;
&lt;palette index="0" red="0" green="0" blue="255"/&gt;
&lt;palette index="80" red="0" green="255" blue="255"/&gt;
&lt;palette index="120" red="0" green="255" blue="0"/&gt;
&lt;palette index="160" red="255" green="255" blue="0"/&gt;
&lt;palette index="240" red="255" green="0" blue="0"/&gt;
&lt;/Legend&gt;
&lt;!-- Auto style --&gt;
&lt;Style name="auto"&gt;
&lt;Legend&gt;rainbow&lt;/Legend&gt;
&lt;Scale&gt;0&lt;/Scale&gt;
&lt;Offset&gt;0&lt;/Offset&gt;
&lt;RenderMethod&gt;nearest,bilinear,nearestpoint&lt;/RenderMethod&gt;
&lt;/Style&gt;

&lt;!-- Layer configuration --&gt;
&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;overview&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;airmass&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;ash&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;cloudtop&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;convection&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;dust&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;green\_snow&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;natural&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;night\_fog&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="MSG\_RGB\_EuropeCanary"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/services/data/pytroll/MSG\_RGB\_EuropeCanary/&lt;/FilePath&gt;
&lt;Variable&gt;red\_snow&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="noaa"/&gt;
&lt;Name&gt;overview\_neur&lt;/Name&gt;
&lt;Title&gt;Overview Northern Europe&lt;/Title&gt;
&lt;FilePath&gt;/data/services/data/pytroll/noaa/NOAA19\_RGB\_20121127\_0959\_NEur.nc&lt;/FilePath&gt;
&lt;Variable&gt;overview&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="noaa"/&gt;
&lt;Name&gt;overview\_moll&lt;/Name&gt;
&lt;Title&gt;Overview Mollweide&lt;/Title&gt;
&lt;FilePath&gt;/data/services/data/pytroll/noaa/NOAA19\_RGB\_20121127\_0959\_moll.nc&lt;/FilePath&gt;
&lt;Variable&gt;overview&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Group value="npp"/&gt;
&lt;Name&gt;overview\_moll&lt;/Name&gt;
&lt;Title&gt;Overview Mollweide&lt;/Title&gt;
&lt;FilePath&gt;/data/services/data/pytroll/npp/NPP\_RGB\_20121125\_1046\_moll.nc&lt;/FilePath&gt;
&lt;Variable&gt;overview&lt;/Variable&gt;
&lt;RenderMethod&gt;rgba&lt;/RenderMethod&gt;
&lt;/Layer&gt;

&lt;!-- End of configuration /--&gt;

&lt;/Configuration&gt;

```

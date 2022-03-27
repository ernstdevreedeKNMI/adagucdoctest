Pointtimeseries example
=======================

NetCDF files using this structure can be found here:
http://opendap.knmi.nl/knmi/thredds/catalog/ADAGUC/testsets/pointtimeseries/catalog.html

The following examples can be found on this page:

-   1\) 10000 random points - no time dimension
-   2\) Point timeseries NetCDF - Automated weather station observations
-   3\) Random observations with a timestamp (earthquakes)
-   4\) Random events fixed in timeslots (lightning)
-   5\) TODO symbols

1) 10000 random points - no time dimension
------------------------------------------

This example demonstrates how a file with 10000 points can be created
and displayed in ADAGUC.

![](https://dev.knmi.nl/attachments/660/10000_random_points.jpg)

The NetCDF file should have the following structure:
```
netcdf points\_10000\_random {
dimensions:
numpoints = 10000 ;
variables:
double lat(numpoints) ;
lat:units = "degrees\_north" ;
lat:standard\_name = "latitude" ;
double lon(numpoints) ;
lon:units = "degrees\_east" ;
lon:standard\_name = "longitude" ;
double percent(numpoints) ;
percent:units = "percentage" ;
percent:standard\_name = "percent" ;

// global attributes:
:featureType = "point" ;
:Conventions = "CF-1.4" ;
}
```

The ADAGUC configuration for the Layer object looks like this:

```

&lt;Legend name="bluewhitered" type="colorRange"&gt;
&lt;palette index="0" red="0" green="60" blue="123"/&gt;
&lt;palette index="30" red="0" green="100" blue="140"/&gt;
&lt;palette index="60" red="8" green="130" blue="206"/&gt;
&lt;palette index="85" red="132" green="211" blue="255"/&gt;
&lt;palette index="120" red="247" green="247" blue="247"/&gt;
&lt;palette index="155" red="255" green="195" blue="57"/&gt;
&lt;palette index="180" red="232" green="28" blue="0"/&gt;
&lt;palette index="210" red="165" green="0" blue="0"/&gt;
&lt;palette index="240" red="90" green="0" blue="0"/&gt;
&lt;/Legend&gt;

&lt;Style name="randompoint1"&gt;
&lt;Legend fixed="true" tickinterval="10"&gt;bluewithred&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;100&lt;/Max&gt;
&lt;NameMapping name="point" title="Points" abstract="Points"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="8"
textradius="0" dot="true" fontsize="14" textcolor="\#FFFFFF"
textformat=" "/&gt;
&lt;/Style&gt;

&lt;Layer type="database"&gt;
&lt;Group value="tests"/&gt;
&lt;Title&gt;10000 random points!&lt;/Title&gt;
&lt;FilePath
filter="\^.\*\\.nc\$"&gt;/data/services/data/testsets/pointtimeseries/points\_10000\_random.nc&lt;/FilePath&gt;
&lt;Variable&gt;percent&lt;/Variable&gt;
&lt;Styles&gt;randompoint1&lt;/Styles&gt;
&lt;/Layer&gt;
```

2) Point timeseries NetCDF - Automated weather station observations
-------------------------------------------------------------------

This file contains observations over time for several stations, this is
usually used to store observations from fixed automated weather stations
over time.

![](https://dev.knmi.nl/attachments/661/KIS_TG_ADAGUC.jpg)

The data for each parameter is organised as a table with a station and a
time dimension.
```
netcdf KIS*OPER\_POBS*\_L2 {
dimensions:
station = 149 ;
time = 23538 ;
variables:
string station(station) ;
station:long\_name = "station name" ;
station:cf\_role = "timeseries\_id" ;
double time(time) ;
time:long\_name = "time of measurement" ;
time:standard\_name = "time" ;
time:units = "seconds since 1950-01-01 00:00:00" ;
double lat(station) ;
lat:long\_name = "station latitude" ;
lat:standard\_name = "latitude" ;
lat:units = "degrees\_north" ;
double lon(station) ;
lon:long\_name = "station longitude" ;
lon:standard\_name = "longitude" ;
lon:units = "degrees\_east" ;
short TG (station, time) ;
TG:coordinates = "lat lon" ;
TG:kisid = "TG" ;
TG:description = "Daily mean temperature in (0.1 degrees Celsius);" ;
TG:\_FillValue = -9999s ;
TG:standard\_name = "air\_temperature" ;
TG:units = "degrees Celsius" ;
TG:long\_name = "Temperature" ;
TG:scale\_factor = 0.1f ;
TG:add\_offset = 0.f ;
char projection ;
projection:EPSG\_code = "EPSG:4326" ;

// global attributes:
:featureType = "timeSeries" ;
:Conventions = "CF-1.4" ;
:title = "KIS*OPER\_POBS*\_L2" ;
:institution = "Royal Netherlands Meteorological Institute (KNMI)" ;
:source = "Royal Netherlands Meteorological Institute (KNMI)" ;
:history = "File created from KIS ASCII file. " ;
:references = "http://data.knmi.nl" ;
:comment = "none" ;
}

```

The ADAGUC configuration looks like this:
```
&lt;Legend name="temperature" type="interval"&gt;
&lt;palette index="0" color="\#2E2E73"/&gt; &lt;!-- ~~14 -~~&gt;
&lt;palette index="9" color="\#282898"/&gt; &lt;!-- ~~12 -~~&gt;
&lt;palette index="18" color="\#201FBB"/&gt; &lt;!-- ~~10 -~~&gt;
&lt;palette index="27" color="\#1A1ADC"/&gt; &lt;!-- ~~8 -~~&gt;
&lt;palette index="36" color="\#3654DE"/&gt; &lt;!-- ~~6 -~~&gt;
&lt;palette index="45" color="\#548EDC"/&gt; &lt;!-- ~~4 -~~&gt;
&lt;palette index="54" color="\#72CADE"/&gt; &lt;!-- ~~2 -~~&gt;
&lt;palette index="63" color="\#6DD8DF"/&gt; &lt;!-- 0--&gt;
&lt;palette index="72" color="\#55CDE2"/&gt; &lt;!-- 2--&gt;
&lt;palette index="81" color="\#38BBDC"/&gt; &lt;!-- 4 --&gt;
&lt;palette index="90" color="\#20B0DC"/&gt; &lt;!-- 6 --&gt;
&lt;palette index="99" color="\#19BAA6"/&gt; &lt;!-- 8 --&gt;
&lt;palette index="108" color="\#1CCE6A"/&gt; &lt;!-- 10 --&gt;
&lt;palette index="117" color="\#1BDF22"/&gt; &lt;!-- 12 --&gt;
&lt;palette index="126" color="\#82C319"/&gt; &lt;!-- 14 --&gt;
&lt;palette index="135" color="\#DCA819"/&gt; &lt;!-- 16 --&gt;
&lt;palette index="144" color="\#DD921A"/&gt; &lt;!-- 18 --&gt;
&lt;palette index="153" color="\#DE7C1A"/&gt; &lt;!-- 20 --&gt;
&lt;palette index="162" color="\#DF671A"/&gt; &lt;!-- 22 --&gt;
&lt;palette index="171" color="\#DE501A"/&gt; &lt;!-- 24 --&gt;
&lt;palette index="180" color="\#DD3819"/&gt; &lt;!-- 26 --&gt;
&lt;palette index="189" color="\#DD2319"/&gt; &lt;!-- 28 --&gt;
&lt;palette index="198" color="\#D21A1E"/&gt; &lt;!-- 30 --&gt;
&lt;palette index="207" color="\#C31927"/&gt; &lt;!-- 32 --&gt;
&lt;palette index="216" color="\#AD1A30"/&gt; &lt;!-- 34 --&gt;
&lt;palette index="225" color="\#9A1A3B"/&gt; &lt;!-- 36 --&gt;
&lt;palette index="234" color="\#871A44"/&gt; &lt;!-- 38 --&gt;
&lt;palette index="240" color="\#871A44"/&gt; &lt;!-- 39,33 --&gt;
&lt;/Legend&gt;

&lt;Style name="temperature"&gt;
&lt;Legend fixed="true" tickinterval="2"&gt;temperature&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;-14&lt;/Min&gt;
&lt;Max&gt;39,33333333&lt;/Max&gt; &lt;!-- 39,33333333 = (240 / (234/(38
- ~~14)))~~ 14 --&gt;
&lt;NameMapping name="point" title="Temperature"
abstract="Temperature"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="15"
textradius="0" dot="false" fontsize="8" textcolor="\#000000" /&gt;
&lt;/Style&gt;

&lt;Layer type="database"&gt;
&lt;Group value="KNMI Daily Obs"/&gt;
&lt;FilePath
filter="\^.\*\\.nc\$"&gt;/data/services/data/testsets/pointtimeseries/KIS*OPER\_POBS*\_L2.nc&lt;/FilePath&gt;
&lt;Variable&gt;TG&lt;/Variable&gt;
&lt;Styles&gt;temperature&lt;/Styles&gt;
&lt;/Layer&gt;
```

3) Random observations with a timestamp (earthquakes)
-----------------------------------------------------

This file is characterized by random observations which occur over time.
This file has no time dimension, but has time attached to each
observation.

![](https://dev.knmi.nl/attachments/662/earthquakes_last_100_nl_adaguc.jpg)
```
netcdf EQ*OPER\_POBS*\_\_L2 {
dimensions:
obs = 100 ;
variables:
string location(obs) ;
location:long\_name = "Location name" ;
location:units = "string" ;
location:coordinates = "time lat lon depth" ;
string phase\_file(obs) ;
phase\_file:long\_name = "Phase file name" ;
phase\_file:units = "string" ;
phase\_file:coordinates = "time lat lon depth" ;
string type(obs) ;
type:long\_name = "Event type" ;
type:units = "string" ;
type:coordinates = "time lat lon depth" ;
double time(obs) ;
time:long\_name = "Time of measurement" ;
time:standard\_name = "time" ;
time:units = "days since 1970-01-01 00:00:00" ;
double lat(obs) ;
lat:long\_name = "Latitude of the observation" ;
lat:standard\_name = "latitude" ;
lat:units = "degrees\_north" ;
double lon(obs) ;
lon:long\_name = "Longitude of the observation" ;
lon:standard\_name = "longitude" ;
lon:units = "degrees\_east" ;
double depth(obs) ;
depth:long\_name = "Vertical distance below the surface" ;
depth:standard\_name = "height" ;
depth:units = "km" ;
depth:axis = "Z" ;
depth:positive = "down" ;
double magnitude(obs) ;
magnitude:long\_name = "Richter magnitude scale" ;
magnitude:standard\_name = "magnitude" ;
magnitude:units = "magnitude" ;
magnitude:coordinates = "time lat lon depth" ;
char projection ;
projection:EPSG\_code = "EPSG:4326" ;

// global attributes:
:featureType = "point" ;
:Conventions = "CF-1.4" ;
:title = "EQ*OPER\_POBS*\_\_L2" ;
:institution = "Royal Netherlands Meteorological Institute (KNMI)" ;
:source = "Royal Netherlands Meteorological Institute (KNMI)" ;
:history = "File created from last100.json JSON file. " ;
:references = "http://data.knmi.nl" ;
:comment = "none" ;
}

```

The configuration in ADAGUC looks like this:
```
&lt;Legend name="magnitude" type="colorRange"&gt;
&lt;palette index="0" color="\#55005550"/&gt; &lt;!-- 0 Nothing --&gt;
&lt;palette index="20" color="\#66009980"/&gt; &lt;!-- 1 Insignificant
--&gt;
&lt;palette index="40" color="\#0099FF80"/&gt; &lt;!-- 2 Low --&gt;
&lt;palette index="60" color="\#00CC99B0"/&gt; &lt;!-- 3 Minor --&gt;
&lt;palette index="80" color="\#99CC66B0"/&gt; &lt;!-- 4 Moderate
--&gt;
&lt;palette index="100" color="\#99FF33B0"/&gt; &lt;!-- 5 Intermediate
--&gt;
&lt;palette index="120" color="\#FFFF33B0"/&gt; &lt;!-- 6 Noteworthy
--&gt;
&lt;palette index="140" color="\#FFCC66C0"/&gt; &lt;!-- 7 High --&gt;
&lt;palette index="160" color="\#FF9966D0"/&gt; &lt;!-- 8 Far-reaching
--&gt;
&lt;palette index="180" color="\#FF3300E0"/&gt; &lt;!-- 9 Outstanding
--&gt;
&lt;palette index="200" color="\#CC0000FF"/&gt; &lt;!-- 10 Extraordinary
--&gt;
&lt;palette index="220" color="\#880000FF"/&gt; &lt;!-- 11 ! --&gt;
&lt;palette index="239" color="\#000000FF"/&gt; &lt;!-- 12 !! --&gt;
&lt;/Legend&gt;
&lt;Style name="magnitude"&gt;
&lt;Legend fixed="true" tickinterval="1"&gt;magnitude&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;12&lt;/Max&gt;
&lt;NameMapping name="point" title="Richter magnitude scale"
abstract="Wth continuous colors"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="20"
textradius="0" dot="false" fontsize="14" textcolor="\#FFFFFF"/&gt;
&lt;/Style&gt;

&lt;Layer type="database"&gt;
&lt;Group value="KNMI Earthquakes NL"/&gt;
&lt;FilePath
filter="\^.\*\\.nc\$"&gt;/data/services/data/testsets/pointtimeseries/EQ*OPER\_POBS*\_\_L2.nc&lt;/FilePath&gt;
&lt;Variable&gt;magnitude&lt;/Variable&gt;
&lt;Styles&gt;magnitude&lt;/Styles&gt;
&lt;/Layer&gt;

```

4) Random events fixed in timeslots (lightning)
-----------------------------------------------

This is an example on how a timeseries of lightning events can be
quantized in fixed timeslots. This enables for example the animated
display of multiple lightning detections over 5 minute time intervals.
This is achieved by creating netcdf files each containing a timeslot
with lightning events. The NetCDF files must have a time dimension of
length 1 and contains all events in that timeslot. An example of such a
dataset can be found here:
http://opendap.knmi.nl/knmi/thredds/catalog/ADAGUC/testsets/btdsensor/catalog.html

![](https://dev.knmi.nl/attachments/663/btd300_adaguc.jpg)

```
netcdf btd\_20150605T180000 {
dimensions:
obs = 5 ;
time = 1 ;
variables:
double lat(obs) ;
lat:units = "degrees\_north" ;
lat:standard\_name = "latitude" ;
double lon(obs) ;
lon:units = "degrees\_east" ;
lon:standard\_name = "longitude" ;
double time(time) ;
time:units = "seconds since 1970-01-01 00:00:00" ;
time:standard\_name = "time" ;
double warningindicator(obs, time) ;
warningindicator:units = "warningindicator" ;
warningindicator:standard\_name = "warningindicator" ;
double warningflag(obs, time) ;
warningflag:units = "warningflag" ;
warningflag:standard\_name = "warningflag" ;

// global attributes:
:featureType = "point" ;
:Conventions = "CF-1.4" ;
}
```

The ADAGUC configuration contains a layer with a Dimension definition,
this dimension has an interval of 5 minutes:

```

&lt;Style name="btd"&gt;
&lt;Legend fixed="true"&gt;bluewhitered&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;2&lt;/Max&gt;
&lt;Point discradius="5" textformat=" " dot="false"/&gt;
&lt;/Style&gt;

&lt;Layer type="database"&gt;
&lt;Group value="BTD300 test"/&gt;
&lt;Title&gt;BTD300 warning flag&lt;/Title&gt;
&lt;Variable&gt;warningflag&lt;/Variable&gt;
&lt;FilePath
filter="\^btd\_.\*\\.nc\$"&gt;/data/services/data/testsets/btdsensor/&lt;/FilePath&gt;
&lt;Dimension name="time" interval="PT5M"
default="min"&gt;time&lt;/Dimension&gt;
&lt;Styles&gt;btd&lt;/Styles&gt;
&lt;/Layer&gt;

```

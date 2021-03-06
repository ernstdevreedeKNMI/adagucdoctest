Datapostprocessors (algorithm, a, b, c, units, name, mode)
==========================================================

Data postprocessors modify the data inside the adagucserver before any
further operations are applied. The modified data can be visualized
using WMS and retrieved using WCS. DataPostprocessors can be for example
simple unit conversions from Kelvin to Celsius.

-   algorithm - The Datapostprocessor to choose, e.g. "ax+b"
-   a - Input value a
-   b - Input value b
-   c - Input value c
-   units - The new units of the data.
-   name - name attributes, function depending on the processor
-   mode - additional settings for the processor

Current data postprocessors:

1.  ax+b: Linear transformation ax+b - Suitable for unit conversions
2.  include\_layer: Include another layer into your layer as new
    dataobject
3.  datamask: Mask one variable with another variable with several
    options
4.  MSGCPP VISIBLE-mask - Display the visible part of the disk
5.  HIWC-mask: Thresholds for detection of “High Ice Water Content”
    according to HAIC case.
6.  addfeatures: Turn geographical features (areas) into a grid
7.  beaufort: do conversion of wind speeds in m/s or kts to Beaufort
    values
8.  toknots: do conversion of wind speeds in m/s to kts

New datapost processors can be implemented via
https://github.com/KNMI/adaguc-server/blob/master/adagucserverEC/CDataPostProcessor.h

1. ax+b: Linear transformation ax+b - Suitable for unit conversions
-------------------------------------------------------------------

Example to convert cloudcover fraction to octa:
```
&lt;DataPostProc algorithm="ax+b" a="8" b="0" units="octa"/&gt;
```

2. include\_layer: Include another layer into your layer as new dataobject
--------------------------------------------------------------------------

-   Available since adagucserver version 2.0.9

This processor includes another layer in your current layer. The
variables configured in the other layer are added to your new layer.
These are visible in the GetFeatureInfo and GetMetadata request. This is
for example useful if u and v vectors are in two separate files. This
processor allows you to combine them into one layer.
**Note:** The two layers do not need to have the same gridsize and
projection, the other layer will be transformed to fit into the new
layer. The grids will be made the same.

-   algorithm: should be set to "include\_layer"
-   name: the other configured layer you wish to include
-   mode: prepend or append, e.g. will the new layer be put in front of
    the current variables or after.

```
&lt;Layer&gt;
...
&lt;Name&gt;theotherlayer&lt;/Name&gt;
...
&lt;/Layer&gt;

&lt;Layer&gt;
...
&lt;Name&gt;combinedlayer&lt;/Name&gt;
&lt;DataPostProc algorithm="include\_layer" name="theotherlayer"
mode="prepend"/&gt;
...
&lt;/Layer&gt;
```

It is for example also possible to create a layer with 3 variables,
minimum, average and maximum temperature:
```
&lt;Layer type="database"&gt;
&lt;Name&gt;t2minlayer&lt;/Name&gt;
&lt;Title&gt;t2minlayer&lt;/Title&gt;
&lt;FilePath&gt;http://opendap.knmi.nl/knmi/thredds/dodsC/ADAGUC/testsets/projectedgrids/t2min.KNMI-2014.KNXT12.HCAST2.DD.nc.fixed.nc&lt;/FilePath&gt;
&lt;Variable&gt;t2min&lt;/Variable&gt;
&lt;Styles&gt;auto&lt;/Styles&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Name&gt;t2maxlayer&lt;/Name&gt;
&lt;Title&gt;t2maxlayer&lt;/Title&gt;
&lt;FilePath&gt;http://opendap.knmi.nl/knmi/thredds/dodsC/ADAGUC/testsets/projectedgrids/t2max.KNMI-2014.KNXT12.HCAST2.DD.nc.fixed.nc&lt;/FilePath&gt;
&lt;Variable&gt;t2max&lt;/Variable&gt;
&lt;Styles&gt;auto&lt;/Styles&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Name&gt;combinedlayer&lt;/Name&gt;
&lt;Title&gt;combinedlayer&lt;/Title&gt;
&lt;FilePath&gt;http://opendap.knmi.nl/knmi/thredds/dodsC/ADAGUC/testsets/projectedgrids/t2m.KNMI-2014.KNXT12.HCAST2.DD.nc.fixed.nc&lt;/FilePath&gt;
&lt;Variable&gt;t2m&lt;/Variable&gt;
&lt;Styles&gt;auto&lt;/Styles&gt;
&lt;Min&gt;250&lt;/Min&gt;
&lt;Max&gt;300&lt;/Max&gt;
&lt;DataPostProc algorithm="include\_layer" name="t2minlayer"
mode="prepend"/&gt;
&lt;DataPostProc algorithm="include\_layer" name="t2maxlayer"
mode="append"/&gt;
&lt;/Layer&gt;
```

A get featureinfo request will show the 3 values for a point:
```
Coordinates - (lon=5.25; lat=51.96)
Minimum 2-m Temperature (secondlayer)
- Minimum 2-m Temperature 279.701904 K
- 2-m Temperature 281.849213 K
- Maximum 2-m Temperature 284.590302 K
```

3. datamask: Mask one variable with another variable with several options
-------------------------------------------------------------------------

-   Available since adagucserver version 2.0.9

This datapostproc allows to mask a layer with two variables defined. The
first variable is the data and the second variable is the mask.

-   algorithm: should be set to "datamask"
-   a : the lower comparison value. All values higher or equal to a are
    included as mask
-   b : the upper comparison value. All values lower or equal to a are
    included as mask
    -   Mask is active when a&gt;=maskvalue and b&lt;=maskvalue.
-   mode : optional, the masking operation, can be
    -   if\_mask\_includes\_then\_nodata\_else\_data, fills in nodata,
        e.g. areas become transparent
    -   if\_mask\_excludes\_then\_nodata\_else\_data, fills in nodata,
        e.g. areas become transparent
    -   if\_mask\_includes\_then\_valuec\_else\_data, value c will be
        used
    -   if\_mask\_excludes\_then\_valuec\_else\_data, value c will be
        used
    -   if\_mask\_includes\_then\_mask\_else\_data, combines the sets
    -   if\_mask\_excludes\_then\_mask\_else\_data, combines the sets
-   c : optional, the value to write when mask applies
-   name : optional, the new long\_name of the mask
-   units : optional, the new units of the mask

Example usage:
```
&lt;DataPostProc algorithm="datamask" a="0" b="0" name="newmask"
units="newunits" c="0"
mode="if\_mask\_excludes\_then\_nodata\_else\_data"/&gt;
```

Two variables need to be defined in the layer. This can be done by
adding an extra &lt;Variable&gt;...varname..&lt;/Variable&gt; element in
the Layer config if the corresponding file has the two variables. If the
masking variable is in another file, it can be added by using the
datapostproc include\_layer. The example below uses two different files
with different grid to create a masked result.

### Study case: Only display temperature field where precipitation is zero

This example demonstrates how a temperature field can be masked by
precipitation. By using the include\_layer postproc first, the layer
gets two variables. The first variable is the temperature from the KNMI
next scenarios, the second variable is precipitation from EOBS gridded
observations. Both grids are very different and are regridded to the
grid as used by the temperature variable (e.g. the original variable
from this layer).

![](adaguc_masking_example.png)
Configuration which has been used to create image above:
```
&lt;Layer type="database"&gt;
&lt;Name&gt;temperature&lt;/Name&gt;
&lt;Title&gt;temperature&lt;/Title&gt;
&lt;FilePath&gt;http://opendap.knmi.nl/knmi/thredds/dodsC/ADAGUC/testsets/projectedgrids/t2m.KNMI-2014.KNXT12.HCAST2.DD.nc.fixed.nc&lt;/FilePath&gt;
&lt;Variable&gt;t2m&lt;/Variable&gt;
&lt;Styles&gt;auto&lt;/Styles&gt;
&lt;Min&gt;250&lt;/Min&gt;
&lt;Max&gt;300&lt;/Max&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Name&gt;precipitation&lt;/Name&gt;
&lt;Title&gt;precipitation&lt;/Title&gt;
&lt;FilePath&gt;http://opendap.knmi.nl/knmi/thredds/dodsC/e-obs\_0.25regular/rr\_0.25deg\_reg\_v15.0.nc&lt;/FilePath&gt;
&lt;Variable&gt;rr&lt;/Variable&gt;
&lt;Styles&gt;auto&lt;/Styles&gt;
&lt;/Layer&gt;

&lt;Layer type="database"&gt;
&lt;Name&gt;masked&lt;/Name&gt;
&lt;Title&gt;masked&lt;/Title&gt;
&lt;FilePath&gt;http://opendap.knmi.nl/knmi/thredds/dodsC/ADAGUC/testsets/projectedgrids/t2m.KNMI-2014.KNXT12.HCAST2.DD.nc.fixed.nc&lt;/FilePath&gt;
&lt;Variable&gt;t2m&lt;/Variable&gt;
&lt;Styles&gt;auto&lt;/Styles&gt;
&lt;Min&gt;250&lt;/Min&gt;
&lt;Max&gt;300&lt;/Max&gt;
&lt;DataPostProc algorithm="include\_layer" name="precipitation"
mode="append"/&gt;
&lt;DataPostProc algorithm="datamask" a="0" b="0" name="newmask"
units="newunits" c="0"
mode="if\_mask\_excludes\_then\_nodata\_else\_data"/&gt;
&lt;/Layer&gt;
```

4. MSGCPP VISIBLE-mask - Display the visible part of the disk
-------------------------------------------------------------

Based on sunz and satz.
Parameter a is sunz+satz threshold and b is satz threshold

```
&lt;Layer type="database"&gt;
&lt;Group value="auxiliary" /&gt;
&lt;Name force="true"&gt;mask&lt;/Name&gt;
&lt;Title&gt;Mask (-)&lt;/Title&gt;
&lt;DataBaseTable&gt;msgcpp\_0001&lt;/DataBaseTable&gt;
&lt;Variable&gt;sunz&lt;/Variable&gt;
&lt;Variable&gt;satz&lt;/Variable&gt;
&lt;RenderMethod&gt;nearest&lt;/RenderMethod&gt;
&lt;FilePath
filter="\^SEVIR\_OPER\_R*MSGCPP*\_L2.\*\\.nc\$"&gt;/data/ogcrt/data/temporary/&lt;/FilePath&gt;
&lt;Styles&gt;mask,red,green,blue&lt;/Styles&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;LatLonBox minx="-80" maxx="80" miny="-82" maxy="82" /&gt;
&lt;Cache enabled="false" /&gt;
&lt;DataPostProc algorithm="msgcppvisiblemask" a="78" b="80" /&gt;
&lt;ImageText&gt;source: EUMETSAT/KNMI&lt;/ImageText&gt;
&lt;/Layer&gt;
```

5. MSGCPP HIWC-mask - Used for detecting high ice water content derived from four input variables.
--------------------------------------------------------------------------------------------------

MSGCPP HIWC-mask: Thresholds for detection of “High Ice Water Content”
according to HAIC case.
\* - The cloud phase is ice
\* - Cloud water path is &gt; 0.1 kg/m2
\* - Cloud top temperature &lt; 270 K
\* - Cloud optical thickness &gt; 20

```
&lt;Layer type="database"&gt;
&lt;Group value="auxiliary" /&gt;
&lt;Name force="true"&gt;hiwc&lt;/Name&gt;
&lt;Title&gt;High Ice Water Content (-)&lt;/Title&gt;
&lt;DataBaseTable&gt;msgcpp\_0001&lt;/DataBaseTable&gt;
&lt;Variable&gt;cph&lt;/Variable&gt;
&lt;Variable&gt;cwp&lt;/Variable&gt;
&lt;Variable&gt;ctt&lt;/Variable&gt;
&lt;Variable&gt;cot&lt;/Variable&gt;
&lt;RenderMethod&gt;nearest&lt;/RenderMethod&gt;
&lt;FilePath
filter="\^SEVIR\_OPER\_R*MSGCPP*\_L2.\*\\.nc\$"&gt;/data/ogcrt/data/temporary/&lt;/FilePath&gt;
&lt;Styles&gt;red,green,blue,mask,gray\_red,gray\_green,gray\_blue&lt;/Styles&gt;
&lt;Dimension name="time" interval="PT15M"&gt;time&lt;/Dimension&gt;
&lt;LatLonBox minx="-80" maxx="80" miny="-82" maxy="82" /&gt;
&lt;Cache enabled="false" /&gt;
&lt;DataPostProc algorithm="msgcpphiwcmask" a="78" b="80" /&gt;
&lt;ImageText&gt;source: EUMETSAT/KNMI&lt;/ImageText&gt;
&lt;/Layer&gt;
```

6. Colour geographical features according to point values
---------------------------------------------------------

A common case is to have data for a set of geographical features, for
example mean wind per province. These data can be stored in a netCDF
file as point data. A geoJSON file with the geographical information for
the features can then be coupled to the point data (by matching station
name in the point file with the name or id property in the geoJSON
file). This enables ADAGUC to draw the geographical features, coloured
according to the value in the point file.

For example, let's say we have a netCDF poimt file with the maximum
windspeed for 3 areas:
```
ncdump windareas.nc
netcdf windareas {
dimensions:
time = 1 ;
station = 3 ;
variables:
double time(time) ;
time:standard\_name = "time" ;
time:units = "seconds since 1970-1-1" ;
double lon(station) ;
lon:standard\_name = "longitude" ;
lon:units = "degrees\_east" ;
double lat(station) ;
lat:standard\_name = "latitude" ;
lat:units = "degrees\_north" ;
string station(station) ;
station:long\_name = "station\_name" ;
station:cf\_role = "timeseries\_id" ;
double maxw(station, time) ;
maxw:units = "m/s" ;
maxw:standard\_name = "maximum\_windspeed" ;
maxw:grid\_mapping = "projection" ;
char projection ;
projection:proj4 = "+proj=longlat +ellps=WGS84 +datum=WGS84 +no\_defs" ;

// global attributes:
:Conventions = "CF-1.5" ;
:featureType = "timeSeries" ;
data:
time = 1458226800 ;
lon = 4.86, 5.73, 6.61 ;
lat = 52.8, 53.04, 53.17 ;
station = "23", "34", "67" ;
maxw =
30.2,
18.2,
6.5 ;
projection = "" ;
}
```
As point data this file could be displayed as:
![](windareas_point.png)

The geographical information for the wind areas could be in the
windareas.geojson file:
```
{ [type]("FeatureCollection","bbox":[2.0,48.0,8.0,55.0]),
[features]([)
{[type]("Feature","id":"67"),
[properties]({"name":"GR"},"geometry":{"type":"Polygon","coordinates":[[[6.976318359375,53.4291738804146],[6.13037109375,53.40298249424814],[6.15234375,52.928774525801366],[7.05322265625,52.93539665862318],[6.976318359375,53.4291738804146]]]}}),
{[type]("Feature","id":"34"),
[properties]({"name":"FR"},"geometry":{"type":"Polygon","coordinates":[[[6.141357421875,53.409531853086435],[5.38330078125,53.32431151982718],[5.328369140625,52.796119005678506],[6.15234375,52.80940281068805],[6.141357421875,53.409531853086435]]]}}),
{[type]("Feature","id":"23"),
[properties]({"name":"WFR"},"geometry":{"type":"Polygon","coordinates":[[[4.6,52.7],[4.6,53],[5.2,53],[5.2,52.7],[4.6,52.7]]]}})
\]}
```

The addfeature datapostproc can join these two files, by generating a
grid where each grid cell has the value of the maxwind in the grid cell
it belongs to.
The DataPostProc element would be defined in a layer like this:
```
&lt;Layer type="database" hidden="false"&gt;
&lt;Name&gt;windareas&lt;/Name&gt;
&lt;Title&gt;Wind Areas&lt;/Title&gt;
&lt;Variable&gt;maxw&lt;/Variable&gt;
&lt;DataPostProc
a="/usr/people/vreedede/nob/adaguc\_gladheid/testgeojson/data/map.geojson"
algorithm="addfeatures"/&gt;
&lt;FilePath
filter="windareas.nc\$"&gt;/usr/people/vreedede/nob/adaguc\_gladheid/testgeojson/data&lt;/FilePath&gt;
&lt;Styles&gt;weatherall&lt;/Styles&gt;
&lt;/Layer&gt;

```

The result could be a display of values for the entire areas:
![](windareas_grid.png)

The really interesting thing is that an actual data grid is generated
from the point data. This grid can be used to draw a map with a WMS
call, but can also be downloaded through a WCS call, to be used in
further processing.

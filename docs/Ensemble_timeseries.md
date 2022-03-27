Ensemble timeseries
===================

For the CLIPC project, a multimodel ensemble was composed and stored in
a single NetCDF file with an extra dimension named "member". The data
can be found here:
https://climate4impact.eu/impactportal/data/catalogbrowser.jsp?catalog=http://opendap.knmi.nl/knmi/thredds/catalog/CLIPC/knmi/RCM/EUR-44/BC/tas/catalog.xml?

A OpenDAP URL to such a file is
http://opendap.knmi.nl/knmi/thredds/dodsC/CLIPC/knmi/RCM/EUR-44/BC/tas/hd17\_icclim-4-2-3\_KNMI\_ens-multiModel\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc

![](Adaguc-server_timeseries_of_multimodel.png)

**To view a timeseries of the ensemble please do:**

1.  https://climate4impact.eu/impactportal/adagucviewer/?srs=EPSG%3A32661&amp;bbox=31732.813672623597,-5067149.338590992,5740102.015054799,-165317.46308152343&amp;service=%2Fimpactportal%2Fadagucserver%3Fsource%3Dhttp%253A%252F%252Fopendap.knmi.nl%252Fknmi%252Fthredds%252FdodsC%252FCLIPC%252Fknmi%252FRCM%252FEUR-44%252FBC%252Ftas%252Fhd17\_icclim-4-2-3\_KNMI\_ens-multiModel\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc&amp;layer=hd17%24image%2Fpng%24true%24auto%2Fnearest%241%240&amp;selected=0&amp;dims=member\$median,time\$2005-07-01T00:00:00Z&amp;baselayers=baselayer\$ne\_10m\_admin\_0\_countries\_simplified
2.  Click on the big gear, and click "Timeseries mode", a panel on the
    right expands
3.  Click on the map to obtain a multimodel timeseries for specified
    location

**A timeseries request to ADAGUC GetFeatureInfo looks like:**

-   https://climate4impact.eu/impactportal/adagucserver?source=http%3A%2F%2Fopendap.knmi.nl%2Fknmi%2Fthredds%2FdodsC%2FCLIPC%2Fknmi%2FRCM%2FEUR-44%2FBC%2Ftas%2Fhd17\_icclim-4-2-3\_KNMI\_ens-multiModel\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc&amp;service=WMS&amp;request=GetFeatureInfo&amp;version=1.3.0&amp;layers=hd17&amp;query\_layers=hd17&amp;crs=EPSG%3A32661&amp;bbox=-1815715.8820717316%2C-5067149.338590992%2C7587550.710799154%2C-165317.46308152343&amp;width=1550&amp;height=808&amp;i=697&amp;j=358&amp;format=image%2Fgif&amp;info\_format=application%2Fjson&amp;dim\_member=\*&time=1000-01-01T00%3A00%3A00Z%2F3000-01-01T00%3A00%3A00Z&amp;&JSONP=jQuery18309623778657215742\_1496744720914&amp;\_=1496745072033
-   A json is returned, as described in [WMSExtensions](WMSExtensions.md)

**In the \[\[Preinstalled\_virtual\_environment\_2017\]\] the OpenDAP
server can be linked with ADAGUC using:**

-   http://localhost:8080/adaguc-services/adagucserver?source=http%3A%2F%2Fopendap.knmi.nl%2Fknmi%2Fthredds%2FdodsC%2FCLIPC%2Fknmi%2FRCM%2FEUR-44%2FBC%2Ftas%2Fhd17\_icclim-4-2-3\_KNMI\_ens-multiModel\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc
-   This link can be added to the viewer by using "Add data"
-   Or go to
    http://localhost:8080/adaguc-viewer/?service=http%3A%2F%2Flocalhost%3A8080%2Fadaguc-services%2Fadagucserver%3Fsource%3Dhttp%253A%252F%252Fopendap.knmi.nl%252Fknmi%252Fthredds%252FdodsC%252FCLIPC%252Fknmi%252FRCM%252FEUR-44%252FBC%252Ftas%252Fhd17\_icclim-4-2-3\_KNMI\_ens-multiModel\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc

```
ncdump -h
http://opendap.knmi.nl/knmi/thredds/dodsC/CLIPC/knmi/RCM/EUR-44/BC/tas/hd17\_icclim-4-2-3\_KNMI\_ens-multiModel\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc
netcdf
hd17\_icclim-4-2-3\_KNMI\_ens-multiModel\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231
{
dimensions:
bnds = 2 ;
maxStrlen64 = 64 ;
member = 13 ;
rlat = 103 ;
rlon = 106 ;
time = 36 ;
x = 106 ;
y = 103 ;
variables:
double time(time) ;
time:standard\_name = "time" ;
time:long\_name = "time" ;
time:bounds = "time\_bnds" ;
time:units = "days since 1949-12-01 00:00:00" ;
time:calendar = "365\_day" ;
double y(rlat) ;
y:standard\_name = "grid\_latitude" ;
y:long\_name = "latitude in rotated pole grid" ;
y:units = "degrees" ;
y:axis = "Y" ;
double x(rlon) ;
x:units = "degrees" ;
x:axis = "X" ;
x:standard\_name = "grid\_longitude" ;
x:long\_name = "longitude in rotated pole grid" ;
char member(member, maxStrlen64) ;
double lon(y, x) ;
lon:standard\_name = "longitude" ;
lon:long\_name = "longitude" ;
lon:units = "degrees\_east" ;
lon:\_CoordinateAxisType = "Lon" ;
double lat(y, x) ;
lat:standard\_name = "latitude" ;
lat:long\_name = "latitude" ;
lat:units = "degrees\_north" ;
lat:\_CoordinateAxisType = "Lat" ;
double time\_bnds(time, bnds) ;
time\_bnds:calendar = "365\_day" ;
time\_bnds:units = "days since 1949-12-01 00:00:00" ;
float hd17(member, time, y, x) ;
hd17:standard\_name = "ECA&amp;D\_indice" ;
hd17:long\_name = "Heating degree days (sum of 17 degrees - mean
temperature)" ;
hd17:units = "K" ;
hd17:coordinates = "lon lat" ;
hd17:\_FillValue = 1.e+20f ;
hd17:missing\_value = 1.e+20f ;
hd17:cell\_methods = "time: mean" ;
hd17:grid\_mapping = "rotated\_pole" ;
hd17:\_ChunkSize = 13, 1, 103, 106 ;
char rotated\_pole(maxStrlen64) ;
rotated\_pole:grid\_mapping\_name = "rotated\_latitude\_longitude" ;
rotated\_pole:grid\_north\_pole\_latitude = 39.25 ;
rotated\_pole:grid\_north\_pole\_longitude = -162. ;

// global attributes:
:Conventions = "CF-1.6" ;
:institution = "Climate impact portal (http://climate4impact.eu)" ;
:title = "hd17: heating degree days" ;
:references = "http://www.ecad.eu/documents/atbd.pdf" ;
:comment = "ECA&amp;D stands for European Climate Assessment & Dataset"
;
:variable\_name = "hd17" ;
:summary = "hd17 is a climate change index definied by ECA&amp;D. The
indicator measures the total temperature amount of 17C - tas during a
year for a given location" ;
:invar\_gcm\_model\_id = " " ;
:invar\_experiment\_name = "historical" ;
:time\_coverage\_start = "19700101" ;
:time\_coverage\_end = "20051231" ;
:keywords = "ETCCDI, ECA&amp;D, climate, index, hd17,year, reference,
climate model output, EUR-44" ;
:tracking\_id = "2d6e9183-0624-43a2-b925-b6a730aa338f" ;
:invar\_variable\_name = "tasAdjust" ;
:activity = "clipc" ;
:product = "climate model output" ;
:package\_name = "icclim-4-2-3" ;
:package\_references = "https://github.com/cerfacs-globc/icclim" ;
:institution\_id = "KNMI" ;
:institution\_url = "knmi.nl" ;
:contact = "eca@knmi.nl" ;
:contributor\_name = "KNMI" ;
:contributor\_role = "This index was calculated by the ECA&amp;D team.
More ETCCDI and ECA&amp;D indices are available on www.ecad.eu" ;
:date\_created = "20160725" ;
:date\_issued = "20160801" ;
:date\_modified = " " ;
:realisation\_id = " " ;
:source\_data\_id = " " ;
:source\_data\_id\_comment = " " ;
:invar\_platform = " " ;
:invar\_platform\_id = " " ;
:invar\_satellite\_algorithm = " " ;
:invar\_satellite\_sensor = " " ;
:invar\_rcm\_model\_id = "SMHI-RCA4\_v1" ;
:invar\_rcm\_model\_realization\_id = " " ;
:invar\_reanalysis\_id = " " ;
:invar\_bc\_method\_id = "SMHI-DBS43" ;
:invar\_bc\_observation\_id = "EOBS10" ;
:invar\_bc\_period = "1981-2010" ;
:reference\_period = " " ;
:output\_frequency = "yr" ;
:cdm\_datatype = "Grid" ;
:domain = "EUR-44" ;
:geospatial\_bounds = "CORDEX domain: EUR-44" ;
:geospatial\_lat\_min = -44.74485f ;
:geospatial\_lat\_max = 65.15146f ;
:geospatial\_lat\_resolution = "0.44 degrees" ;
:geospatial\_lon\_min = 21.91731f ;
:geospatial\_lon\_max = 72.63582f ;
:geospatial\_lon\_resolution = "0.44 degrees" ;
:tile = " " ;
:invar\_ensemble\_member = "r1i1p1" ;
:invar\_tracking\_id = "0cb10a86-5778-4e4b-a5e7-6186235deff8" ;
:invar\_rcm\_model\_driver = "ens-multiModel" ;
:history = "Thu Sep 22 14:37:34 2016: ncatted -O -a
calendar,time\_bnds,c,c,365\_day
./RCM/EUR-44/BC/tas/hd17\_icclim-4-2-3\_KNMI\_ens-multiModel\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc\\n",
"Thu Sep 22 14:37:04 2016: ncatted -O -a units,time\_bnds,c,c,days since
1949-12-01 00:00:00
./RCM/EUR-44/BC/tas/hd17\_icclim-4-2-3\_KNMI\_ens-multiModel\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc\\n",
"Aggregated members into a single file with ADAGUC. Used input files:
hd17\_icclim-4-2-3\_KNMI\_ens-multiModel-20p-historical-EUR-44-SMHI-DBS43-EOBS10-bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_ens-multiModel-80p-historical-EUR-44-SMHI-DBS43-EOBS10-bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_CCCma-CanESM2\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_CNRM-CM5\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_CSIRO-Mk3-6-0\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_EC-EARTH\_historical\_r12i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_GFDL-ESM2M\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_HadGEM2-ES\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051230.nc,hd17\_icclim-4-2-3\_KNMI\_IPSL-CM5A-MR\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_MIROC5\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_MPI-ESM-LR\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_NorESM1-M\_historical\_r1i1p1\_SMHI-RCA4\_v1\_EUR-44\_SMHI-DBS43\_EOBS10\_bcref-1981-2010\_yr\_19700101-20051231.nc,hd17\_icclim-4-2-3\_KNMI\_ens-multiModel-median-historical-EUR-44-SMHI-DBS43-EOBS10-bcref-1981-2010\_yr\_19700101-20051231.nc"
;
:DODS.strlen = 0 ;
}
```

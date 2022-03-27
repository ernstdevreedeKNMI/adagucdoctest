Layer (type,hidden)
===================

-   type - The type of layer, can be either database,grid or cascaded
-   hidden - When set to true, the Layer is not advertised in the
    GetCapabilities document, but is accessible with GetMap requests.

Below an example of a minimum Layer configuration is given:
```
&lt;Layer type="database"&gt;
&lt;Variable&gt;T2m&lt;/Variable&gt;
&lt;FilePath&gt;/data/sdpkdc/har\_nc/t2mtest.nc&lt;/FilePath&gt;
&lt;Styles&gt;temperature&lt;/Styles&gt;
&lt;/Layer&gt;
```

Grid Layers
-----------

This type of layer show a Graticule grid, displaying meridians and
parallels.
Here an example of a grid layer with a 10 degree interval is given:
```
&lt;Layer type="grid"&gt;
&lt;Group value="baselayers"/&gt;
&lt;Name force="true"&gt;grid10&lt;/Name&gt;
&lt;Title&gt;grid 10 degrees&lt;/Title&gt;
&lt;Grid resolution="10"/&gt;
&lt;WMSFormat name="image/png32"/&gt;
&lt;/Layer&gt;
```

Cascaded Layers
---------------

Cascaded layers are copies of Layers from other services. This mostly
used to add an external background or baselayer map to the service. The
cascaded layer can be called like any normal Layer in the GetMap
request. Combinations of Layers can be requested in the GetMap URL to
compose nice maps.
```
&lt;Layer type="cascaded" hidden="false"&gt;
&lt;Group value="baselayers"/&gt;
&lt;Name force="true"&gt;npsnaturalearth2&lt;/Name&gt;
&lt;Title&gt;NPS - Natural Earth II&lt;/Title&gt;
&lt;WMSLayer service="http://geoservices.knmi.nl/cgi-bin/bgmaps.cgi?"
layer="naturalearth2"/&gt;
&lt;LatLonBox minx="-180" miny="-90" maxx="180" maxy="90"/&gt;
&lt;/Layer&gt;
```

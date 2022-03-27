Service Use Cases
=================

The Adaguc service can be used in a lot of different ways. It can be
used to generate a transparant layer visualising data from a variable in
a NetCDF file (for overlaying) ![](ServiceUseCase1.png) or it can be
used to generate a complete graphical product with a geographical map as
base layer and several data layers as overlay ![](ServiceUseCase2.png).

It can also be used to get information about data on a point on the map,
through the GetFeatureInfo or the GetPointValue call. Data can be served
as ASCII, as HTML, as image, as XML/GML or as JSON or JSONP. This data
can be consumed by programs written in JavaScript, JAVA, C, Python etc.
and used for displaying tabular or graphical output.
In this case the ADAGUC service is used to sample data from the
underlying NetCDF data files, through a special ADAGUC API, which is an
extension of the OGC WMS GetFeatureInfo call. This way of data access
through ADAGUC saves a lot of configuration work and issues in software
that uses model data.

Image of transparent layer
--------------------------

Complete graphical product
--------------------------

GetFeatureInfo
--------------

GetPointValue
-------------

&gt; h3. Image output
&gt;
&gt; h3. JSON formatted output
&gt;
&gt; h3. JSONP protocol
&gt;

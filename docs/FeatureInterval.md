FeatureInterval (match, matchid, label, bgcolor, fillcolor)
===========================================================

-   match - Required, The regular expression to match with the attribute
    value
-   matchid - Required, The attribute name to match with. All attributes
    per feature can be queried with GetFeatureInfo (click on the map in
    ADAGUCViewer).
-   label - Recommended, the label to display inside the legend
-   bgcolor - Optional, the background color for the map, can only be
    configured in the first FeatureInterval
-   fillcolor - Required, the color to shade.

```
&lt;Style name="countries\_nlmask"&gt;
&lt;Legend fixed="true"&gt;bluewhitered&lt;/Legend&gt;
&lt;FeatureInterval match=".\*" matchid="abbrev" bgcolor="\#CCCCFF"
fillcolor="\#CCFFCCFF" label="Other"/&gt;
&lt;FeatureInterval match="NLD.\*" matchid="adm0\_a3"
fillcolor="\#DFFFDF00" label="The Netherlands"/&gt;
&lt;FeatureInterval match="\^Luxembourg\$" matchid="brk\_name"
fillcolor="\#0000FF" label="Luxembourg"/&gt;
&lt;FeatureInterval match="\^Asia\$" matchid="continent"
fillcolor="\#808080" label="Asia"/&gt;
&lt;FeatureInterval match="\^India\$" matchid="abbrev"
fillcolor="\#80FF80" label="India"/&gt;
&lt;NameMapping name="nearest" title="Mask NL"/&gt;
&lt;RenderMethod&gt;nearest&lt;/RenderMethod&gt;
&lt;/Style&gt;

&lt;Layer type="database"&gt;
&lt;Title&gt;Countries&lt;/Title&gt;
&lt;Name&gt;countries&lt;/Name&gt;
&lt;!-- Data obtained from https://geojson-maps.kyd.com.au/ --&gt;
&lt;FilePath
filter=""&gt;{ADAGUC\_PATH}data/datasets/countries.geojson&lt;/FilePath&gt;
&lt;Variable&gt;features&lt;/Variable&gt;
&lt;Styles&gt;countries\_nlmask&lt;/Styles&gt;
&lt;/Layer&gt;
```

-   An example configuration is available here:
    -   https://github.com/KNMI/adaguc-server/blob/master/data/config/adaguc.geojson.xml

<!-- -->

-   Can be used with the following GeoJSON:
    -   https://github.com/KNMI/adaguc-server/blob/master/data/datasets/countries.geojson

![](ADAGUC_GeoJSON_MASKED.png)
In this image, the Netherlands is transparent and can be used as a
visual mask overlay.

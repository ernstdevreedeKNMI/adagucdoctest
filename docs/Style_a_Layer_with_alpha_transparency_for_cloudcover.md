Style a Layer with alpha transparency for cloudcover
====================================================

-   Remember to adjust WMSFormat in WMS to output 32bit PNG images:

```
&lt;WMSFormat name="image/png" format="image/png32"/&gt;
```

This is the legend configuration for cloudcover with alpha transparency
```
&lt;/Legend&gt;
&lt;Legend name="cloudcover" type="colorRange"&gt;
&lt;palette index="0" red="255" green="255" blue="255" alpha="0"/&gt;
&lt;palette index="240" red="255" green="255" blue="255"
alpha="255"/&gt;
&lt;/Legend&gt;
```

This is the style for cloudcover
```
&lt;Style name="cloudcover"&gt;
&lt;Legend fixedclasses="true"
tickround=".1"&gt;cloudcover&lt;/Legend&gt;
&lt;Min&gt;0.0&lt;/Min&gt;
&lt;Max&gt;8&lt;/Max&gt;
&lt;ContourLine width="1" linecolor="\#444444" textcolor="\#444444"
textformatting="%2.1f" classes="3"/&gt;
&lt;ContourLine width="3" linecolor="\#0000FF" textcolor="\#444444"
textformatting="%2.1f" classes="4"/&gt;
&lt;ShadeInterval min="-1" max="2" label="&lt;2"
fillcolor="\#E6E6FF"/&gt;
&lt;ShadeInterval min="2" max="4" label="2-4" fillcolor="\#B3B3FF"/&gt;
&lt;ShadeInterval min="4" max="6" label="4-6" fillcolor="\#8080FF"/&gt;
&lt;ShadeInterval min="6" max="8" label="&gt;6"
fillcolor="\#4C4CFF"/&gt;
&lt;RenderMethod&gt;nearest,bilinear,contour,contourbilinear,shaded&lt;/RenderMethod&gt;
&lt;NameMapping name="nearest" title="Alpha transparency"
abstract="Visualize radar images with alpha transparency on a log
scale"/&gt;
&lt;NameMapping name="bilinear" title="Alpha transparency smooth"
abstract="Visualize radar images with alpha transparency on a log
scale"/&gt;
&lt;/Style&gt;
```

This is is the layer definition with cloudcover
```
&lt;Layer type="database"&gt;
&lt;Cache enabled="false"/&gt;
&lt;Styles&gt;cloudcover&lt;/Styles&gt;
&lt;Dimension name="time" interval="P1D"&gt;time&lt;/Dimension&gt;
&lt;Variable&gt;hih\_cld&lt;/Variable&gt;
&lt;DataPostProc algorithm="ax+b" a="8" b="0" units="octa"/&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;http://opendap.nmdc.eu/knmi/thredds/dodsC/essence/run021/2D\_daymean/hih\_cld\_021\_2026-2100.nc&lt;/FilePath&gt;
&lt;/Layer&gt;
```

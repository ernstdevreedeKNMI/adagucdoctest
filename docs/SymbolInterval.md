SymbolInterval(min,max,binary\_and,file, offset\_x, offset\_y)
==============================================================

Draw symbols for point values
-----------------------------

The SymbolInterval element specifies a symbol file for a range of point
values.

- RenderMethod should be set to "point"

- Pointstyle "symbol" should be selected, see [Point](Point.md) for details.

- The **min** and **max** attributes specify the value range. If just
one SymbolInterval is specified and min max is not configured, all
points will be plotted as symbols.

- The **file** attribute specifies the symbol icon to be plotted at the
station's location.
- Optional settings **offset\_x** and **offset\_y** are used to position
the symbol, symbol is centered around 0,0

Configuration:
```
&lt;Style name="LGTKNMI"&gt;
&lt;Legend&gt;bluewhitered&lt;/Legend&gt;
&lt;ValueRange min="1" max="4"/&gt;
&lt;SymbolInterval min="1" max="2"
file="/home/vreedede/nob/web/WWWRADAR/bolt1\_yellow.png"/&gt;
&lt;SymbolInterval min="2" max="3"
file="/home/vreedede/nob/web/WWWRADAR/bolt2\_yellow.png"/&gt;
&lt;SymbolInterval min="3" max="4"
file="/home/vreedede/nob/web/WWWRADAR/bolt1\_orange.png"/&gt;
&lt;SymbolInterval min="4" max="5"
file="/home/vreedede/nob/web/WWWRADAR/bolt2\_orange.png"/&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Point pointstyle="symbol" fillcolor="\#000000FF"
textcolor="\#FFFFFFFF" linecolor="\#000000A0" discradius="16"
dot="false" anglestart="0" anglestep="120" fontsize="12"
textformat="%0.1f"/&gt;
&lt;/Style&gt;
```

This can be used for example for lightning data where vertical and
horizontal discharges are marked differently:
![](/attachments/694/symbol.png)

Binary\_and example: Combines images based on binary operator &
---------------------------------------------------------------

```
&lt;Style name="BTD300\_sensor"&gt;
&lt;Legend&gt;bluewhitered&lt;/Legend&gt;
&lt;SymbolInterval min="0" max="63"
file="/ssd1/adaguc/btd300/symbols/btdsensor/0.png"/&gt; &lt;!-- Base
image --&gt;
&lt;SymbolInterval binary\_and="1"
file="/ssd1/adaguc/btd300/symbols/btdsensor/1.png"/&gt; &lt;!-- combined
with binary operator --&gt;
&lt;SymbolInterval binary\_and="2"
file="/ssd1/adaguc/btd300/symbols/btdsensor/2.png"/&gt;
&lt;SymbolInterval binary\_and="4"
file="/ssd1/adaguc/btd300/symbols/btdsensor/4.png"/&gt;
&lt;SymbolInterval binary\_and="8"
file="/ssd1/adaguc/btd300/symbols/btdsensor/8.png"/&gt;
&lt;SymbolInterval binary\_and="16"
file="/ssd1/adaguc/btd300/symbols/btdsensor/16.png"/&gt;
&lt;SymbolInterval binary\_and="32"
file="/ssd1/adaguc/btd300/symbols/btdsensor/32.png"/&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Point pointstyle="symbol" fillcolor="\#000000FF"
textcolor="\#FFFFFFFF" linecolor="\#000000A0" discradius="16"
dot="false" anglestart="0" anglestep="120" fontsize="12"
textformat="%0.1f"/&gt;
&lt;NameMapping name="point" title="Sensor warning indicator"
abstract="Draw status of BTD sensor with flash detections"/&gt;
&lt;LegendGraphic
value="/ssd1/adaguc/btd300/symbols/btd300legend.png"/&gt;
&lt;/Style&gt;
```

![](/attachments/713/btd300_adaguc.png)

Draw symbols as marker
----------------------

Sometimes one wants to draw a marker if there is any data available for
a point. for example, to draw a Google maps like marker for every
station that has a name.
This can be done by selecting pointstyle symbol and specifying exactly
one SymbolInterval without min and max attributes.
The offset\_x and offset\_y can be used to offset the image around the
plot coordinate.
The attribute plotstationid (true/false) determines if the station name
will be plotted above the point.

An example are the use of markers like ![](marker.png).

This would look like:
![](singlesymbol.png)

```
&lt;Style name="marker"&gt;
&lt;Legend&gt;bluewhitered&lt;/Legend&gt;
&lt;SymbolInterval file="/home/vreedede/adaguc/marker.png" offset\_x="0"
offset\_y="-8"/&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Point pointstyle="symbol" fillcolor="\#000000FF"
textcolor="\#FFFFFFFF" linecolor="\#000000A0" discradius="16"
dot="false" anglestart="0" anglestep="120" fontsize="12"
textformat="%0.1f" plotstationid="true" /&gt;
&lt;/Style&gt;
```

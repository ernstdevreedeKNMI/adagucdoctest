Vector (linecolor, linewidth,scale,vectorstyle,plotstationid,plotvalue,textformat)
==================================================================================

Configuration of rendering vector point data
--------------------------------------------

If a layer with point data has two components they are assumed to be
speed and direction. Wind vector rendering is configured by a vector
element, together with the configuration by the [Point](Point.md) element.

The vectorstyle attribute can be "disc", "vector" (an arrow whose length
depends on wind speed) or "barb" (a wind barb).
The linecolor attribute defines the color of the wind barb or the
vector.
The linewidth attribute defines the width of lines in of the wind barb
or the vector.
The scale attribute is only needed for the "vector" style and defines a
scaling factor to relate the length of the vector to the wind speed.
The plotstationid determines if a stationid is shown.
The plotvalue attribute determines if the value itself is plotted next
to the barb. Can not be combined with plotstationid.
The textformat attribute is used for formatting the value if
plotvalue="true"

```
&lt;Style name="bftalldiscvec"&gt;
&lt;Legend fixed="true"&gt;bluewhitered&lt;/Legend&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;10000&lt;/Max&gt;
&lt;Thinning radius="40"/&gt;
&lt;RenderMethod&gt;barb,barbthin&lt;/RenderMethod&gt;
&lt;Point pointstyle="point" fillcolor="\#00000060"
textcolor="\#FFFFFFFF" linecolor="\#00000060" discradius="20" dot="true"
anglestart="0" anglestep="120" fontsize="10" textformat="%1.0f"/&gt;
&lt;Vector vectorstyle="disc" linewidth="1.0"
linecolor="\#00FF00FF"/&gt;
&lt;/Style&gt;
```

Example of wind as an arrow:
![](barbvector.png)
Example of wind as a barb:
![](barb.png)
Example of wind as a disc:
![](barbdisc.png)

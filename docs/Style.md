Style (name)
============

Configures a style configuration, which can be assigned to a layer by
using the &lt;Styles&gt; element in that Layer. Styles can also be
assigned automatically to a Layer by configuring one or more
StandardNames element(s). When the Layers standard\_name matches with
one of the names configured in a Style, this Style will also be assigned
to that Layer.

When using remote resources with [AutoResource](AutoResource.md), a style with name
"auto" needs to be configured for automatic scaling of min/max values.
This style is assigned to all layers and can be used for previewing the
data with automatically detected min/max values.

-   name, The name of the style to use within the service.

```

&lt;Style name="auto"&gt;
&lt;Legend&gt;Tg\_woltnhoff&lt;/Legend&gt;
&lt;Scale&gt;0&lt;/Scale&gt;
&lt;Offset&gt;0&lt;/Offset&gt;
&lt;RenderMethod&gt;nearest,bilinear,point&lt;/RenderMethod&gt;
&lt;/Style&gt;

&lt;Style name="examplestyle1"&gt;
&lt;Legend fixedclasses="true" tickinterval="2"
tickround="2"&gt;color&lt;/Legend&gt;
&lt;ContourLine width="0.8" linecolor="\#000000" textcolor="\#404040"
textformatting="%2.0f" interval="2"/&gt;

&lt;ShadeInterval min="-10000" max="0" label="&lt;0"
fillcolor="\#FFFFFF"&gt;0&lt;/ShadeInterval&gt;
&lt;ShadeInterval min="0" max="1" label="0 - 1" /&gt;
&lt;ShadeInterval min="1" max="2" label="1 - 2" /&gt;
&lt;ShadeInterval min="2" max="3" label="2 - 3" /&gt;
&lt;ShadeInterval min="3" max="4" label="3 - 4" /&gt;
&lt;ShadeInterval min="4" max="5" label="4 - 5" /&gt;
&lt;ShadeInterval min="5" max="6" label="5 - 6" /&gt;
&lt;ShadeInterval min="6" max="7" label="6 - 7" /&gt;
&lt;ShadeInterval min="7" max="8" label="7 - 8" /&gt;
&lt;ShadeInterval min="8" max="9" label="8 - 9" /&gt;
&lt;ShadeInterval min="9" max="10" label="9 - 10" /&gt;
&lt;ShadeInterval min="10" max="10000" label="&gt;10"
fillcolor="\#FF00AF"/&gt;
&lt;RenderMethod&gt;nearest,nearestcontour,bilinearcontour,shadedcontour,bilinear&lt;/RenderMethod&gt;
&lt;SmoothingFilter&gt;0&lt;/SmoothingFilter&gt;
&lt;NameMapping name="nearest" title="Temperature 0-10"
abstract="Nearest neighbour rendering"/&gt;
&lt;NameMapping name="shadedcontour" title="Temperature 0-10 shaded"
abstract="Shaded with contourlines"/&gt;
&lt;NameMapping name="nearestcontour" title="Temperature 0-10 contours"
abstract="Nearest neighbour with contourlines"/&gt;
&lt;NameMapping name="bilinearcontour" title="Temperature 0-10 bilinear"
abstract="Bilinear with contourlines"/&gt;
&lt;StandardNames standard\_name="air\_temperature"
units="Celsius"/&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;10&lt;/Max&gt;
&lt;/Style&gt;

&lt;Layer&gt;
&lt;Styles&gt;examplestyle1,examplestyle2,...&lt;/Styles&gt;
...
&lt;/Layer&gt;

```

An example style for cloudcover:
```
&lt;Style name="highcloudcover"&gt;
&lt;Legend fixedclasses="true" tickround="0.1" tickinterval=".1"
&gt;highcloudcover&lt;/Legend&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;1&lt;/Max&gt;
&lt;ShadeInterval min="0.05" max="0.25" label="0.05-0.25"
fillcolor="\#E6E6FF"/&gt;
&lt;ShadeInterval min="0.25" max="0.50" label="0.25-0.5"
fillcolor="\#B3B3FF"/&gt;
&lt;ShadeInterval min="0.50" max="0.75" label="0.50-0.75"
fillcolor="\#8080FF"/&gt;
&lt;ShadeInterval min="0.75" max="1.00" label="0.75-1.00"
fillcolor="\#4C4CFF"/&gt;
&lt;RenderMethod&gt;bilinear,nearest,shaded&lt;/RenderMethod&gt;
&lt;NameMapping name="nearest" title="High cloud cover"
abstract="Rendered with nearest neighbour interpolation"/&gt;
&lt;NameMapping name="bilinear" title="High cloud cover bilinear"
abstract="Rendered with bilinear interpolation"/&gt;
&lt;NameMapping name="contour" title="High cloud cover contour"
abstract="Contourlines on a transparent background"/&gt;
&lt;NameMapping name="shaded" title="High cloud cover shaded"
abstract="Shaded"/&gt;
&lt;NameMapping name="nearestcontour" title="High cloud cover nearest +
contours" abstract="Contours with nearest neighbour interpolated
background"/&gt;
&lt;NameMapping name="bilinearcontour" title="High cloud cover bilinear
+ contours" abstract="Contours with bilinear interpolated
background"/&gt;
&lt;NameMapping name="shadedcontour" title="High cloud cover shaded +
contours" abstract="Contours with shaded background"/&gt;
&lt;StandardNames standard\_name="high\_cloud\_cover"/&gt;
&lt;/Style&gt;
```

See [Predefined Legends](Predefined Legends.md) for some precooked legends for several
physical quantities like temperature, pressure, precipitation, etc..

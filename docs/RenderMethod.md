RenderMethod &lt;value&gt;
==========================

Rendermethod defines the way the data is rendered inside the service.
There are currently four mechanisms to render an image:

-   nearestneighbour in class CImgWarpNearestNeighbour
-   bilinear in class CImgWarpBilinear
-   truecolor in class CImgWarpNearestRGBA
-   points in class CImgRenderPoints

CImgWarpNearestNeighbour
------------------------

-   Choose with "nearest"
    This mechanism renders the data very quickly using nearest neighbour
    rendering. This method is suited to project large images, up to
    5000x5000 pixels in realtime. This is used in http://msgcpp.knmi.nl/
    for rendering the derived products from the MSG satellite.

CImgWarpBilinear
----------------

-   Choose with "bilinear,contour,shaded" or combination of these
    This mechanism has more advanced methods of styling and is able to
    draw the data with bilinear interpolation, contourlines and shading.
    It is mainly used to draw model data with shading and contourlines.

CImgWarpNearestRGBA
-------------------

-   Choose with "rgba"
    This is used to draw true color with alpha channel netcdf files.
    This can be used to draw RGBA netcdf data generated by for example
    the pytroll framework.

CImgRenderPoints
----------------

-   Choose with "point", "pointthin", "barb" or "barbthin"
    These are used to draw point data. The method **point** is for
    simple point data or for a Layer with more than 2 Variables defined.
    The method **barb** for a Layer with wind strength and wind
    direction Variables defined.
    The pointthin and barbthin variants switch on the thinning (getting
    rid of points that would be drawn too close to other points). See
    [Thinning](Thinning.md)

CImgRenderStippling
-------------------

-   Choose with "stippling"

Stippling distance and disc radius can be specified in [Stippling](Stippling.md)

```
&lt;RenderMethod&gt;stippling,nearest&lt;/RenderMethod&gt;
&lt;Stippling distancex="22" distancey="22" discradius="7"/&gt;
```

```
&lt;Legend name="uncertainty" type="colorRange"&gt;
&lt;palette index="000" red="255" green="255" blue="255"/&gt;
&lt;palette index="060" red="196" green="196" blue="196"/&gt;
&lt;palette index="120" red="252" green="209" blue="112"/&gt;
&lt;palette index="180" red="249" green="145" blue="45"/&gt;
&lt;palette index="240" red="191" green="25" blue="35"/&gt;
&lt;/Legend&gt;
&lt;Style name="uncertainty"&gt;
&lt;Legend fixed="true" tickinterval="1"&gt;uncertainty&lt;/Legend&gt;
&lt;Min&gt;1&lt;/Min&gt;
&lt;Max&gt;5&lt;/Max&gt;
&lt;ValueRange min="1" max="5"/&gt;
&lt;RenderMethod&gt;stippling,nearest&lt;/RenderMethod&gt;
&lt;Stippling distancex="22" distancey="22" discradius="7"/&gt;
&lt;NameMapping name="nearest" title="Uncertainty"
abstract="Uncertainty"/&gt;
&lt;NameMapping name="stippling" title="Uncertainty stippled"
abstract="Uncertainty stippled"/&gt;
&lt;StandardNames standard\_name="uncertainty"/&gt;
&lt;/Style&gt;
```

Styling of Layers with shading and contourlines
===============================================

The following configuration provides several ways for styling a layer
using shading and contourlines.

```
&lt;Style name="clt"&gt;
&lt;Legend fixedclasses="true" tickinterval="500"
tickround="1"&gt;rainbow&lt;/Legend&gt;
&lt;Min&gt;0.0&lt;/Min&gt;
&lt;Max&gt;100&lt;/Max&gt;
&lt;RenderMethod&gt;nearest,bilinear,contour,contournearest,contourshaded&lt;/RenderMethod&gt;
&lt;NameMapping name="nearest" title="clt colors" abstract="Drawing
images with clt colors"/&gt;
&lt;NameMapping name="bilinear" title="clt colors smooth"
abstract="Drawing images with clt colors and bilinear
interpolation"/&gt;
&lt;NameMapping name="contour" title="clt contour line"
abstract="Drawing images with clt contour and bilinear
interpolation"/&gt;
&lt;ContourLine width="1.0" linecolor="\#444444" textcolor="\#444444"
textformatting="%2.0f" classes="0,25,50,75,100"/&gt;
&lt;ShadeInterval min="90" max="100" label="90-100" fillcolor="\#00E6FF"
/&gt;
&lt;/Style&gt;
```

Use the following settings in the WMS element to get antialiased smooth
contourlines:
```
&lt;WMSFormat name="image/png" format="image/png32"/&gt;
```

For details please see [Configuration](Configuration.md)

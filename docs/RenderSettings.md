RenderSettings (settings, striding, renderer)
=============================================

-   settings : auto / precise / fast

Controls behaviour of nearestneighbour rendering
(https://github.com/KNMI/adaguc-server/blob/master/adagucserverEC/CImgWarpNearestNeighbour.h).

Option fast is recommended for large grids. Files up to 1000x1000 pixels
can be done with the precise renderer, above the fast renderer is
advise. For files over 4000x4000 pixels tiling is recommended instead.

```
&lt;RenderSettings settings="precise"/&gt;
```

-   striding

Controls how many grid cells are skipped. E.g. if set to 2, every other
(even) grid cell is used for reading.
```
&lt;RenderSettings striding="1"/&gt;
```

-   renderer

At the moment GD can be forced
```
&lt;RenderSettings renderer="gd" /&gt;
```

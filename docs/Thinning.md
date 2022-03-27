Thinning
========

Sometimes there can be so much point data that the rendered point data
items can overlap. It is possible to define the minimum wanted empty
space around an element by the Thinning element with a radius attribute,
which describes the minimum distance in pixels. The points are drawn in
the order in which the occur in the data file. If a new point is closer
than radius pixels from one of the previous points it will not be drawn.
There is no other way to prioritize the drawing order.

```
&lt;Style&gt;
&lt;Point ..../&gt;
&lt;Thinning radius="40"/&gt;
&lt;RenderMethod&gt;pointthin&lt;/RenderMethod&gt;
...
&lt;Style&gt;
```

Example with no thinning:
![](/attachments/692/nothin.png)

Example with thinning:
![](/attachments/693/thin.png)

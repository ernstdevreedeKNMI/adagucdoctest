Include
=======

Inludes additional configuration files

-   location - The XML file to include, must be an absolute path.

For example:

&lt;Include location="/data/services/config/datasets/mystyles.xml"/&gt;

Where mystyles.xml can be like:

```

&lt;?xml version="1.0" encoding="UTF-8" ?&gt;
&lt;Configuration&gt;
&lt;Legend name="temperature" type="colorRange"&gt;
&lt;palette index="0" red="0" green="60" blue="123"/&gt;
&lt;palette index="30" red="0" green="100" blue="140"/&gt;
&lt;palette index="60" red="8" green="130" blue="206"/&gt;
&lt;palette index="85" red="132" green="211" blue="255"/&gt;
&lt;palette index="120" red="247" green="247" blue="247"/&gt;
&lt;palette index="155" red="255" green="195" blue="57"/&gt;
&lt;palette index="180" red="232" green="28" blue="0"/&gt;
&lt;palette index="210" red="165" green="0" blue="0"/&gt;
&lt;palette index="240" red="90" green="0" blue="0"/&gt;
&lt;/Legend&gt;

&lt;Style name="tg"&gt;
&lt;Legend&gt;temperature&lt;/Legend&gt;
&lt;Min&gt;-20&lt;/Min&gt;
&lt;Max&gt;30&lt;/Max&gt;
&lt;RenderMethod&gt;nearest,bilinear&lt;/RenderMethod&gt;
&lt;/Style&gt;
&lt;/Configuration&gt;
```

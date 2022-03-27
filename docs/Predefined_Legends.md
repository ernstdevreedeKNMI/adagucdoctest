Predefined Legends
==================

Legends from soliton:
---------------------

http://soliton.vm.bytemark.co.uk/pub/cpt-city/views/totp-cpt.html

Isoluminant legend:
-------------------

```
&lt;Legend name="isoluminant" type="colorRange"&gt;
&lt;palette index="0" red="216" green="15" blue="15"/&gt;
&lt;palette index="48" red="134" green="134" blue="0"/&gt;
&lt;palette index="96" red="0" green="151" blue="0"/&gt;
&lt;palette index="144" red="0" green="143" blue="143"/&gt;
&lt;palette index="192" red="81" green="253" blue="247"/&gt;
&lt;palette index="240" red="183" green="0" blue="183"/&gt;
&lt;/Legend&gt;
```
The min and max parameters refer directly to the position in the
palette. The colors are not interpolated, which results in discrete
intervals. For an interval legend, both index and min/max parameters can
be used.

Climate and weather physical quantities
---------------------------------------

```
&lt;Legend name="temperature" type="interval"&gt;
&lt;palette index="0" color="\#2E2E73"/&gt; &lt;!-- ~~14 -~~&gt;
&lt;palette index="9" color="\#282898"/&gt; &lt;!-- ~~12 -~~&gt;
&lt;palette index="18" color="\#201FBB"/&gt; &lt;!-- ~~10 -~~&gt;
&lt;palette index="27" color="\#1A1ADC"/&gt; &lt;!-- ~~8 -~~&gt;
&lt;palette index="36" color="\#3654DE"/&gt; &lt;!-- ~~6 -~~&gt;
&lt;palette index="45" color="\#548EDC"/&gt; &lt;!-- ~~4 -~~&gt;
&lt;palette index="54" color="\#72CADE"/&gt; &lt;!-- ~~2 -~~&gt;
&lt;palette index="63" color="\#6DD8DF"/&gt; &lt;!-- 0--&gt;
&lt;palette index="72" color="\#55CDE2"/&gt; &lt;!-- 2--&gt;
&lt;palette index="81" color="\#38BBDC"/&gt; &lt;!-- 4 --&gt;
&lt;palette index="90" color="\#20B0DC"/&gt; &lt;!-- 6 --&gt;
&lt;palette index="99" color="\#19BAA6"/&gt; &lt;!-- 8 --&gt;
&lt;palette index="108" color="\#1CCE6A"/&gt; &lt;!-- 10 --&gt;
&lt;palette index="117" color="\#1BDF22"/&gt; &lt;!-- 12 --&gt;
&lt;palette index="126" color="\#82C319"/&gt; &lt;!-- 14 --&gt;
&lt;palette index="135" color="\#DCA819"/&gt; &lt;!-- 16 --&gt;
&lt;palette index="144" color="\#DD921A"/&gt; &lt;!-- 18 --&gt;
&lt;palette index="153" color="\#DE7C1A"/&gt; &lt;!-- 20 --&gt;
&lt;palette index="162" color="\#DF671A"/&gt; &lt;!-- 22 --&gt;
&lt;palette index="171" color="\#DE501A"/&gt; &lt;!-- 24 --&gt;
&lt;palette index="180" color="\#DD3819"/&gt; &lt;!-- 26 --&gt;
&lt;palette index="189" color="\#DD2319"/&gt; &lt;!-- 28 --&gt;
&lt;palette index="198" color="\#D21A1E"/&gt; &lt;!-- 30 --&gt;
&lt;palette index="207" color="\#C31927"/&gt; &lt;!-- 32 --&gt;
&lt;palette index="216" color="\#AD1A30"/&gt; &lt;!-- 34 --&gt;
&lt;palette index="225" color="\#9A1A3B"/&gt; &lt;!-- 36 --&gt;
&lt;palette index="234" color="\#871A44"/&gt; &lt;!-- 38 --&gt;
&lt;palette index="240" color="\#871A44"/&gt; &lt;!-- 39,33 --&gt;
&lt;/Legend&gt;

&lt;Legend name="precipitation" type="interval"&gt;
&lt;palette index="0" color="\#BACDCB"/&gt; &lt;!-- 0 --&gt;
&lt;palette index="30" color="\#A3C3C9"/&gt; &lt;!-- 0.1 --&gt;
&lt;palette index="60" color="\#8BBCC8"/&gt; &lt;!-- 0.2 --&gt;
&lt;palette index="90" color="\#6AAEC1"/&gt; &lt;!-- 0.5 --&gt;
&lt;palette index="120" color="\#42A1C0"/&gt; &lt;!-- 1 --&gt;
&lt;palette index="150" color="\#377EAF"/&gt; &lt;!-- 2 --&gt;
&lt;palette index="180" color="\#46669C"/&gt; &lt;!-- 5 --&gt;
&lt;palette index="210" color="\#56528D"/&gt; &lt;!-- 10--&gt;
&lt;palette index="239" color="\#86008D"/&gt; &lt;!-- 30--&gt;
&lt;/Legend&gt;

&lt;Legend name="pressure" type="interval"&gt;
&lt;palette index="0" color="\#5C5797"/&gt; &lt;!-- 960 --&gt;
&lt;palette index="12" color="\#1D5791"/&gt; &lt;!-- 964 --&gt;
&lt;palette index="24" color="\#1E8BC5"/&gt; &lt;!-- 968 --&gt;
&lt;palette index="36" color="\#1EA6B9"/&gt; &lt;!-- 972 --&gt;
&lt;palette index="48" color="\#1A99A0"/&gt; &lt;!-- 976 --&gt;
&lt;palette index="60" color="\#1C7976"/&gt; &lt;!-- 980 --&gt;
&lt;palette index="72" color="\#1C7244"/&gt; &lt;!-- 984 --&gt;
&lt;palette index="84" color="\#72B060"/&gt; &lt;!-- 988 --&gt;
&lt;palette index="96" color="\#AFC560"/&gt; &lt;!-- 992 --&gt;
&lt;palette index="108" color="\#C9CF3C"/&gt; &lt;!-- 996 --&gt;
&lt;palette index="120" color="\#E3DA36"/&gt; &lt;!-- 1000 --&gt;
&lt;palette index="132" color="\#EFE686"/&gt; &lt;!-- 1004 --&gt;
&lt;palette index="144" color="\#EFE3BB"/&gt; &lt;!-- 1008 --&gt;
&lt;palette index="156" color="\#ECCB90"/&gt; &lt;!-- 1012 --&gt;
&lt;palette index="168" color="\#E7A34A"/&gt; &lt;!-- 1016 --&gt;
&lt;palette index="180" color="\#DE7222"/&gt; &lt;!-- 1020 --&gt;
&lt;palette index="192" color="\#D93531"/&gt; &lt;!-- 1024 --&gt;
&lt;palette index="204" color="\#C41F32"/&gt; &lt;!-- 1028 --&gt;
&lt;palette index="216" color="\#843537"/&gt; &lt;!-- 1032 --&gt;
&lt;palette index="228" color="\#5E3F3A"/&gt; &lt;!-- 1036 --&gt;
&lt;palette index="239" color="\#2E3F2A"/&gt; &lt;!-- 1040 --&gt;
&lt;/Legend&gt;

&lt;Style name="temperature"&gt;
&lt;Legend fixed="true" tickinterval="2"&gt;temperature&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;-14&lt;/Min&gt;
&lt;Max&gt;39,33333333&lt;/Max&gt; &lt;!-- 39,33333333 = (240 / (234/(38
- ~~14)))~~ 14 --&gt;
&lt;NameMapping name="point" title="Temperature"
abstract="Temperature"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="15"
textradius="0" dot="false" fontsize="8" textcolor="\#000000" /&gt;
&lt;/Style&gt;

&lt;Style name="precipitation"&gt;
&lt;Legend fixed="true"
tickinterval="2"&gt;precipitation&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;30&lt;/Max&gt;
&lt;NameMapping name="point" title="precipitation"
abstract="precipitation"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="15"
textradius="0" dot="false" fontsize="8" textcolor="\#000000" /&gt;
&lt;/Style&gt;

&lt;Style name="pressure"&gt;
&lt;Legend fixed="true" tickinterval="4"&gt;pressure&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;960&lt;/Min&gt;
&lt;Max&gt;1040&lt;/Max&gt;
&lt;NameMapping name="point" title="pressure" abstract="pressure"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="15"
textradius="0" dot="false" fontsize="8" textcolor="\#000000"
textformat="%0.0f"/&gt;
&lt;/Style&gt;
```

Seismological data
------------------

```
&lt;Legend name="magnitude\_int" type="interval"&gt;
&lt;palette index="0" color="\#55005550"/&gt; &lt;!-- 0 Nothing --&gt;
&lt;palette index="20" color="\#66009980"/&gt; &lt;!-- 1 Insignificant
--&gt;
&lt;palette index="40" color="\#0099FF80"/&gt; &lt;!-- 2 Low --&gt;
&lt;palette index="60" color="\#00CC99B0"/&gt; &lt;!-- 3 Minor --&gt;
&lt;palette index="80" color="\#99CC66B0"/&gt; &lt;!-- 4 Moderate
--&gt;
&lt;palette index="100" color="\#99FF33B0"/&gt; &lt;!-- 5 Intermediate
--&gt;
&lt;palette index="120" color="\#FFFF33B0"/&gt; &lt;!-- 6 Noteworthy
--&gt;
&lt;palette index="140" color="\#FFCC66C0"/&gt; &lt;!-- 7 High --&gt;
&lt;palette index="160" color="\#FF9966D0"/&gt; &lt;!-- 8 Far-reaching
--&gt;
&lt;palette index="180" color="\#FF3300E0"/&gt; &lt;!-- 9 Outstanding
--&gt;
&lt;palette index="200" color="\#CC0000FF"/&gt; &lt;!-- 10 Extraordinary
--&gt;
&lt;palette index="220" color="\#880000FF"/&gt; &lt;!-- 11 ! --&gt;
&lt;palette index="239" color="\#000000FF"/&gt; &lt;!-- 12 !! --&gt;
&lt;/Legend&gt;

&lt;Legend name="magnitude\_col" type="colorRange"&gt;
&lt;palette index="0" color="\#55005550"/&gt; &lt;!-- 0 Nothing --&gt;
&lt;palette index="20" color="\#66009980"/&gt; &lt;!-- 1 Insignificant
--&gt;
&lt;palette index="40" color="\#0099FF80"/&gt; &lt;!-- 2 Low --&gt;
&lt;palette index="60" color="\#00CC99B0"/&gt; &lt;!-- 3 Minor --&gt;
&lt;palette index="80" color="\#99CC66B0"/&gt; &lt;!-- 4 Moderate
--&gt;
&lt;palette index="100" color="\#99FF33B0"/&gt; &lt;!-- 5 Intermediate
--&gt;
&lt;palette index="120" color="\#FFFF33B0"/&gt; &lt;!-- 6 Noteworthy
--&gt;
&lt;palette index="140" color="\#FFCC66C0"/&gt; &lt;!-- 7 High --&gt;
&lt;palette index="160" color="\#FF9966D0"/&gt; &lt;!-- 8 Far-reaching
--&gt;
&lt;palette index="180" color="\#FF3300E0"/&gt; &lt;!-- 9 Outstanding
--&gt;
&lt;palette index="200" color="\#CC0000FF"/&gt; &lt;!-- 10 Extraordinary
--&gt;
&lt;palette index="220" color="\#880000FF"/&gt; &lt;!-- 11 ! --&gt;
&lt;palette index="239" color="\#000000FF"/&gt; &lt;!-- 12 !! --&gt;
&lt;/Legend&gt;

&lt;Legend name="magnitude\_noalpha" type="colorRange"&gt;
&lt;palette index="0" color="\#550055"/&gt; &lt;!-- 0 Nothing --&gt;
&lt;palette index="20" color="\#660099"/&gt; &lt;!-- 1 Insignificant
--&gt;
&lt;palette index="40" color="\#0099FF"/&gt; &lt;!-- 2 Low --&gt;
&lt;palette index="60" color="\#00CC99"/&gt; &lt;!-- 3 Minor --&gt;
&lt;palette index="80" color="\#99CC66"/&gt; &lt;!-- 4 Moderate --&gt;
&lt;palette index="100" color="\#99FF33"/&gt; &lt;!-- 5 Intermediate
--&gt;
&lt;palette index="120" color="\#FFFF33"/&gt; &lt;!-- 6 Noteworthy
--&gt;
&lt;palette index="140" color="\#FFCC66"/&gt; &lt;!-- 7 High --&gt;
&lt;palette index="160" color="\#FF9966"/&gt; &lt;!-- 8 Far-reaching
--&gt;
&lt;palette index="180" color="\#FF3300"/&gt; &lt;!-- 9 Outstanding
--&gt;
&lt;palette index="200" color="\#CC0000"/&gt; &lt;!-- 10 Extraordinary
--&gt;
&lt;palette index="220" color="\#880000"/&gt; &lt;!-- 11 ! --&gt;
&lt;palette index="239" color="\#000000"/&gt; &lt;!-- 12 !! --&gt;
&lt;/Legend&gt;

&lt;Style name="magnitude\_int"&gt;
&lt;Legend fixed="true"
tickinterval="1"&gt;magnitude\_int&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;12&lt;/Max&gt;
&lt;NameMapping name="point" title="Richter magnitude scale"
abstract="With discrete colors"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="20"
textradius="0" dot="false" fontsize="14" textcolor="\#FFFFFF"/&gt;
&lt;/Style&gt;

&lt;Style name="magnitude\_col"&gt;
&lt;Legend fixed="true"
tickinterval="1"&gt;magnitude\_col&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;12&lt;/Max&gt;
&lt;NameMapping name="point" title="Richter magnitude scale"
abstract="Wth continuous colors"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="20"
textradius="0" dot="false" fontsize="14" textcolor="\#FFFFFF"/&gt;
&lt;/Style&gt;

&lt;Style name="magnitude2"&gt;
&lt;Legend fixed="true"
tickinterval="1"&gt;magnitude\_int&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;12&lt;/Max&gt;
&lt;NameMapping name="point" title="Richter magnitude scale &gt;=2.0"
abstract="magnitude"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="20"
textradius="0" dot="false" fontsize="14" textcolor="\#FFFFFF"/&gt;
&lt;ValueRange min="2" max="1000"/&gt;
&lt;/Style&gt;

&lt;Style name="magnitude3"&gt;
&lt;Legend fixed="true"
tickinterval="1"&gt;magnitude\_int&lt;/Legend&gt;
&lt;RenderMethod&gt;point&lt;/RenderMethod&gt;
&lt;Min&gt;0&lt;/Min&gt;
&lt;Max&gt;12&lt;/Max&gt;
&lt;NameMapping name="point" title="Richter magnitude scale &gt;=3.0"
abstract="magnitude"/&gt;
&lt;Point plotstationid="false" pointstyle="point" discradius="20"
textradius="0" dot="false" fontsize="14" textcolor="\#FFFFFF"/&gt;
&lt;ValueRange min="3" max="1000"/&gt;
&lt;/Style&gt;

```

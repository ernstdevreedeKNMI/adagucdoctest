ADAGUC Workshop 2017
====================

The announcement can be found here:
http://adaguc.knmi.nl//contents/documents/ADAGUC\_workshop\_2017\_June\_7.pdf

Please install the virtual image from
\[\[Preinstalled\_virtual\_environment\_2017\]\]

The workshop will be held at KNMI in the Bleekerzaal on Wednesday June
the 7th.

Agenda (flexible)
-----------------

-   09:00 Opening of the workshop, coffee, tour de table
-   09:30 Overview and new features since last workshop:
    -   https://dev.knmi.nl/attachments/1330/ADAGUC-2017-06-01\_KNMI.pptx
    -   [Overview](Overview.md) of system
    -   [Adaguc-services](Adaguc-services.md)
    -   GitHub
        -   https://github.com/KNMI/adaguc-services - Java application
            for running adaguc-server from tomcat or as a spring boot
            application
        -   https://github.com/KNMI/adaguc-server - C** server for
            serving WMS, WCS and OpenDAP
        -   https://github.com/KNMI/adaguc-viewer - Javascript web
            client for connecting to WMS
        -   https://github.com/KNMI/adaguc-datasets - Example dataset
            configurations
    -   ADAGUC OpenEarth Docker
        -   [Docker](Docker.md)
        -   sudo docker run -i -t --net adagucnet --ip 172.18.0.2 -v
            /data:/data openearth/adaguc-server
    -   [Himawari and Tiling](Himawari and Tiling.md)
        -   [TileSettings](TileSettings.md)
    -   Tropomi and NetCDF groups
        -   https://github.com/KNMI/adaguc-server/blob/master/CCDFDataModel/CCDFNetCDFIO.cpp
    -   GCM's and 360 day calendars
        -   https://github.com/KNMI/adaguc-server/blob/master/CCDFDataModel/CTime.cpp
    -   [OpenDAP](OpenDAP.md) Server
        -   ncdump -h
            http://localhost/cgi-bin/adaguc-datasets.cgi/opendap/opendapdataset/RADNL\_OPER\_R**\_25PCPRR\_L3\_KNMI.nc
        -   ncview
            http://localhost/cgi-bin/adaguc-datasets.cgi/opendap/opendapdataset/RADNL\_OPER\_R**\_25PCPRR\_L3\_KNMI.nc
        -   https://github.com/KNMI/adaguc-datasets/blob/master/opendapdataset.xml
    -   Datapostprocessors: masking
        -   [DataPostProc](DataPostProc.md)
        -   https://github.com/KNMI/adaguc-datasets/blob/master/datapostproc\_mask.xml
    -   Timeseries
        -   [WMSExtensions](WMSExtensions.md)
    -   [Ensemble timeseries](Ensemble timeseries.md)
-   10:30 Coffee
-   10:45 Overview and new features since last workshop:
    -   GeoJSON and WCS rasterizer
        -   [FeatureInterval](FeatureInterval.md)
    -   Additional layer functions (GMS)
        -   [AdditionalLayer](AdditionalLayer.md)
-   11:15 Demo of climate4impact and GeoWeb (ReacjtJS)
    -   https://esgf.llnl.gov/media/2016-F2F/7-12-2016/community\_software/F2F-2016-climate4impact\_provenance.pdf
-   11:45 Virtual machine and tour through VM / Installation
    instructions
    -   \[\[Preinstalled\_virtual\_environment\_2017\]\]
-   12:30 Lunch (at your own expense)
-   13:00 Continue installation / Get your data into the system / Hands
    on experience
-   15:00 Live configuration demo
-   16:00 Continuation installation / add your own data
-   18:00 End of Workshop

References
----------

-   ADAGUC overview presentation:
    https://dev.knmi.nl/attachments/1330/ADAGUC-2017-06-01\_KNMI.pptx
-   Clipc results:
    http://www.clipc.eu/media/clipc/org/documents/deliverables/clipc-d4.3-final.pdf
-   Please check VM: \[\[Preinstalled\_virtual\_environment\_2017\]\]
-   Installation: \[\[Install\_Adaguc\_on\_Ubuntu\]\]
-   Configuration: [Configuration](Configuration.md)
-   Web Processing and Climate4Impact:
    https://esgf.llnl.gov/media/2016-F2F/7-12-2016/community\_software/F2F-2016-climate4impact\_provenance.pdf


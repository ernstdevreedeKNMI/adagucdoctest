ADAGUC Workshop 2018 @ KNMI, 21 - 23 November
=============================================

The third ADAGUC workshop will be hosted at KNMI from 21 till 23
November in rooms A0.10 and A0.12 .

**Subscribe:** Subscription and requests for information can be done by
sending an email to adaguc at knmi.nl. The workshop has no subscription
fee, lunch is at your own expense. There is a maximum number of \~25
participants. Especially for the second and third day you have to bring
your own laptop, wifi is provided. Please indicate which days you wish
to participate.

The first day will include a demonstration and is to learn about the
ADAGUC system and its capabilities. The second and third day is for
installation and getting experience and getting your own data into the
system.

KNMI is reachable via
https://www.knmi.nl/over-het-knmi/contact/contactformulier

Flyer
-----

-   https://dev.knmi.nl/attachments/download/8071/ADAGUC\_workshop\_2018\_21till23-November.pdf

Agenda (flexible)
-----------------

**Wednesday 21 November from 13:00-18:00**

-   13:00 Opening of the workshop, coffee, tour de table
-   13:30 Overview and features *[]{.Plieger .Maarten}*
    -   Features:
        https://dev.knmi.nl/attachments/download/6301/Geoweb\_ADAGUC\_technical\_fundamentals\_Maarten\_Plieger\_2018-05-30.pdf
    -   Overview of system [Overview](Overview.md)
    -   Hosted open source on GitHub:
        -   https://github.com/KNMI/adaguc-services - Java application
            for running adaguc-server from tomcat or as a spring boot
            application
        -   https://github.com/KNMI/adaguc-server - C** server for
            serving WMS, WCS and OpenDAP
        -   https://github.com/KNMI/adaguc-viewer - Javascript web
            client for connecting to WMS
        -   https://github.com/KNMI/adaguc-datasets - Example dataset
            configurations
    -   Dockerized version of ADAGUC server and ADAGUC viewer
        -   Much easier installation and configuration
        -   Documentation about docker containers for ADAGUC:
            [Docker](Docker.md)
        -   Configuration via [Dataset](Dataset.md) for aggregation of files
            and custom styling
        -   Demo: Application example of dockerized version in KNMI
            research environment with adaguc-server and adaguc-viewer
            (AutoWMS and Dataset configuration)
        -   \[\[Preinstalled\_virtual\_environment\_2017\]\], with
            instructions top update to the 2018 version
        -   ADAGUC-WebMapJS -
            https://github.com/maartenplieger/adaguc-webmapjs and
            https://github.com/maartenplieger/adaguc-webmapjs-demo
-   14:30 GeoWeb
    -   Presentation of Geoweb (30 min) *[]{.Berge .den .van .Marco}*
    -   Demo of Geoweb (30 min)
-   15:30 Eunadics
    -   Presentation and demonstration of Eunadics *[]{.Wagenaar
        .Saskia}*
-   16:00 New backend for running ADAGUC-server: [Adaguc-services](Adaguc-services.md)
    -   \[\[Himawari and Tiling|Tiling for Himawari high resolution
        satellite dataset\]\]
    -   Support for Tropomi satellite data
        -   https://github.com/KNMI/adaguc-server/blob/master/CCDFDataModel/CCDFNetCDFIO.cpp
        -   https://github.com/KNMI/adaguc-server/blob/master/adagucserverEC/CConvertTROPOMI.h
    -   Time support for Global Climate Models and 360 day calendars
        -   https://github.com/KNMI/adaguc-server/blob/master/CCDFDataModel/CTime.cpp
    -   [OpenDAP](OpenDAP.md) Server
        -   ncdump -h
            http://localhost/cgi-bin/adaguc-datasets.cgi/opendap/opendapdataset/RADNL\_OPER\_R**\_25PCPRR\_L3\_KNMI.nc
        -   ncview
            http://localhost/cgi-bin/adaguc-datasets.cgi/opendap/opendapdataset/RADNL\_OPER\_R**\_25PCPRR\_L3\_KNMI.nc
        -   https://github.com/KNMI/adaguc-datasets/blob/master/opendapdataset.xml
        -   Application/json support for OpenDAP server to facilitate
            interaction with web applications
    -   Datapostprocessors: masking
    -   Timeseries
        -   [WMSExtensions](WMSExtensions.md)
        -   [Ensemble timeseries](Ensemble timeseries.md)
    -   Rasterization of GeoJSON using the Web Coverage Service
    -   Styling of GeoJSON with [FeatureInterval](FeatureInterval.md)
    -   [AdditionalLayer](AdditionalLayer.md) - Additional layer functions, for
        combining different datastreams in one layer (e.g. archive +
        realtime data)
-   16:30 Preview into virtual machine and tour through VM and
    Installation instructions for next days
    -   \[\[Preinstalled\_virtual\_environment\_2017\]\]
    -   [Docker](Docker.md)
        -   Install adaguc-server via Docker
        -   Install adaguc-viewer via Docker
        -   Demonstration of AutoWMS
        -   Demonstration of [Dataset](Dataset.md) configuration
-   18:00 End

**Thursday 22 November from 09:00-18:00**

-   09:00 Coffee
-   09:15 ADAGUC Checker *[]{.Verhoef .Hans}*
-   09:30 Fimex to convert grib2 to NetCDF *[]{.Vreede .de .Ernst}*
-   10:00 ADAGUC Viewer demo and new features (Tiled map support,
    AutoWMS browser)
-   10:30 Live configuration demo
-   11:00 Climate4Impact demo (Web Processing Services)
    https://climate4impact.eu/
-   12:00 Lunch
-   13:00 Continue installation / Get your data into the system / Hands
    on experience
-   18:00 End of day 2

**Friday 23 November from 09:00-17:00**

-   09:00 Get your data into the system / Hands on experience
-   10:00 C3S-Magic Demo https://portal.magic.eu/
-   17:00 End of day 3 (flexible)

References
----------

-   Geoweb and ADAGUC:
    https://dev.knmi.nl/attachments/download/6301/Geoweb\_ADAGUC\_technical\_fundamentals\_Maarten\_Plieger\_2018-05-30.pdf
-   Installation via Docker -
    https://dev.knmi.nl/projects/adagucserver/wiki/Docker
-   ADAGUC overview presentation:
    https://dev.knmi.nl/attachments/1330/ADAGUC-2017-06-01\_KNMI.pptx
-   Clipc results:
    http://www.clipc.eu/media/clipc/org/documents/deliverables/clipc-d4.3-final.pdf
-   Please check VM: \[\[Preinstalled\_virtual\_environment\_2017\]\]
-   Installation: \[\[Install\_Adaguc\_on\_Ubuntu\]\]
-   Configuration: [Configuration](Configuration.md)
-   Web Processing and Climate4Impact:
    https://esgf.llnl.gov/media/2016-F2F/7-12-2016/community\_software/F2F-2016-climate4impact\_provenance.pdf


Workshop 2015
=============

ADAGUC workshop 2015 - June 17-19 (http://adaguc.knmi.nl/)

### Wednesday June 17th - Overview and installation of ADAGUC Viewer + Server

-   10:30 Opening & Tour de table – participants
-   11:00 Overview of the ADAGUC system
    -   Overview of Wiki and Redmine
    -   Short demonstration (Radar + MSGCPP)
    -   What is new, demonstrated via redmine and VM
    -   [DataFormats](DataFormats.md)
        -   Points and symbols
        -   UGrid polygon support
        -   RGBA True color images in NetCDF
        -   Support for curvilinear grids
        -   MetOcean Domain Working group implementation
-   12:00 Lunch
-   13:00 Quick tour on NetCDF, OPeNDAP, WMS, WCS and MetOcean Domain
    Working group implementation
-   https://dev.knmi.nl/attachments/672/KNMI\_ADAGUC\_WMS\_WCS\_NetCDF\_CF\_OpenDAP\_DataFormats\_20150616.pdf
    -   NetCDF file format, Climate and Forecast Conventions
        -   Regular grids
        -   Projected grids
        -   Curvilinear grids
        -   Point timeseries
        -   UGrid polygons
    -   OpenDAP for access to remote NetCDF files and subsetting
    -   WMS and WCS standards
-   14:00 Installation of ADAGUC Viewer and ADAGUC Server
    -   Installation of VM
    -   ADAGUC components
        -   server: cgi and configuration files
        -   viewer: configuration files
-   17:30 End of day one

### Thursday June 18th - Configuration demo and how to use your own data

-   9:30 Wrap-up of previous day
-   10:00 How to configure the server, examples on custom styling and
    rendering
    -   Styling grids: Nearest neighbor, bilinear, shading and
        contourlines configuration
    -   Styling points: Symbols, discs, points, etc...
-   11:30 Embedding the viewer in your own webpage
-   see
    http://geoservices.knmi.nl/viewer2.0/examples/animateradar\_latest.php
-   12:00 Lunch
-   13:00 Get your own data working, display and map your data
    -   Demonstration of ADAGUC applications
    -   OpenLayers, Leaflet, Web Processing (PyWPS)
-   17:30 End of day two

### Friday June 19th - Visualization of remote OpenDAP data and retrieving custom data from the server

-   9:30 Wrap-up of previous day
-   10:00 Visualizing remote OPeNDAP servers (ESGF, Unidata, OpenEarth,
    Met.no, FMI, KNMI)
    -   Demonstration of the Climate4Impact portal
    -   https://climate4impact.eu/
    -   https://dev.knmi.nl/attachments/669/EGU2015\_ESSI2.1-MaartenPlieger-Climate4Impact-IS-ENES2.pdf
-   11:00 Using GetFeatureInfo for making timeseries graphs
-   11:30 Demo application of Pytroll and ADAGUC with Suomi NPP Viirs
    -   https://dev.knmi.nl/attachments/668/EGU2015\_ESSI3.1-MaartenPlieger-Pytroll\_ADAGUC.pdf
-   12:00 Lunch
-   13:00 Roadmap and future work
-   14:00 Getting hands-on experience with ADAGUC
-   17:30 End of workshop

Virtual machine with pre-installed ADAGUC
-----------------------------------------

The virtual machine with the preinstalled ADAGUC system requires \~20Gb
of disk space, a minimum of 1.5Gb of Ram and a Virtual Machine platform
like VirtualBox or VMWare player. Everything has been tested with
Virtualbox under windows. The virtual machine can be downloaded here
via:

-   \[\[Preinstalled\_virtual\_environment\]\]


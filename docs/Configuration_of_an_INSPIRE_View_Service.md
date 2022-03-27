[Configuration](Configuration.md)

Configuration of an INSPIRE View Service
========================================

The following elements need to be configured to create an INSPIRE View
Service:

-   WMS-&gt;Title needs to be set to \[INSPIRE::TITLE\]
-   WMS-&gt;Abstract needs to be set to \[INSPIRE::ABSTRACT\]
-   WMS~~&gt;RootLayer~~&gt;Title needs to be set to \[INSPIRE::TITLE\]

<!-- -->

-   WMS~~&gt;Inspire~~&gt;ViewServiceCSW - The global view service
    document (CSW service) describing the view services
-   WMS~~&gt;Inspire~~&gt;DatasetCSW - The dataset CSW service
    describing the dataset
-   WMS~~&gt;Inspire~~&gt;AuthorityURL - The name and URL of the
    Authority offering the data
-   WMS~~&gt;Inspire~~&gt;Identifier - The identifier of the Authority

<!-- -->

-   Layer~~&gt;Abstract~~ An abstract describing the layer, Name and
    Title needs to be set as normal

```

&lt;WMS&gt;
&lt;Title&gt;\[INSPIRE::TITLE\]&lt;/Title&gt;
&lt;Abstract&gt;\[INSPIRE::ABSTRACT\]&lt;/Abstract&gt;
&lt;RootLayer&gt;
&lt;Title&gt;\[INSPIRE::TITLE\]&lt;/Title&gt;
&lt;Abstract&gt;&lt;/Abstract&gt;
&lt;/RootLayer&gt;
&lt;TitleFont location="/data/fonts/FreeSans.ttf" size="19"/&gt;
&lt;SubTitleFont location="/data/fonts/FreeSans.ttf" size="10"/&gt;
&lt;DimensionFont location="/data/fonts/FreeSans.ttf" size="7"/&gt;
&lt;ContourFont location="/data/fonts/FreeSans.ttf" size="7"/&gt;
&lt;GridFont location="/data/fonts/FreeSans.ttf" size="5"/&gt;
&lt;WMSFormat name="image/png" format="image/png"/&gt;
&lt;Inspire&gt;
&lt;ViewServiceCSW&gt;http://data-test.knmi.nl/inspire/csw?Service=CSW&amp;amp;Request=GetRecordById&amp;amp;Version=2.0.2&amp;amp;id=9155a021-ac62-464c-99e2-b4c809e5ecde&amp;amp;outputSchema=http://www.isotc211.org/2005/gmd&amp;amp;elementSetName=full&lt;/ViewServiceCSW&gt;
&lt;DatasetCSW&gt;http://data-test.knmi.nl/inspire/csw?Service=CSW&amp;amp;Request=GetRecordById&amp;amp;Version=2.0.2&amp;amp;id=0d6f8f49-94d0-4e21-a7c1-2d703ce1fd22&amp;amp;outputSchema=http://www.isotc211.org/2005/gmd&amp;amp;elementSetName=full&lt;/DatasetCSW&gt;
&lt;AuthorityURL name="NL.KNMI" onlineresource="http://knmi.nl/"/&gt;
&lt;Identifier authority="NL.KNMI" id="id\_value"/&gt;
&lt;/Inspire&gt;
&lt;/WMS&gt;

&lt;Layer&gt;
...
&lt;Abstract&gt;nice abstract describing the layer&lt;/Abstract&gt;
&lt;/Layer&gt;

```

Configuration of an INSPIRE View Service with one service endpoint and multiple datasets
========================================================================================

This tutorial is based on a single endpoint for a WMS service, where
several datasets are identified with the DATASET= parameter.

The endpoint is for example:
```
http://data-test.knmi.nl/inspire/wms/cgi-bin/wms.cgi?
```

Datasets within the WMS service are identified with the DATASET=
parameter, for example:

```
http://data-test.knmi.nl/inspire/wms/cgi-bin/wms.cgi?DATASET=urn:xkdc:ds:nl.knmi::kisinspire2/1/&amp;
```

In the GetCapabilities document this URL is returned as online resource
for the GetMap, GetFeatureInfo and GetLegendGraphic requests.

The datasets identified with the DATASET parameter are extra
configuration files which are included in the main configuration file of
the WMS service. To enable this feature, the [Dataset](Dataset.md) option
needs to be configured in the WMS service.

When everything is configured correctly, there is one global
configuration file and several dataset configuration files representing
the datasets.

-   /data/config/inswms.xml - The global configuration file
-   /data/datasetconfigs/urn\_xkdc\_ds\_nl.knmi\_*kisinspire2\_1*.xml -
    The dataset configuration file, which is loaded by using the
    DATASET=urn:xkdc:ds:nl.knmi::kisinspire2/1/ parameter. Note that the
    DATASET identifier is escaped, the ':' and '/' characters become
    '\_' on the filesystem.

The global configuration file is named /data/config/inswms.xml and can
look like this:

```

&lt;WMS&gt;
&lt;Title&gt;\[INSPIRE::TITLE\]&lt;/Title&gt;
&lt;Abstract&gt;\[INSPIRE::ABSTRACT\]&lt;/Abstract&gt;
&lt;RootLayer&gt;
&lt;Title&gt;\[INSPIRE::TITLE\]&lt;/Title&gt;
&lt;Abstract&gt;&lt;/Abstract&gt;
&lt;/RootLayer&gt;
&lt;TitleFont location="/data/fonts/FreeSans.ttf" size="19"/&gt;
&lt;SubTitleFont location="/data/fonts/FreeSans.ttf" size="10"/&gt;
&lt;DimensionFont location="/data/fonts/FreeSans.ttf" size="7"/&gt;
&lt;ContourFont location="/data/fonts/FreeSans.ttf" size="7"/&gt;
&lt;GridFont location="/data/fonts/FreeSans.ttf" size="5"/&gt;
&lt;WMSFormat name="image/png" format="image/png"/&gt;
&lt;Inspire&gt;
&lt;ViewServiceCSW&gt;http://data-test.knmi.nl/inspire/csw?Service=CSW&amp;amp;Request=GetRecordById&amp;amp;Version=2.0.2&amp;amp;id=9155a021-ac62-464c-99e2-b4c809e5ecde&amp;amp;outputSchema=http://www.isotc211.org/2005/gmd&amp;amp;elementSetName=full&lt;/ViewServiceCSW&gt;
&lt;AuthorityURL name="NL.KNMI" onlineresource="http://knmi.nl/"/&gt;
&lt;Identifier authority="NL.KNMI" id="id\_value"/&gt;
&lt;/Inspire&gt;
&lt;/WMS&gt;

&lt;Dataset enabled="true" location="/data/datasetconfigs/"/&gt;
```

Note that in the Inspire section the DatasetCSW is removed, as this
option is dependent of the dataset in question.

The dataset configuration file needs to have the filename
urn\_xkdc\_ds\_nl.knmi\_*kisinspire2\_1*.xml and looks like this:
```
&lt;?xml version="1.0" encoding="UTF-8" ?&gt;
&lt;Configuration&gt;
&lt;WMS&gt;
&lt;Inspire&gt;
&lt;DatasetCSW&gt;http://data-test.knmi.nl/inspire/csw?Service=CSW&amp;amp;Request=GetRecordById&amp;amp;Version=2.0.2&amp;amp;id=0d6f8f49-94d0-4e21-a7c1-2d703ce1fd22&amp;amp;outputSchema=http://www.isotc211.org/2005/gmd&amp;amp;elementSetName=full&lt;/DatasetCSW&gt;
&lt;/Inspire&gt;
&lt;/WMS&gt;
&lt;Layer type="database"&gt;
&lt;FilePath
filter=".\*\\.nc\$"&gt;/data/kisinspire2/1/&lt;/FilePath&gt;
&lt;Name&gt;TG\_air\_temperature&lt;/Name&gt;
&lt;Title&gt;Temperature&lt;/Title&gt;
&lt;Variable&gt;TG&lt;/Variable&gt;
&lt;Abstract&gt;Daily mean temperature in (0.1 degrees
Celsius);&lt;/Abstract&gt;
&lt;/Layer&gt;
&lt;/Configuration&gt;
```
This file is located in /data/datasetconfigs/

Here the WMS~~&gt;Inspire~~&gt;DatasetCSW is given, including the Layer.

This sub configuration file can be generated with the adagucserver using
the following command:

```
adagucserver --getlayers --file
/data/kisinspire2/1/inspire\_daily\_weather\_observations\_kis\_v20131021.nc
--inspiredatasetcsw
"http://data-test.knmi.nl/inspire/csw?Service=CSW&amp;Request=GetRecordById&amp;Version=2.0.2&amp;id=0d6f8f49-94d0-4e21-a7c1-2d703ce1fd22&amp;outputSchema=http://www.isotc211.org/2005/gmd&amp;elementSetName=full"
--datasetpath /data/kisinspire2/1/ &gt;
/data/datasetconfigs/urn\_xkdc\_ds\_nl.knmi\_*kisinspire2\_1*.xml
```

To update the database with these two configuration files you can use
the following command:

```
adagucserver --updatedb --config
/data/config/inswms.xml,/data/datasetconfigs/urn\_xkdc\_ds\_nl.knmi\_*kisinspire2\_1*.xml
--tailpath &lt;optional, path to granule in datasetdirectory&gt;
```

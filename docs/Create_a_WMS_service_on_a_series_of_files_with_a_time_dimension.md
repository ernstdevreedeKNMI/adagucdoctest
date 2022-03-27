Create a WMS service on a series of files with a time dimension
===============================================================

When you want to serve a series of files with a time component in your
WMS service, you need to add the directory where all files are located
and you need to provide information about the time dimension.

For example, if you have daily files located in
/data/services/data/mydailyfiles/, you have to point the FilePath
element to that location. You can specify a filter to filter only the
desired files you would like to add. This filter uses posix regular
expressions to make the selection.
Because the data has a time dimension, you need to configure a time
dimension in the layer as well. See [Dimension](Dimension.md) for details on the
configuration.
We select a interval of "P1D", which means that we are dealing with
daily data.

Part of mydailydataconfig.xml:
```
&lt;!-- Layer configuration --&gt;
&lt;Layer type="database"&gt;
&lt;FilePath
filter="\^mydailyfiles.\*\\.nc\$"&gt;/data/services/data/mydailyfiles/&lt;/FilePath&gt;
&lt;Variable&gt;dailytemp&lt;/Variable&gt;
&lt;Styles&gt;rainbow&lt;/Styles&gt;
&lt;Dimension name="time" interval="P1D"
default="max"&gt;time&lt;/Dimension&gt;
&lt;/Layer&gt;
```

(\^mydailyfiles.\*\\.nc\$ is a regular expression, see
http://en.wikipedia.org/wiki/Regular\_expression)

When everything is configured, you have to scan the files, this can be
done with the following command:
```
adagucserver --updatedb --config &lt;path&gt;/mydailydataconfig.xml
```

The scan is recursive, e.g. files may be nested in subdirectories:

```
/data/services/data/mydailyfiles/2013/01/01/myfile.nc
/data/services/data/mydailyfiles/2013/01/02/myfile.nc
...
/data/services/data/mydailyfiles/2013/06/11/myfile.nc
/data/services/data/mydailyfiles/2013/06/12/myfile.nc
```

If you would like to add a single file in the configured data directory,
you can do:
```
adagucserver --updatedb --config &lt;path&gt;/mydailydataconfig.xml
--tailpath /2012/06/11/myfile.nc
```

If you would like to scan specific files in a certain subdirectory of
the configured data directory, you can do:
```
adagucserver --updatedb --config &lt;path&gt;/mydailydataconfig.xml
--tailpath 2012/06/11
```

This adds the files which are located in the given subdirectory. If
files are already added in a previous command, nothing happens.

To create a realtime WMS service, you have to scan for the latest files
in a directory. You could create the following script:
```
\#!/bin/bash
\#Update the server with the latest four days
adagucserver --updatedb --config &lt;path&gt;/mydailydataconfig.xml
--tailpath \`date --date="0 days ago" +%Y/%m/%d\` &gt; /dev/null
adagucserver --updatedb --config &lt;path&gt;/mydailydataconfig.xml
--tailpath \`date --date="1 days ago" +%Y/%m/%d\` &gt; /dev/null
adagucserver --updatedb --config &lt;path&gt;/mydailydataconfig.xml
--tailpath \`date --date="2 days ago" +%Y/%m/%d\` &gt; /dev/null
adagucserver --updatedb --config &lt;path&gt;/mydailydataconfig.xml
--tailpath \`date --date="3 days ago" +%Y/%m/%d\` &gt; /dev/null
```

This script updates the WMS service with the latest days (four) of data.
You could call this script every minute using a crontab to create a
realtime service.

Removing files from the service
-------------------------------

If you would like to remove files from the service, because they do not
exist anymore on the filesystem or for any other reason, you can call
updatedb without tailpath:
```
adagucserver --updatedb --config &lt;path&gt;/mydailydataconfig.xml
```

You can also query the postgres database yourself and throw away the
corresponding records:
```
\#!/bin/bash

PSQL="psql mydatabase -h localhost -U adagucuser "
datesevendays=\`date -~~date="7 days ago" +%Y~~%m-%d\\ %H:%M:%S\`
\$PSQL -c "delete from &lt;table&gt;\_time where time &lt;
'\$datesevendays'" &gt; /dev/null
touch /data/services/config/newservice.xml
```

In that case you should touch the configuration file in order to trigger
regeneration of the XML GetCapabilities document.

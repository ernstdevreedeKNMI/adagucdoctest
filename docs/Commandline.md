Commandline
===========

adagucserver
------------

### Update the database

**--updatedb**

-   --updatedb
-   --config the configuration files to use
-   --path for a absolute path to update
-   --tailpath for scanning specific sub directory (Tailpath is not
    allowed to start with a /)
-   -~~layername Optionally specify the layername to scan, as specified
    in Layer~~&gt;Name to update
-   --rescan Ignores file modification date and re-inserts the file.
-   --noclean Do not remove file records from the database
-   --recreate Drops and recreates database tables
-   --dumpheader Shows NetCDF header

### Get layers - scan a file, returns the possible layers for that file

**--getlayers**

-   --getlayers
-   --file
-   --inspiredatasetcsw
-   --datasetpath

### --createtiles

-   --adagucserver --createtiles --config
    \~/adagucserver/data/config/adaguc.pik.xml

### Output report to a file

**--report**

-   --report=filename to write report specified by filename
-   --report to write report specified in environment variable
    ADAGUC\_CHECKER\_FILE. If variable ADAGUC\_CHECKER\_FILE is not set,
    write file to default location ./checker\_report.txt

aggregate\_time
---------------

Aggregates multiple files over the time dimension into one big file.
Does work on files without unlimited dims as well.
Commandlande arguments are &lt;input dir&gt; &lt;output file&gt;,
optionaly third argument can be a comma separated list of variable names
to add the time dimension to.

E.g.
```
aggregate\_time /data/swe\_L3A\_daily/ /tmp/swe\_L3A\_daily.nc swe
```

Automatically delete files from database and filesystem
-------------------------------------------------------

```
\#/bin/bash

datadir=/data/data2/storage/permanent/adaguc/SEVIR\_OPER\_R**VOLE**\_L2
postgrescredentials="dbname=SEVIR\_OPER\_R**VOLE**\_L2 host=localhost"
limitdaysold=50

1.  Get the right tablenames from the database, based on the directory.
    tablenames=\$(psql -t "\${postgrescredentials}" -c "select tablename
    from pathfiltertablelookup where path = 'P\_\${datadir}' and
    dimension='time';")

for tablename in \$tablenames;do
\# Get the list of files with more than \$limitdaysold days old.
timeolder=\`date -~~date="\${limitdaysold} days ago"
+%Y~~%m-%d\`T00:00:00Z
filelist=\$(psql -t "\${postgrescredentials}" -c "select path from
\${tablename} where time &lt; '\${timeolder}' order by time asc;")
for file in \$filelist;do
echo "RM file \$file"
rm \$file
psql -t "\${postgrescredentials}" -c "delete from \${tablename} where
path = '\${file}';"
done
done

```

Check how many seconds a webservice is behind current date
----------------------------------------------------------

```
/bin/bash -c datasetdate=\`curl -s
"http://geoservices.knmi.nl/cgi-bin/RADNL\_OPER\_R**\_25PCPRR\_L3.cgi?SERVICE=WMS&amp;VERSION=1.3.0&amp;REQUEST=GetCapabilities"
| sed -E 's/xmlns:/aaa/g' | sed -E 's/xlink:/aaa/g'| sed -E
's/xsi:/aaa/g' |sed -E 's/xmlns/aaa/g' | xmllint --shell -~~xpath
'(/WMS\_Capabilities/Capability/Layer/Layer)\[1\]/Dimension/@default'~~
| awk -F\\" 'NR % 1 == 0 { print \$2 }' | xargs date +%s ~~d\` &&
currentdate=\`date +%s\` && echo \`expr \$datasetdate~~ \$currentdate\`
```

Or continuously:
```
while true; do datasetdate=\`curl -s
"http://geoservices.knmi.nl/cgi-bin/RADNL\_OPER\_R**\_25PCPRR\_L3.cgi?SERVICE=WMS&amp;VERSION=1.3.0&amp;REQUEST=GetCapabilities"
| sed -E 's/xmlns:/aaa/g' | sed -E 's/xlink:/aaa/g'| sed -E
's/xsi:/aaa/g' |sed -E 's/xmlns/aaa/g' | xmllint --shell -~~xpath
'(/WMS\_Capabilities/Capability/Layer/Layer)\[1\]/Dimension/@default'~~
| awk -F\\" 'NR % 1 == 0 { print \$2 }' | xargs date +%s ~~d\` &&
currentdate=\`date +%s\` && echo \`expr \$datasetdate~~ \$currentdate\`;
sleep 2; done
```

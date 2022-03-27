Install Adaguc on Ubuntu Old
============================

Installation instructions for Ubuntu 15.04
------------------------------------------

```
sudo apt-get install mercurial
sudo apt-get install build-essential
sudo apt-get install libcurl4-openssl-dev libcairo2-dev libxml2-dev
libgd2-xpm-dev
sudo apt-get install libudunits2-dev udunits-bin
sudo apt-get install sqlite3 libsqlite3-dev
sudo apt-get install netcdf-bin libnetcdf-dev libhdf5-dev
sudo apt-get install libproj-dev
sudo apt-get install libgdal-dev

cd \~
hg clone https://dev.knmi.nl/hg/adagucserver
cd adagucserver
bash compile.sh

\#Done!
```

Full Installation instructions for xubuntu-14.04.2-desktop-amd64
----------------------------------------------------------------

### Install packages using the package manager

```
sudo apt-get install vim
sudo apt-get install kate kwrite konsole
sudo apt-get install postgresql
sudo apt-get install libcurl4-openssl-dev libcairo2-dev libxml2-dev
libgd2-xpm-dev postgresql-server-dev-all postgresql-client
sudo apt-get install mercurial
sudo apt-get install libudunits2-dev udunits-bin
sudo apt-get install php5
sudo apt-get install php5-gd
sudo apt-get install g**
sudo apt-get install m4
sudo apt-get install sqlite3 libsqlite3-dev
sudo apt-get install ncview
```

### Setup postgresql and create a database

```

\#\#\# Setup postgres for adaguc: \#\#\#
sudo -u postgres createuser --superuser adaguc
sudo -u postgres psql postgres
\\password adaguc
\\q

1.  note: type adaguc as password, when finished press \\q to exit.

createdb adaguc
```

### Setup directories (/data/)

```
\#Setup directories under /data/
sudo mkdir /data
sudo chown adaguc /data
mkdir /data/software/
mkdir -p /data/www/htdocs
mkdir -p /data/services/cgi-bin
mkdir /data/tmp
chmod 777 /data/tmp
mkdir /data/log
chmod 777 /data/log
```

### Setup apache www server

```

\#\#\# setup apache configuration point to /data/www/ directories \#\#\#

sudo vi /etc/apache2/sites-enabled/000-default.conf

&lt;VirtualHost \*:80&gt;
ServerAdmin webmaster@localhost

DocumentRoot /data/www/htdocs
&lt;Directory /&gt;
Options FollowSymLinks
AllowOverride None
&lt;/Directory&gt;
&lt;Directory /data/www/htdocs/&gt;
Options Indexes FollowSymLinks MultiViews
AllowOverride None
Order allow,deny
allow from all
&lt;/Directory&gt;

ScriptAlias /cgi-bin/ /data/services/cgi-bin/
&lt;Directory "/data/services/cgi-bin"&gt;
AllowOverride None
Options +ExecCGI -MultiViews +FollowSymLinks
Order allow,deny
Allow from all
&lt;/Directory&gt;

ErrorLog \${APACHE\_LOG\_DIR}/error.log

\# Possible values include: debug, info, notice, warn, error, crit,
\# alert, emerg.
LogLevel warn

CustomLog \${APACHE\_LOG\_DIR}/access.log combined
&lt;/VirtualHost&gt;

\#In /etc/apache2/apache2.conf, change /var/www to /data
sudo vi /etc/apache2/apache2.conf

\#Enable CGI mods
sudo cp /etc/apache2/mods-available/cgi\* /etc/apache2/mods-enabled/

\#Restart the service
sudo apache2ctl restart

1.  In order to test whether CGI scripts are functioning, place the
    following file in /data/services/cgi-bin/ with name helloworld.cgi

\#!/bin/bash
echo "Content-type: text/html"
echo ''
echo Hello world!

\#Make this file executable
chmod +x /data/services/cgi-bin/ helloworld.cgi

\#Check if only "Hello world!" is displayed in a web browser:
http://localhost/cgi-bin/helloworld.cgi
```

### Install libraries from source (HDF5, NetCDF4, Proj, GDAL)

```

\#\#\# Install latest hdf,netcdf and gdal libraries \#\#\#

export CPPFLAGS="-I/data/build/include/"
export LDFLAGS="-L/data/build/lib/"
export LD\_LIBRARY\_PATH="/data/build/lib/:\$LD\_LIBRARY\_PATH"
export PATH="/data/build/bin/:\$PATH"

\#You can add these exports to the .bashrc file

\#HDF5
cd /data/software
wget
http://www.hdfgroup.org/ftp/HDF5/current/src/hdf5-1.8.15-patch1.tar
tar -xvf hdf5-1.8.15-patch1.tar.gz
cd hdf5-1.8.15-patch1/
./configure --prefix=/data/build
make
make install

\#NetCDF4
cd /data/software
wget ftp://ftp.unidata.ucar.edu/pub/netcdf/netcdf-4.3.3.1.tar.gz
tar -xzvf netcdf-4.3.3.1.tar.gz
cd netcdf-4.3.3.1
./configure --prefix=/data/build
make
make install

\#Proj4
cd /data/software/
wget http://download.osgeo.org/proj/proj-4.9.1.tar.gz
tar -xzvf proj-4.9.1.tar.gz
cd proj-4.9.1
./configure --prefix=/data/build
make
make install

\#GDAL
cd /data/software
wget http://download.osgeo.org/gdal/1.11.2/gdal-1.11.2.tar.gz
tar -xzvf gdal-1.11.2.tar.gz
./configure --prefix=/data/build
make
make install
```

### Install ADAGUC

After this procudere has been followed, ADAGUC can be installed in the
following way:
```

\#\#\# Install adaguc server: \#\#\#
cd /data/software/
hg clone http://dev.knmi.nl/hg/adagucserver
cd adagucserver
bash compile.sh
cp ./bin/\* /data/build/bin/

\#Install adaguc viewer
cd /data/www/htdocs/
hg clone http://dev.knmi.nl/hg/adagucviewer

\#visit http://localhost/adagucviewer/ with a web browser
```

Complete, you have installed the ADAGUC software suite!

Create a sharedfolder in virtualbox
-----------------------------------

This enables data sharing between the host and guest system.

**On the host system**

-   Go to Devices/Shared Folders settings...
-   Add a "Machine folder" which points to a directory you wish to share
    and give it the Folder name "vboxshare"
-   Enable Auto-mount and Make permanent

**On the guest system**
```
mkdir /data/vboxshare
sudo mount -t vboxsf vboxshare /data/vboxshare
```

You can now share files between the host and guest systems

Old Installation instructions for xubuntu 11.10
===============================================

```
sudo apt-get install vim
sudo apt-get install kate kwrite konsole
sudo apt-get install virtualbox-guest-additions virtualbox-guest-x11
virtualbox-guest-utils virtualbox-guest-source virtualbox-guest-dkms
virtualbox-guest-additions-iso
sudo apt-get install postgresql
sudo apt-get install libcurl4-openssl-dev libcairo2-dev libxml2-dev
libgd2-xpm-dev libproj-dev postgresql-server-dev-all postgresql-client
sudo apt-get install mercurial
sudo apt-get install libudunits2-dev udunits-bin
sudo apt-get install php5
sudo apt-get install php5-gd

\#Setup postgres for adaguc:
sudo -u postgres createuser --superuser adaguc
sudo -u postgres psql postgres
\\password adaguc \# type adaguc as password, when finished press \\q to
exit.
\\q

createdb adagucdemo

\#Setup directories under /data/
sudo mkdir /data
sudo chown adaguc /data
mkdir /data/software/
mkdir -p /data/www/htdocs
mkdir -p /data/www/cgi-bin
mkdir /data/tmp
chmod 777 /data/tmp
mkdir /data/log
chmod 777 /data/log

\#Install latest hdf,netcdf and gdal libraries

export CPPFLAGS="-I/data/build/include/"
export LDFLAGS="-L/data/build/lib/"
export LD\_LIBRARY\_PATH="/data/build/lib/:\$LD\_LIBRARY\_PATH"
export PATH="/data/build/bin/:\$PATH"

\#You can add these exports to the .bashrc file

\#HDF5
cd /data/software
wget http://www.hdfgroup.org/ftp/HDF5/current/src/hdf5-1.8.11.tar.gz
tar -xzvf hdf5-1.8.11.tar.gz
cd hdf5-1.8.11/
./configure --prefix=/data/build
make
make install

\#NetCDF4
cd /data/software
wget
http://www.unidata.ucar.edu/downloads/netcdf/ftp/netcdf-4.3.0.tar.gz
tar -xzvf netcdf-4.3.0.tar.gz
cd netcdf-4.3.0/
./configure --prefix=/data/build --enable-netcdf-4
make
make install

\#GDAL
cd /data/software
wget http://download.osgeo.org/gdal/1.10.0/gdal-1.10.0.tar.gz
tar -xzvf gdal-1.10.0.tar.gz
\#Install GDAL ADAGUC driver (optional)
cd gdal-1.10.0/frmts/netcdf
wget
http://trac.osgeo.org/gdal/raw-attachment/wiki/ADAGUC/GDAL\_ADAGUC\_source\_v0.3.tar.gz
tar -xzvf GDAL\_ADAGUC\_source\_v0.3.tar.gz
mv GDAL\_ADAGUC\_source\_v0.3/\* .
\#vi GNUMakefile and add adagucdataset.o to the OBJ list
vi /data/software/gdal-1.10.0/frmts/gdalallregister.cpp
\# add GDALRegister\_ADAGUC(); between GMT and NetCDF drivers
vi /data/software/gdal-1.10.0/gcore/gdal\_frmts.h
\# add void CPL\_DLL GDALRegister\_ADAGUC(void); between GMT and NetCDF
drivers
\#Continue compiling GDAL
cd /data/software/gdal-1.10.0/
./configure --prefix=/data/build LIBS="-ludunits2"

make
make install

1.  Setup Apache www server
2.  Configure /etc/apache2/sites-enabled/000-default to point to
    /data/www/htdocs and /data/www/cgi-bin
    sudo apache2ctl restart

\#\#\# The environment has now been setup completely for the ADAGUC
installation \#\#\#

```

After this procudere has been followed, ADAGUC can be installed in the
following way:

```
\#Install adaguc server:
cd /data/software/
hg clone http://dev.knmi.nl/hg/adagucserver
cd adagucserver
bash compile.sh

\#Install adaguc viewer
cd /data/www/htdocs/
hg clone http://dev.knmi.nl/hg/adagucviewer

\#visit http://localhost/adagucviewer/ with a web browser
```

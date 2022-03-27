Preinstalled virtual environment 2015
=====================================

Preinstalled virtual environment
================================

An image of a virtual machine is available which can be installed to use
the software directly. The image can be downloaded from:

-   http://geoservices.knmi.nl/adagucworkshop/adagucvm-20150616.ova
    (9.1Gb)

The image can be used inside Virtualbox. Virtualbox is available from
https://www.virtualbox.org/. You need both Virtualbox and the virtualbox
extensionpack:

-   https://www.virtualbox.org/wiki/Downloads

You can see the installation procedure of ADAGUC on ubuntu on this page:
[Install Adaguc on Ubuntu](Install Adaguc on Ubuntu.md)

When virtualbox is installed, you can select "Import appliance" and
select the image.

By default 1536Mb of ram and 2 CPU cores are assigned to the VM, this is
enough to run the ADAGUC software, but increasing the amount of ram will
result in a better experience.

Logging in
----------

The user is "adaguc" the password is "adaguc", root password is "adaguc"

Everything is installed under /data/

All services are available under /data/services and all example data is
stored under /data/services/data.

The datasets used in this VM are also available via
http://opendap.knmi.nl/knmi/thredds/ADAGUC.html

Mounting a shared folder
------------------------

On your host machine, create a shared folder option via
Devices-&gt;Shared folders settings...
On your client machine create a directory you wish to mount. This should
be an empty directory.
On your client machine give the command:
```
\#sudo mount -t vboxsf &lt;mount name&gt; &lt;folder name&gt;
sudo mount -t vboxsf vboxshare /data/vboxshare
```
Now you can share data between the host and client.

Updating the software (optional)
--------------------------------

The image contains probably outdated ADAGUC software. The following
procedure updates the software to the latest version:

**Viewer update**
```
cd /data/www/htdocs/adagucviewer/
hg pull
hg update
```

The viewer is now updated to the latest version. When visiting the
viewer using a browser it is possible that certain files are still kept
in the browsers cache. Double press F5 (reload) to refresh all files.

**Server update**
```
cd /data/software/adagucserver/
hg pull
hg update
bash compile.sh
```

The server is now updated to the latest version.

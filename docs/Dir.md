Dir (basedir,prefix)
====================

Directory to read netcdf files from to create WMS services from netcdf
files on the fly.

-   basedir - The server cannot read outside this path, but can only
    descend. The server is locked into this path. Realpath is used for
    checks, symbolic links are not followed.
-   prefix - The part that will be removed from the path for external
    presentation.

Multiple Dir elements are allowed.

For example:
```
&lt;AutoResource enableautoopendap="false" enablelocalfile="false"
enablecache="false" &gt;
&lt;Dir basedir="/data/sdpkdc/" prefix="/data/sdpkdc/"/&gt;
&lt;Dir basedir="/data/omi/" prefix="/data/omi/"/&gt;
&lt;/AutoResource&gt;
```

-   See [AutoResource](AutoResource.md)


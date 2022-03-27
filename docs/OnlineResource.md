OnlineResource (value)
======================

Sets the external location of the server. There are three options to
configure this:

1). Specify the full path in the configuration:
```
&lt;OnlineResource
value="http://yourserver/cgi-bin/adagucserver.cgi?"/&gt;
```

2). Specify the suffix, the server will prepend the HTTP\_HOST
environment variable for you:
```
&lt;OnlineResource value="/cgi-bin/adagucserver.cgi?"/&gt;
```

3). Specify it in the environment via ADAGUC\_ONLINERESOURCE
You can leave out the OnlineResource and specify it as environment
variable ADAGUC\_ONLINERESOURCE in the cgi shell script.
```
export
ADAGUC\_ONLINERESOURCE="http://yourserver/cgi-bin/adagucserver.cgi?"
```

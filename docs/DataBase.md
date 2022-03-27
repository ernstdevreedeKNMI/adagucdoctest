DataBase (dbtype,parameters, maxquerylimit)
===========================================

Configuration to access a PostgreSQL or SQLite database, for example:

``` &lt;DataBase maxquerylimit="365"
parameters="dbname=thedatabase host=thehostname user=theuser
password=asecretpassword"/&gt;```

``` &lt;DataBase dbtype="sqlite"
parameters="databasefile.db"/&gt;```

-   dbtype can be either sqlite or postgresql. Default is postgresl
-   parameters are the database parameters required for making the
    connection
-   maxquerylimit is the maximum number of results for a getfeatureinfo
    call.


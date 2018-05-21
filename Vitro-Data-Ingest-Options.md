_Note these are not in any order of preference_

## 1. Load data using the `SparqlUpdate` API

The Vitro `SparqlUpdateApi` code is accessible via a tomcat servlet that takes a request with an update param. The request string is literally the `update=INSERT DATA {}` wrapper syntax for the inserted triples. The `SparqlUpdateApiController` class takes the value of update as a string and performs the update using the Jena Sparql api.

**Sample code:**

```
vitro/api/src/main/java/edu/cornel /mannlib/vitro/webapp/controller/api/SparqlUpdateApiController.java
```

## 2. Load data using Vitro data loading abstractions (TDB Java API).

This would involve modifying or extending the Vitro code that controls how data gets loaded into Vitro via the webapp, or using them as guides. The data is loaded from dataset files.

https://jena.apache.org/documentation/tdb/java_api.html
https://jena.apache.org/documentation/tdb/tdb_transactions.html

**Sample code:**

https://github.com/vivo-project/Vitro/blob/608aa1cf54648f35045eb1ec717b143269b11273/api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/adapters/RDFServiceBulkUpdater.java

## 3. Jena SPARQL Update API (ARQ: direct loading via SPARQL not http)

https://jena.apache.org/documentation/query/update.html
https://jena.apache.org/documentation/query/cmds.html

**Sample code:**

https://github.com/vivo-project/Vitro/blob/608aa1cf54648f35045eb1ec717b143269b11273/api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/adapters/SparqlBulkUpdater.java

https://github.com/wcmc-its/vivo-import-data/blob/667b21adeb4d9d67e2909449dee9be48e7df0972/vivo-import-data/src/main/java/org/vivoweb/harvester/util/repo/JenaConnect.java

https://github.com/wcmc-its/vivo-import-data/blob/master/vivo-import-data/src/main/java/org/vivoweb/harvester/ingest/AcademicFetchFromED.java

## 4. Jena SDB (JDBC) Connection.

See: https://github.com/wcmc-its/vivo-import-data/blob/28e43203c8414e7f51446b60cbbc9e36ca92b024/README.md#using-sdbjenaconnect-to-import-data-into-vivo

**Sample code:**

https://github.com/wcmc-its/vivo-import-data/blob/master/vivo-import-data/src/main/java/org/vivoweb/harvester/connectionfactory/JenaConnectionFactory.java

## 5. Load data as a filegraph

Anything put in the `abox/firsttime` or `tbox/firsttime` directories will get loaded into the store the first time (hence the name) - i.e. when those models are empty or on startup. The obvious downfall here is that it would require an application restart every time we want the data loaded.

## 6. Use Jena Tdbloader

Use Jena's command line tool to load files directly and efficiently into a TDB-back model. Tdbloader2 can only be used to create a database.

https://jena.apache.org/documentation/tdb/commands.html

The directory of the TDB database is one of these(?)
```
/usr/local/vivo/home> ls -ld tdb*
drwxr-x---  31 jgreben  admin  992 May  8 15:51 tdbContentModels
drwxr-x---  31 jgreben  admin  992 May  7 22:28 tdbModels
```

## 7. Fuseki

Fuseki is a SPARQL server. It provides REST-style SPARQL HTTP Update, SPARQL Query, and SPARQL Update using the SPARQL protocol over HTTP. This would be similar to loading data via the Vitro sparql api without using Vitro...

https://jena.apache.org/documentation/serving_data/

## Other concerns

### Global Stop of Indexer
 - Globally stop or pause the indexer when bulkloading. This appears in the `/usr/share/tomcat/logs/vitro.all.log` as records are being loaded one at a time:
```
...
2018-05-15 16:37:21,950 INFO  [IndexHistory] PAUSE, 5/15/18 4:24 PM, []
2018-05-15 16:37:21,964 INFO  [IndexHistory] UNPAUSE, 5/15/18 4:24 PM, []
2018-05-15 16:37:22,053 INFO  [IndexHistory] PAUSE, 5/15/18 4:24 PM, []
2018-05-15 16:37:22,067 INFO  [IndexHistory] UNPAUSE, 5/15/18 4:24 PM, []
...
```

### Notes on Accessing Jena Directly

> Re: accessing Jena directly:
>
> The Vitro java code ^^ is accessible via a tomcat servlet that takes a request with an update param. The request string is literally the update=INSERT DATA {} wrapper syntax for the inserted triples. The SparqlUpdateApiController.java class takes the value of update as a string and sends that to a Jena library class to perform the update.
>
> Basically I think that hacking the java code to load data will only buy us the avoidance of passing a potentially large string over http to the tomcat servlet and it's associated class. The largeness of the string is not really a major issue because tomcat can be configured to handle large post requests with the maxPostSize connector attribute and additional tomcat tuning.
>
> Otherwise, we could probably write a java wrapper class to call the SparqlUpdateApiController with the same update string as an argument, but I'm not so sure that seeking to avoiding the servlet layer will give us much of a serious performance boost. It would probably be better to just tune tomcat to be performant in case we run into issues.

### Index / Derivative Datastore

From Huda at Cornell:

> We should also keep in mind that at Cornell, when they do an update they do have to stop things for some hours, and there's also search index rebuilding time to take into account.

### TDB vs SDB

From Jim Blake at Cornell:

> Configuring Vitro to use Jena TDB is easy (applicationSetup.n3)
>
> There are good reasons to use Jena TDB instead of Jena SDB. TDB might well be the best choice. Don’t know.
>
> For standard VIVO installation, Jena SDB is still the default.
>
> I don’t know of anyone who is using Vitro or VIVO in production with a large triple-store based on Jena TDB – the community will not be able to provide input with regard to performance or reliability.
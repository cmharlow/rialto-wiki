## 1. Load data using the sparqlUpdate api

The Vitro `SparqlUpdateApi` code is accessible via a tomcat servlet that takes a request with an update param. The request string is literally the `update=INSERT DATA {}` wrapper syntax for the inserted triples. The `SparqlUpdateApiController` class takes the value of update as a string and performs the update using the Jena Sparql api.

`Vitro/api/src/main/java/edu/cornell/mannlib/vitro/webapp/controller/api/SparqlUpdateApiController.java`

## 2. Load data using Vitro data loading abstractions, or Jena Connection.

This would involve hacking, modifying, or wrapping the Vitro code that controls how data gets loaded into Vitro using the webapp features. The data is loaded from files instead of strings.

Sample code:

https://github.com/vivo-project/Vitro/tree/608aa1cf54648f35045eb1ec717b143269b11273/api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/adapters

(Note: the following approach loads data using SDB via jdbc)

See: https://github.com/wcmc-its/vivo-import-data/blob/28e43203c8414e7f51446b60cbbc9e36ca92b024/README.md#using-sdbjenaconnect-to-import-data-into-vivo

https://github.com/wcmc-its/vivo-import-data/blob/master/vivo-import-data/src/main/java/org/vivoweb/harvester/connectionfactory/JenaConnectionFactory.java

### Jena Spaqrql Update API (direct loading via sparql, i.e. not via http)
Sample code:

https://github.com/wcmc-its/vivo-import-data/blob/master/vivo-import-data/src/main/java/org/vivoweb/harvester/ingest/AcademicFetchFromED.java

https://github.com/wcmc-its/vivo-import-data/blob/667b21adeb4d9d67e2909449dee9be48e7df0972/vivo-import-data/src/main/java/org/vivoweb/harvester/util/repo/JenaConnect.java

## 3. Load data as a filegraph
Anything put in the `abox/firsttime` or `tbox/firsttime` directories will get loaded into the store the first time (hence the name) - i.e. when those models are empty or on startup. The obvious downfall here is that it would require an application restart every time we want the data loaded.
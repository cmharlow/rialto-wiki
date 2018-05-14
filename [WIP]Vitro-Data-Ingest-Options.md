## 1. Load data using the sparqlUpdate api

## 2. Load data using Vitro data loading abstractions, or Jena Connection.

Sample code:

https://github.com/vivo-project/Vitro/blob/4859eb7da1fabb5a3e091f5d08495e28e4017b79/api/src/main/java/edu/cornell/mannlib/vitro/webapp/controller/jena/RDFUploadController.java

https://github.com/vivo-project/Vitro/blob/4859eb7da1fabb5a3e091f5d08495e28e4017b79/api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/adapters/RDFServiceBulkUpdater.java

https://github.com/wcmc-its/vivo-import-data/blob/master/vivo-import-data/src/main/java/org/vivoweb/harvester/connectionfactory/JenaConnectionFactory.java

### Jena Spaqrql Update API (direct loading via sparql, i.e. not via http)
Sample code:

https://github.com/wcmc-its/vivo-import-data/blob/master/vivo-import-data/src/main/java/org/vivoweb/harvester/ingest/AcademicFetchFromED.java

https://github.com/wcmc-its/vivo-import-data/blob/667b21adeb4d9d67e2909449dee9be48e7df0972/vivo-import-data/src/main/java/org/vivoweb/harvester/util/repo/JenaConnect.java

## 3. Load data as a filegraph
Anything put in the `abox/firsttime` or `tbox/firsttime` directories will get loaded into the store the first time (hence the name) - i.e. when those models are empty or on startup. The obvious downfall here is that it would require an application restart every time we want the data loaded.
This document describes how we load data into Vitro using the TDB Java API. The solution described below is effectively a Java-based version of using the tdbloader command line tool.

See generally https://jena.apache.org/documentation/tdb/java_api.html

For expediency, we wrote a Java class within our forked Vitro:

https://github.com/sul-dlss-labs/Vitro/blob/73-tdb-load/rialto/src/main/java/edu/stanford/RialtoLoad.java

The RialtoLoad class is set up to load each file in our sample data directory into Vitro's TDB instance. Note that it uses the TDB API to accomplish this, and not going via Vitro itself. Also note that it uses Jena transactions to accomplish the work.

To run this Java program on the server, follow these steps.

1. Stop Tomcat: `sudo services stop tomcat`
2. Clear out Vitro's TDB content directory: `rm -f /opt/app/vitro/home/tdbContentModels/*`
3. If necessary, deploy the branch `73-tdb-load` to the server.
4. `cd /opt/app/vitro/current/rialto`
5. Run the code on the test data using `java -jar lib/vitro-rialto-1.9.3-jar-with-dependencies.jar /opt/app/vitro/home/tdbContentModels   /opt/app/vitro/data/rialto-sample-data/vivo/agents` 


# How Vitro loads data using the Jena API (background information)
This class parameterizes the TDB directory on the server:
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/triplesource/impl/tdb/ContentTripleSourceTDB.java`

This class creates the Jena Model, locks it, and applies the dataset changes to it and does other model operations:
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/impl/jena/RDFServiceJena.java`

This class initializes the Jena Dataset, kicks off the update, and notifies the listeners of changes
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/impl/jena/tdb/RDFServiceTDB.java`

# Findings

After running the load, Vitro could no longer write to TDB due to a `BlockAccessBase: Bounds exception` (same as the `tdbloader` load). Restarting Tomcat restores Vitro's connection to its TDB database.

The team dismissed TDB Jena API as an ingest/load mechanism. The documentation of TDB is clear that it wasn't designed for multi-JVM usage. The team is not going to use TDB Jena API partly because needing to restart the server is an undesirable hack, but mostly because there is a risk that writing data this way while Vitro is also writing to TDB will cause data corruption, necessitating a wipe and full reload. 

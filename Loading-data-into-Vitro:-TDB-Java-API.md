This document describes how we load data into Vitro using the TDB Java API.

See generally https://jena.apache.org/documentation/tdb/java_api.html

# How Vitro loads data using the Jena API
This class parameterizes the TDB directory on the server:
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/triplesource/impl/tdb/ContentTripleSourceTDB.java`

This class creates the Jena Model, locks it, and applies the dataset changes to it and does other model operations:
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/impl/jena/RDFServiceJena.java`

This class initializes the Jena Dataset, kicks off the update, and notifies the listeners of changes
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/impl/jena/tdb/RDFServiceTDB.java`

# How to load data using the Jena TDB API
For expediency, we wrote a Java class within our forked Vitro:

https://github.com/sul-dlss-labs/Vitro/blob/73-tdb-load/rialto/src/main/java/edu/stanford/RialtoLoad.java

The RialtoLoad class is set up to load each file in our sample data directory into Vitro's TDB instance. Note that it uses the TDB API to accomplish this, and not going via Vitro itself.

# How we can load data using the Jena API or Vitro's existing classes
## Extending or wrapping the Vitro API Classes to Ingest our data
### Maybe this is crazy talk, but could we...?
1. Write a main class as part of the Vitro API package to handle our data input from the command line and apply that incoming data to the existing classes and methods, avoiding and re-writing anything to do with the webapp
1. Get it installed using Maven to produce a JAR
1. Load the data directly using the JAR from the command line...

## Writing a Vitro-external Class 
This will be very similar in result to using the [tdbloader](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-tdbloader). The tdbloader is a command-line utility that encapsulates a Jena ReadWrite transaction with TDB, but we can write our own if necessary.


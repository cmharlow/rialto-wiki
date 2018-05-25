This document describes how we load data into Vitro using the TDB Java API.

See generally https://jena.apache.org/documentation/tdb/java_api.html

# How Vitro loads data using the Jena API
This class parameterizes the TDB directory on the server:
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/triplesource/impl/tdb/ConfigurationTripleSourceTDB.java`

This class creates the Jena Model, locks it, and applies the dataset changes to it and does other model operations:
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/impl/jena/RDFServiceJena.java`

This class initializes the Jena Dataset, kicks off the update, and notifies the listeners of changes
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/impl/jena/tdb/RDFServiceTDB.java`

# How we can load data using the Jena API or Vitro's existing classes
## Writing a Vitro-external Class 
This will be very similar in result to using the [tdbloader](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-tdbloader). The tdbloader is a command-line utility that encapsulates a Jena ReadWrite transaction with TDB, but we can write our own if necessary.
This document describes how we load data into Vitro using the TDB Java API.

See generally https://jena.apache.org/documentation/tdb/java_api.html

# How Vitro loads data using the Jena API
This class parameterizes the TDB directory on the server:
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/triplesource/impl/tdb/ConfigurationTripleSourceTDB.java`

This class creates the Jena Model, locks it, and applies the dataset changes to it and does other model operations:
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/impl/jena/RDFServiceJena.java`

This class...
`api/src/main/java/edu/cornell/mannlib/vitro/webapp/rdfservice/impl/jena/tdb/RDFServiceTDB.java` 
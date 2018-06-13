[Apache TDB](https://jena.apache.org/documentation/tdb/) is a storage component of Apache Jena. It is one of four options for the persistence layer of Vitro<sup name="a1">[1](#f1)</sup>. TDB's major shortcoming is that it can only be accessed by a single JVM at a time or corruption of the data will occur. Since Vitro accesses TDB in its own JVM, it is not possible to load data into the same TDB instance from a second JVM while Vitro is running<sup name="a2">[2](#f2)</sup>. TDB exposes no external (network) APIs that we can leverage; it was built to be accessed by a single application. TDB works best as the datastore for a standalone application not as a component in a system.

[Apache Fuseki](https://jena.apache.org/documentation/fuseki2/) is a SPARQL server that provides (network) APIs atop TDB. This would be one way to share a single TDB datastore with multiple applications. Fuseki's APIs are built to support multiple consumers at once<sup name="a3">[3](#f3)</sup>; it does not share TDB's multi-JVM restriction. However, Fuseki + TDB doesn't provide for horizontal scalability with writes/updates.

[Blazegraph](https://www.blazegraph.com/) is a standalone triple store with several external (network) APIs that support multiple consumers at once. It is known for being among the fastest triplestores with an available GPU accelerator. It can support "big data"-scale data sets. Blazegraph was acqui-hired by Amazon in 2016 and the developers of Blazegraph went on to produce [Amazon Neptune](https://aws.amazon.com/neptune/). Blazegraph is still available for download but development on it has been at a virtual standstill. The Wikimedia foundation selected Blazegraph for their [Wikidata query service (WDQS)](https://query.wikidata.org/).

# Notes

<b name="f1">1.</b> The other three are: 
* SDB, another Apache triplestore that most of the VIVO community uses despite it being well past end of life; 
* SPARQL endpoint, which we used in [another test](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Fuseki-HTTP-SPARQL-Update-API); and
* Virtuoso, which we did not test. 

<b name="f2">2.</b> The [TDB](https://jena.apache.org/documentation/tdb/tdb_transactions.html#multi-jvm) [documentation](https://jena.apache.org/documentation/tdb/faqs.html#multi-jvm) backs this up unequivocally. [↩](#a2)

<b name="f3">3.</b> We ran a separate [load test using Vitro backed by Fuseki](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Fuseki-HTTP-SPARQL-Update-API). [↩](#a3)
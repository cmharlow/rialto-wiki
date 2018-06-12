## Purpose of this Work

As part of assessing Vitro, we need to:

1. test the scalability of Vitro (and, by extension, VIVO) for RIALTO type data and RIALTO phase 1 amounts of data.
2. ease [and cost time-wise] to work, develop, maintain Vitro
    * Take any info from what we’ve learned in the scaling questions
    * Highlight any open questions about Vitro [VIVO] usage
3. If Vitro scales adequately, Vitro vs VIVO
    * Driven by data modeling
    * Driven by the ease of usage / cost of usage

## Vitro Performance Assessment Matrix

Tests for assessing performance of Vitro (or other identified future options) as the canonical RIALTO data store. Options listed in priority order, starred tests being the preferences for testing. Standard loading of 4,596,065 triples from 73,479 n-triples files.

* inf == inferencing (within Vitro)
* index == indexing (within Vitro, default mappings to Solr)
* :star: == primary foci

Vitro Ingest                | no inf & no index    | inf & no index       | no inf & index :star:  | inf & index :star:
--------------------------- | -------------------- | -------------------- | ---------------------- | --------
1 [SPARQL Update API](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-SPARQL-Update-API) (Vitro)        | Unable to run w/Vitro | Unable to run w/Vitro | [Docs](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-SPARQL-Update-API),  [Metrics](https://sulstats.stanford.edu/dashboard/db/servers?from=1527133800000&to=1527153600000&var-department=dlss&var-project=rialto&var-server=rialto-vitro-dev&theme=light) | [Docs](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-SPARQL-Update-API),  [Metrics TBD]() 
2 [Jena tdbloader](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-tdbloader) (cmd line) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-tdbloader#findings) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-tdbloader#findings) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-tdbloader#findings) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-tdbloader#findings) 
3 [TDB Java API](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-TDB-Java-API) (Vitro)      | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-TDB-Java-API#findings) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-TDB-Java-API#findings) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-TDB-Java-API#findings) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-TDB-Java-API#findings)
4 [Jena SPARQL Update (ARQ)](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-SPARQL-Update-(ARQ))  | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-SPARQL-Update-(ARQ)#findings) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-SPARQL-Update-(ARQ)#findings) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-SPARQL-Update-(ARQ)#findings) | [Dismissed](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Jena-SPARQL-Update-(ARQ)#findings)  
5 [Fuseki SPARQL Update API](https://github.com/sul-dlss/rialto/wiki/Loading-data-into-Vitro:-Fuseki-HTTP-SPARQL-Update-API#findings) | n/a | n/a | n/a | n/a

## Metrics gathered for each case:
- Sample Data Load Times
  - Total time to load all sample data
  - Time per RDF record / file
  - Time per request (if multiple requests, i.e., HTTP)
  - Scaling graph based on the above
- Sample Data Index Times (if indexing)
- Ops Metrics: (taken from https://sulstats.stanford.edu/dashboard/db/servers)
  - CPU usage
  - memory usage
  - overall load
  - swap usage
  - perhaps an I/O-related metric would be good too
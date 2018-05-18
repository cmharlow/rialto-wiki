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

Tests for assessing performance of Vitro (or other identified future options) as the canonical RIALTO data store. Options listed in priority order, starred tests being the preferences for testing.

* inf == inferencing (within Vitro)
* index == indexing (within Vitro, default mappings to Solr)
* :star: == primary foci

Vitro Ingest                | no inf & no index    | inf & no index       | no inf & index :star:  | inf & index :star:
--------------------------- | -------------------- | -------------------- | ---------------------- | --------
1 SPARQL API (Vitro)        | [Blocked](https://github.com/sul-dlss/rialto/issues/53) [Metrics](TBD) | [Blocked](https://github.com/sul-dlss/rialto/issues/54) [Metrics](TBD) | [In progress](https://github.com/sul-dlss/rialto/issues/50) [Metrics](https://sulstats.stanford.edu/dashboard/db/servers?from=1526619600000&to=1526655600000&var-department=dlss&var-project=rialto&var-server=rialto-vitro-dev&theme=light) | [Ready](https://github.com/sul-dlss/rialto/issues/51) [Metrics](TBD)
2 Jena TDBLoader (cmd line) | [Blocked](https://github.com/sul-dlss/rialto/issues/66) | [Blocked](https://github.com/sul-dlss/rialto/issues/67) | [Blocked](https://github.com/sul-dlss/rialto/issues/55)   | [Blocked](https://github.com/sul-dlss/rialto/issues/56)
3 Jena SPARQL Update (ARQ)  | [Blocked](https://github.com/sul-dlss/rialto/issues/61) | Blocked              | [Ready](https://github.com/sul-dlss/rialto/issues/59)     | [Ready](https://github.com/sul-dlss/rialto/issues/60)
4 TDB Java API (Vitro)      | Blocked              | Blocked              | [Ready](https://github.com/sul-dlss/rialto/issues/63)     | [Ready](https://github.com/sul-dlss/rialto/issues/62)
5 [stretch] Fuseki SPARQL Update | n/a | n/a | n/a | n/a

## Metrics gathered for each case:
- Sample Data Load Times
  - Total time to load all sample data
  - Time per RDF record / file
  - Time per request (if multiple requests, i.e., HTTP)
  - Scaling graph based on the above
- Sample Data Index Times (if indexing)
- Ops Metrics:
  - CPU usage
  - memory usage
  - overall load
  - swap usage
  - perhaps an I/O-related metric would be good too

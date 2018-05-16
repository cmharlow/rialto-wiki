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

Vitro Ingest | full load w/o inferencing & w/o indexing | full load w/inferencing & w/o indexing | full load w/o inferencing & w/indexing :star: | full load w/inferencing & w/indexing :star:
---------------------------- | ------------- | ------------ | ----------- | --------
1 SPARQL API (Vitro)        | Blocked       | Blocked | Ready | Ready
2 Jena TDBLoader (cmd line) | Blocked       | Blocked | Open Q | Open Q
3 Jena SPARQL Update (ARQ)  | Ready (dev needed) | Ready (dev needed) | Ready (dev needed) | Ready (dev needed)
4 TDB Java API (Vitro)      | Ready (dev needed) | Ready (dev needed) | Ready (dev needed) | Ready (dev needed)
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

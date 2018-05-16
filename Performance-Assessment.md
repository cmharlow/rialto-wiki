Test matrix for assessing performance of Vitro (or other identified future options) as the canonical RIALTO data store:

Vitro Ingest | full load w/o inferencing & w/o indexing | full load w/inferencing & w/o indexing | full load w/o inferencing & w/indexing :star: | full load w/inferencing & w/indexing :star:
---------------------------- | ------------- | ------------ | -----------
1. SPARQL API (Vitro)        | Blocked       | Blocked | Ready | Ready
2. Jena TDBLoader (cmd line) | Blocked       | Blocked | Open Q | Open Q
3. Jena SPARQL Update (ARQ)  | Ready (dev needed) | Ready (dev needed) | Ready (dev needed) | Ready (dev needed)
4. TDB Java API (Vitro)      | Ready (dev needed) | Ready (dev needed) | Ready (dev needed) | Ready (dev needed)
5. [stretch] Fuseki SPARQL Update | n/a | n/a | n/a | n/a
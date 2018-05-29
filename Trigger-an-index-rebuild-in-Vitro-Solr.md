To rebuild the Vitro index, click the "Rebuild Search Index" link in the admin UI or hit it via https://rialto-vitro-dev.stanford.edu/vitro/SearchIndex?rebuild=1, but note that you can't just curl that URL because 1) you will be challenged by Shibboleth first, and then 2) you need to be logged in to Vitro.

To determine which URIs Vitro can "see" and will reindex, navigate to the [SPARQL query UI in Vitro](http://rialto-vitro-test/vitro/admin/sparqlquery) and issue the following query:

```sparql
SELECT DISTINCT ?ind WHERE {
  { ?ind <http://www.w3.org/2000/01/rdf-schema#label> ?label } UNION { GRAPH ?g { ?ind <http://www.w3.org/2000/01/rdf-schema#label> ?label } 
  FILTER (?g != <http://vitro.mannlib.cornell.edu/default/vitro-kb-applicationMetadata> && !regex(str(?g), "tbox"))
 } }
```
To rebuild the Vitro index, click the "Rebuild Search Index" link in the admin UI or hit it via https://rialto-vitro-dev.stanford.edu/vitro/SearchIndex?rebuild=1, but note that you can't just curl that URL because 1) you will be challenged by Shibboleth first, and then 2) you need to be logged in to Vitro.

To determine which URIs Vitro can "see" and will reindex, navigate to the [SPARQL query UI in Vitro](http://rialto-vitro-test/vitro/admin/sparqlquery) and issue the following query:

```sparql
SELECT DISTINCT ?ind WHERE {
  { ?ind <http://www.w3.org/2000/01/rdf-schema#label> ?label } UNION { GRAPH ?g { ?ind <http://www.w3.org/2000/01/rdf-schema#label> ?label } 
  FILTER (?g != <http://vitro.mannlib.cornell.edu/default/vitro-kb-applicationMetadata> && !regex(str(?g), "tbox"))
 } }
```

Here's what the Solr documents will look like:

```json
    {
        "DocId": "vitroIndividual:http://scholars.cornell.edu/individual/aao4",
        "THUMBNAIL_URL": "",
        "indexedTime": 1527620118647,
        "ALLTEXT": [
          "1000225 aao4"
        ],
        "mostSpecificTypeURIs": [
          "http://www.w3.org/2002/07/owl#Thing",
          "http://purl.obolibrary.org/obo/BFO_0000002",
          "http://purl.obolibrary.org/obo/BFO_0000001",
          "http://xmlns.com/foaf/0.1/Agent",
          "http://xmlns.com/foaf/0.1/Person",
          "http://purl.obolibrary.org/obo/BFO_0000004"
        ],
        "THUMBNAIL": "0",
        "URI": "http://scholars.cornell.edu/individual/aao4",
        "nameRaw": [
          "Ovaska, Arthur Alan",
          "[Ovaska, Arthur Alan]"
        ],
        "etag": "87cb70a8abcd0d86",
        "_version_": 1601825793621622800,
        "timestamp": "2018-05-29T18:55:18.719Z",
        "score": 1
      }
```
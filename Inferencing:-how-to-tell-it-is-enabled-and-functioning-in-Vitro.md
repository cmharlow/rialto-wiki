Use the Vivo sparql interface at https://rialto-vitro-dev.stanford.edu/vitro/admin/sparqlquery and enter the query:

> SELECT count(*)

> WHERE {
>   
>   GRAPH <http://vitro.mannlib.cornell.edu/default/vitro-kb-inf> { ?s ?p ?o }

> }

Or do `curl -i -d 'email=email@stanford.edu' -d 'password=Password' -d 'query=SELECT count(*) WHERE {GRAPH <http://vitro.mannlib.cornell.edu/default/vitro-kb-inf> { ?s ?p ?o }}' http://localhost:8080/vitro/api/sparqlQuery`

This will show the number of triples created by the inferencer.

See https://wiki.duraspace.org/display/VIVODOC19x/Graph+Reference
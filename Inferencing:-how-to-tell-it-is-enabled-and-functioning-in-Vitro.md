## Use the Vivo sparql interface 

Visit https://rialto-vitro-dev.stanford.edu/vitro/admin/sparqlquery and enter the query:

```
SELECT count(*)
WHERE {
  GRAPH <http://vitro.mannlib.cornell.edu/default/vitro-kb-inf> { ?s ?p ?o }
}
```

Or do `curl -i -d 'email=email@stanford.edu' -d 'password=Password' -d 'query=SELECT count(*) WHERE {GRAPH <http://vitro.mannlib.cornell.edu/default/vitro-kb-inf> { ?s ?p ?o }}' http://localhost:8080/vitro/api/sparqlQuery`

This will show the number of triples created by the inferencer.

See https://wiki.duraspace.org/display/VIVODOC19x/Graph+Reference

***

## Check the vitro logs

  a) `ksu` as root 

  b) `cd /usr/share/tomcat/logs`

  c) `grep "inference" vitro.all.log`


e.g.
```
[root@rialto-vitro-dev logs]# grep "inference" vitro.all.log*
vitro.all.log.7:2018-05-11 08:43:33,086 INFO  [SimpleReasonerSetup] starting ABox inference recompute in a separate thread.
vitro.all.log.7:2018-05-11 08:43:33,087 INFO  [ABoxRecomputer] Recomputing ABox inferences.
vitro.all.log.7:2018-05-11 08:43:33,144 INFO  [ABoxRecomputer] Recomputing inferences for 14 individuals
vitro.all.log.7:2018-05-11 08:43:33,304 INFO  [ABoxRecomputer] Finished recomputing inferences
```
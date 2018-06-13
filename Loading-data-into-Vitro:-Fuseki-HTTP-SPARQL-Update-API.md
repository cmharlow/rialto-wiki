This document describes how to load data into Vitro via HTTP SPARQL Update API when Vitro is configured to use a SPARQL endpoint as its data source.

1. Ensure Fuseki is installed and running.
2. See [this Wiki page](https://github.com/sul-dlss/rialto/wiki/Disable-enable-inferencing-at-startup) for information on how to turn inferencing on and off.
3. The original test triples are stored within `/opt/app/vitro/data/rialto-sample-data/vivo/agents/`. Run `nohup time fuseki_load.bash` to wrap these triples in SPARQL insert statements and load them into Vitro via Fuseki's HTTP SPARQL Update API.

# Note

By the time we ran the Fuseki load scenario, the RIALTO team determined that inferencing within the datastore was *not* necessary, so we turned it off for this test.

# Running Fuseki

Note: Fuseki must (at this time) be run in a console session as tomcat does not allow the order of applications startups to be set and when fuseki starts before vitro it fails to start.

1. login to the vitro development server
2. Move into the fuseki folder: `cd /opt/app/vitro/shared/apache-jena-fuseki-3.7.0`
3. Run the server with the `vitro` data set `./fuseki-server --loc=data --update /vitro`

# Findings

## Runtime

For the load into Fuseki:
```
real    47m23.597s
user    2m27.236s
sys     3m29.929s
```

For indexing into Vitro's Solr: TBD

## System Load

https://sulstats.stanford.edu/dashboard/db/servers?from=1528837925028&to=1528841525028&var-department=dlss&var-project=rialto&var-server=rialto-vitro-dev&theme=light

![](https://user-images.githubusercontent.com/131982/41320098-3f6139d4-6e53-11e8-8a98-64b28b61f574.png)

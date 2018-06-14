This document describes how to load data into Vitro via HTTP SPARQL Update API when Vitro is configured to use a SPARQL endpoint as its data source.

1. Ensure Fuseki is installed and running.
2. See [this Wiki page](https://github.com/sul-dlss/rialto/wiki/Disable-enable-inferencing-at-startup) for information on how to turn inferencing on and off.
3. The original test triples are stored within `/opt/app/vitro/data/rialto-sample-data/vivo/agents/`. `cd` to that directory and run `nohup time fuseki_load.bash *.sparql` to wrap these triples in SPARQL insert statements and load them into Vitro via Fuseki's HTTP SPARQL Update API.

# Note

By the time we ran the Fuseki load scenario, the RIALTO team determined that inferencing within the datastore was *not* necessary, so we turned it off for this test.

# Running Fuseki

For expediency's sake, we run Fuseki in a console session as tomcat does not allow the startup order of applications to be set and Vitro depends on Fuseki being present when it spins up.

1. Login to the vitro development server
2. Move into the fuseki folder: `cd /opt/app/vitro/shared/apache-jena-fuseki-3.7.0`
3. Run the server with the `vitro` data set `./fuseki-server --loc=data --update /vitro`

# Findings

## Runtime

Loading the sample dataset into Fuseki took 35 minutes to complete. 

Indexing the Fuseki data into Vitro's Solr index took 41 minutes to complete.

## System Load

https://sulstats.stanford.edu/dashboard/db/servers?from=1528994501301&to=1528999623587&var-department=dlss&var-project=rialto&var-server=rialto-vitro-dev&theme=light

![](https://user-images.githubusercontent.com/131982/41430777-d6d89956-6fc5-11e8-8dc0-dec4c799df08.png)

This document describes how to load data into Vitro via HTTP SPARQL Update API when Vitro is configured to use a SPARQL endpoint as its data source.

1. Ensure Fuseki is installed and running.
2. See [this Wiki page](https://github.com/sul-dlss/rialto/wiki/Disable-enable-inferencing-at-startup) for information on how to turn inferencing on and off.
3. The original test triples are stored within `/opt/app/vitro/data/rialto-sample-data/vivo/agents/`. Run `nohup time fuseki_load.bash` to wrap these triples in SPARQL insert statements and load them into Vitro via Fuseki's HTTP SPARQL Update API.

# Note

By the time we ran the Fuseki load scenario, the RIALTO team determined that inferencing within the datastore was *not* necessary, so we turned it off for this test.

# Findings

## Runtime

```
real    47m23.597s
user    2m27.236s
sys    3m29.929s
```

## System Load

https://sulstats.stanford.edu/dashboard/db/servers?from=1528837925028&to=1528841525028&var-department=dlss&var-project=rialto&var-server=rialto-vitro-dev&theme=light

![](https://user-images.githubusercontent.com/131982/41320098-3f6139d4-6e53-11e8-8a98-64b28b61f574.png)

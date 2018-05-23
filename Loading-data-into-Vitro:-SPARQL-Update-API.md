This document describes how we load data into Vitro using its SPARQL Update API.

1. Stop Tomcat with `sudo service tomcat stop`
2. See [this Wiki page](https://github.com/sul-dlss/rialto/wiki/Disable-enable-inferencing-at-startup) for information on how to turn inferencing on and off.
3. Empty out the TDB store by deleting the contents of `/opt/app/vitro/home/tdbContentModels/`
4. From within the `current` release directory, run `mvn install` to refresh the datastore and Tomcat web application.
5. Start Tomcat again with `sudo service tomcat start`.
6. The original test triples are stored within `/opt/app/vitro/data/rialto-sample-data/vivo/agents/`. Wrap them in SPARQL insert statements using `/opt/app/vitro/data/rialto-sample-data/vivo/wrapit.sh`. Edit the script first, creating a new, named graph for your test load. Then run it with `./wrapit.sh`.
7. To load our test triples into TDB, run the script `/opt/app/vitro/data/rialto-sample-data/vivo/sparql_upd.sh`, e.g. with `nohup ./sparql_upd.sh WRAPPED_DIR > output.log 2>&1 &` where `WRAPPED_DIR` is the output directory specified in the `wrapit.sh` script.

General information about the Vitro sparqlUpdateApi: https://wiki.duraspace.org/display/VIVODOC19x/SPARQL+Update+API
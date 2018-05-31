This document describes how we load data into Vitro using the Jena tdbloader tool.

# tdbloader

1. [Install Apache Jena](https://jena.apache.org/download/index.cgi)
1. [Set up your shell](https://jena.apache.org/documentation/tdb/commands.html#script-set-up-bash-scripts)
1. Ensure your user account has write access to all files in `/path/to/vitro/tdbContentModels/`
1. Run tdbloader:  
    `tdbloader --graph http://vitro.mannlib.cornell.edu/default/vitro-kb-2 --loc /path/to/vitro/tdbContentModels /path/to/vivo/agents/*.nt`
1. Restart Tomcat (this is required because `tdbloader` is writing to TDB underneath Vitro, and TDB has not been designed for concurrent usage across separate application environments)
1. Via the Vitro UI, recompute inferences. This will trigger rebuilding the search index once complete.

# tdbloader2

`tdbloader2` is the faster/newer version of `tdbloader`. It only operates on empty databases, however, so is not an option we can consider since we will need to perform many incremental loads over time.

# Troubleshooting

If running the loader step above throws an `Argument list too long` error, you may need to bump up that limit. On Linux, you can do this using `ulimit -s 65536`.

# Findings

Once we learned that the trick to getting Vitro to "see" `tdbloader`-loaded data was to add it to the ABox named graph (`http://vitro.mannlib.cornell.edu/default/vitro-kb-2`), we ran the loader against the full dataset and it performed admirably:

> 15:02:03 INFO  loader               :: ** Completed: 4,522,586 quads loaded in 68.34 seconds [Rate: 66,176.77 per second]

After that, we attempted to manually kick off inferencing, but Vitro could no longer write to TDB due to a `BlockAccessBase: Bounds exception`. Restarting Tomcat restores Vitro's connection to its TDB database, and also triggers a recomputation of inferences. Running this operation against the full dataset took approximately five minutes with 1,776,753 URIs added to Vitro's inference graph. Inferencing also triggers rebuilding the Solr index, and that too took about five minutes, adding 126,088 documents to the index.

Ultimately, the team dismissed `tdbloader` as an ingest/load mechanism. `tdbloader` doesn't use Jena transactions to write data, and we believed this was the cause of having to restart the Vitro server to get it back in a working state. The documentation of TDB is clear on this point: TDB wasn't designed for concurrency outside of Jena transactions, and `tdbloader` does not support transactions. The team is not going to use `tdbloader` partly because needing to restart the server is an undesirable hack, but mostly because there is a risk that writing data using `tdbloader` while Vitro is also writing to TDB (e.g., recomputing inferences) will cause data corruption, necessitating a wipe and full reload. We have seen this happen, in fact, in our limited experiments with `tdbloader`.
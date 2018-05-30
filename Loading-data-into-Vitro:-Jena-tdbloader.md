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

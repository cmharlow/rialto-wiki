This document describes how we load data into Vitro using the Jena tdbloader tool.

# tdbloader

1. [Install Apache Jena](https://jena.apache.org/download/index.cgi)
1. [Set up your shell](https://jena.apache.org/documentation/tdb/commands.html#script-set-up-bash-scripts)
1. Transform sample data to N-Quads, to ensure imported data is in Vitro's "ABox" named graph  
    `for f in *.nt; do sed -e 's/\.$/<http:\/\/vitro.mannlib.cornell.edu\/default\/vitro-kb-2> ./g' $f > $f.nq; done`
1. Ensure your user account has write access to all files in `/path/to/vitro/tdbContentModels/`
1. Run tdbloader:  
    `tdbloader --loc /path/to/vitro/tdbContentModels /path/to/vivo/agents/*.nq`
1. Restart Tomcat (apparently this is needed because `tdbloader` is writing to TDB underneath Vitro?)
1. Via the Vitro UI, recompute inferences.
1. Via the Vitro UI, rebuild the search index.

# tdbloader2

`tdbloader2` is the faster/newer version of `tdbloader`. It only operates on empty databases, however, so is not an option we can consider since we will need to perform many incremental loads over time.

# Troubleshooting

If running the loader step above throws an `Argument list too long` error, you may need to bump up that limit. On Linux, you can do this using `ulimit -s 65536`.

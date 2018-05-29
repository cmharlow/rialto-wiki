This document describes how we load data into Vitro using the Jena tdbloader tool.

# tdbloader2

`tdbloader2` is the faster/newer version of `tdbloader`. It only operates on empty databases, however, so is not an option we can consider since we will need to perform many incremental loads over time.

# tdbloader

1. [Install Apache Jena](https://jena.apache.org/download/index.cgi)
1. [Set up your shell](https://jena.apache.org/documentation/tdb/commands.html#script-set-up-bash-scripts)
1. Transform sample data to N-Quads, to ensure imported data is in Vitro's "ABox" named graph, e.g., via  
    `for f in *.nt; do sed -e 's/\.$/<http:\/\/vitro.mannlib.cornell.edu\/default\/vitro-kb-2> ./g' $f > $(basename $f).nq; done`
1. Run tdbloader:  
    `tdbloader --loc /path/to/vitro/tdbContentModels /path/to/vivo/agents/*.nq`
1. Via the Vitro UI, recompute inferences.
1. Via the Vitro UI, rebuild the search index.

# Troubleshooting

If running the loader step above throws an `Argument list too long` error, you may need to bump up that limit. On Linux, you can do this using `ulimit -s 65536`.

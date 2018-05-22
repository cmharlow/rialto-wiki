This document describes how we load data into Vitro using the Jena tdbloader(2) tool.

# tdbloader2

1. [Install Apache Jena](https://jena.apache.org/download/index.cgi)
1. [Set up your shell](https://jena.apache.org/documentation/tdb/commands.html#script-set-up-bash-scripts)
1. Clear out your TDB database (`tdbloader2`, the faster/newer version of `tdbloader`, only operates on empty databases). `rm -f /path/to/vitro/tdbContentModels/*`
1. `tdbloader2 --loc /path/to/vitro/tdbContentModels /path/to/vivo/agents/*.nt`

# tdbloader

...

# Troubleshooting

If running the loader step above throws an `Argument list too long` error, you may need to bump up that limit. On Linux, you can do this using `ulimit -s 65536`.
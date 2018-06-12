This document describes how we load data into Vitro using Jena SPARQL Update (ARQ).

On this branch: https://github.com/sul-dlss-labs/Vitro/tree/73-tdb-load

See the instructions: https://github.com/sul-dlss-labs/Vitro/blob/73-tdb-load/rialto/arq_instructions.md

# Findings

After running the load, Vitro could no longer write to TDB due to a BlockAccessBase: Bounds exception (same as the `tdbloader` load). Restarting Tomcat restores Vitro's connection to its TDB database.

The team dismissed Jena SPARQL Update as an ingest/load mechanism. The documentation of TDB is clear that it wasn't designed for multi-JVM usage. The team is not going to use Jena SPARQL Update partly because needing to restart the server is an undesirable hack, but mostly because there is a risk that writing data this way while Vitro is also writing to TDB will cause data corruption, necessitating a wipe and full reload. 
This document describes how we load data into Vitro using Jena SPARQL Update (ARQ).

*NOTE* it doesn't look like Vitro uses ARQ. There are no instances of `org.apache.jena.query` see https://jena.apache.org/documentation/query/app_api.html

1. What is the http endpoint for Jena? Is it available to us? -- There is no HTTP API.
2. Can we use curl, or do we need to use the ARQ tools (e.g. https://jena.apache.org/documentation/query/sparql-remote.html#from-the-command-line) -- no HTTP API - irrelevant
3. Can we do SPARQL `LOAD FILE`?
4. If we can't do that, use the Java API for Jena: https://jena.apache.org/documentation/query/update.html
# Invoking SPARQL on the Command-Line

Store your query in a file (called `recipe.txt` in this example), and invoke the following `curl` command:

```shell
curl --data-urlencode query@recipe.txt -i --http1.1 -H "X-API-Key: GETTHISFROMSHAREDCONFIGS" https://get.this.from.shared.configs.amazonaws.com/env/rialto-sparql-loader/
```

**Note**: If using SPARQL Update syntax, change `query@` above to `update@`.

# SPARQL Recipes

## Get a count for a particular type

To get a count of organizations:

```sparql
SELECT (COUNT(?s) as ?triples) WHERE {
       ?s rdf:type <http://xmlns.com/foaf/0.1/Organization> .
}
```

## Return all of a particular type

To see all organizations, for instance:

```sparql
SELECT ?s ?p ?o WHERE {
       ?s rdf:type <http://xmlns.com/foaf/0.1/Organization> .
}
```

To see all organizations with a malformed URI (*e.g.*, using `/organizations/` instead of `/orgs/`):
```sparql
SELECT ?s ?p ?o WHERE {
       ?s rdf:type <http://xmlns.com/foaf/0.1/Organization> .
       FILTER regex(str(?s), "organizations")
}
```

## Delete all of a particular type

To wipe out all organizations: 

```sparql
DELETE { ?s ?p ?o . }
WHERE {
      ?s rdf:type <http://xmlns.com/foaf/0.1/Organization> .
      ?s ?p ?o
}
```

## Wipe all data

**WARNING: This will delete every triple in the store.**

```sparql
DROP ALL
```

Note that the last time I ran this, the endpoint responds with a `504 Gateway Timeout` and a `"Endpoint request timed out"` message. Despite that error status, the entire graph was wiped a few moments later without my needing to intervene.

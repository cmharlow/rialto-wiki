# Invoking SPARQL on the Command-Line

Store your query in a file (called `query.txt` in this example), and invoke the following `curl` command:

```shell
curl --data-urlencode query@query.txt -i --http1.1 -H "X-API-Key: GETTHISFROMSHAREDCONFIGS" https://get.this.from.shared.configs.amazonaws.com/env/rialto-sparql-loader/
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
};
```
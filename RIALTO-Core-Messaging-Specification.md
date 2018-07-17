See [[RIALTO Architecture]] to see the central role messaging plays.

message: JSON containing the following:

```javascript
{ 
  "Action": "touch",
  "Entities": ["id", "id", "id"],
  "Body": "string"
}
```

Action options:
- touch == C[R]UD on triples / rdf statements,
- delete == full entity delete (stretch goal, i.e. completely remove an entity graph)
- rebuild == full derivative dataset(s) rebuild. 
- others as needed for edge cases or to differentiate sparql-load from ingest-service

Entities: array of identifiers (URIs) that need to be updated / synced in derivative datastores. 

Body: full body of the ingest-service or sparql-loader request (i.e., the POST's JSON or the SPARQL UPDATE request).

Supports both cases for generic re-trigger full re-derivation of data and specific re-derivation of subset of data, with focus on the latter.
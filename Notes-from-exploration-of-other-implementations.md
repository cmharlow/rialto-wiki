In April 2018, the team explored how two other institutions are using VIVO in research information management and profiles.  Full notes in private Google doc here: https://docs.google.com/document/d/1tVlZIdcnbUngqhkeOLgk0nxRVeaV_YBfwt8W1TEq7hQ  

# Cornell

Cornell is using VIVO in their Scholars at Cornell site (https://scholars.cornell.edu/).  The core tech stack includes:

* VIVO for profiles pages - via modified, customized VIVO pages. All freemarker built on sparql data queries, other.
* Vitro with SDB for data store
* Symplectic Elements and Data Insight for harvesting. Creates a merged record from all sources presented in an article (i.e. the Uber record), do normalization via discrimination of which sources you select
* Create a merged record from all sources presented in an article (i.e. the Uber record), do normalization via discrimination of which sources you select
* Data indexed into Solr for performance in queries to feed visualizations
* Data analysis module serves up JSON to visualization using javascript libraries (D3.js is the main one; C3, a D3 extension)
* Data distribution API provides views into that triplestore
* Note that there is an embedded triplestore to solr indexer in VIVO, which is set up with configuration files.



# Brown

Brown is using Vitro as a back-end data store, but not for the front end.  

* Just using Vitro, but still using 3 tiered build
* Abandoned VIVO ontology, not a good fit and was slowing them down + causing data management headaches
* Ingest is via nightly data dumps from homegrown faculty information system
* Separate services for managing faculty publications
* Data lives in Vitro and is indexed into Solr
* Flask Apps communicate with Query API on Vitro -- submit SPARQL queries to VIVO API, publish results as JSON over their API
* VIVO to Rails front end for visualizations - https://github.com/Brown-University-Library/vivo-on-rails
* RDF has been valuable for schema neutrality + merging of data from variety of sources; No schema migrations
Challenges: with RDF, aren’t sort of client libraries for communicating with RDF database / triplestore like a python driver for SQL. Complexity then is pushed into application code.


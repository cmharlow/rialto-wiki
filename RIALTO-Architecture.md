# Proposed Conceptual Architecture

[![Early Architecture Diagram for RIALTO](https://docs.google.com/drawings/d/e/2PACX-1vSQ02m-7tdxzE7UYSbWPsl8DmeWboT952DhosgTLjNCAIUb1f95q71XpijdMQiD60MaWCGBsURLkSmP/pub?w=1440&h=1080)](https://docs.google.com/drawings/d/1A_X8krKQcbuonwtzuwMuk1rkEtzLrx-kcSQiuKEoPns/edit)

# Current Working Architecture
## RIALTO Core
[![Work in Progress Architectural Diagram for RIALTO Core](/sul-dlss/rialto/wiki/Current_RIALTO_Architecture.png)](https://drive.google.com/file/d/14aOYXrn6iN1FzL21_BBQJmf90RuqGO4L/view?usp=sharing)

## RIALTO Combine
TBD

## RIALTO Web App
TBD

# Current Dataflows

## RIALTO Core

* POST JSON-LD (create statements) => Triplestore via SPARQL UPDATE => Message (Subject URIs for each triple) => SPARQL for each Entity graph transformed to JSON (gets new with all data) => Entities in JSON to Index
* POST SPARQL UPDATE INSERT/DELETE (CRUD statements) => Triplestore via SPARQL UPDATE INSERT/DELETE => Message (Subject URIs for each triple) => SPARQL for each Entity graph transformed to JSON (gets updated & new, drops deleted) => Entities in JSON to Index
* DELETE JSON-LD (delete **entities**) => Triplestore via SPARQL UPDATE DELETE {`<entity URI> ?p ?o>`} => Message (Subject URIs for entities to delete) => Delete Entities JSON to Index
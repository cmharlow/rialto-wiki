RIALTO is primarily interested in **Publications** (articles, research output, publications, etc.), **Agents** (people, departments, agencies, organizations, etc.), **Grants**, and **Projects**. Each of these is represented by a data model that defines the scope of the entity and a metadata application profile that shows what information we capture about these entities for RIALTO's usage.

## Publications (aka Documents or Citations)

Publications are representations (published meant generally) of articles, research outputs, datasets, etc. If feasible, there should link to manifestations of that Work (i.e. DOI).

* **Sources**: Web of Science, SUL-PUB (should be subset of what is in WoS), Profiles
* **Types**: 
  * Top level / generic: Publication or Document: http://purl.org/ontology/bibo/Document
  * Abstract: http://vivoweb.org/ontology/core#Abstract
  * Article: http://purl.org/ontology/bibo/Article
  * Book: http://purl.org/ontology/bibo/Book
  * Case study: http://vivoweb.org/ontology/core#CaseStudy
  * Catalog: http://vivoweb.org/ontology/core#Catalog
  * Clinical Guideline: http://purl.org/spar/fabio/ClinicalGuideline
  * Conference Poster: http://vivoweb.org/ontology/core#ConferencePoster
  * Dataset: http://vivoweb.org/ontology/core#Dataset
  * Manual: http://purl.org/ontology/bibo/Manual
  * Manuscript: http://purl.org/ontology/bibo/Manuscript
  * Patent: http://purl.org/ontology/bibo/Patent
  * Report: http://purl.org/ontology/bibo/Report
  * Research Proposal: http://vivoweb.org/ontology/core#ResearchProposal
  * Score: http://vivoweb.org/ontology/core#Score
  * Screenplay: http://vivoweb.org/ontology/core#Screenplay
  * Slideshow: http://purl.org/ontology/bibo/Slideshow
  * Speech: http://vivoweb.org/ontology/core#Speech
  * Standard: http://purl.org/ontology/bibo/Standard
  * Thesis: http://purl.org/ontology/bibo/Thesis
  * Translation: http://vivoweb.org/ontology/core#Translation
  * Webpage: http://purl.org/ontology/bibo/Webpage
  * Working Paper: http://vivoweb.org/ontology/core#WorkingPaper

Field               | Predicate | Expected Data Type | Cardinality | Definition
------------------- | --------- | ------------------ | ----------- | ----------------------
@type               | rdf:type  | URI from list above | [1,n]      |  Type of the resource.
abstract            | bibo:abstract | string-literal | [0,n]       |  A summary of the resource. 
author              | vivo:relatedBy vivo:Authorship vivo:relates | URI for foaf:Agent | [0,n] | Author of the publication.
Profiles confirmed  | vivo:relatedBy vivo:Authorship dcterms:source | "Profiles" string-literal | [0,1] | If the authorship relationship has been confirmed by the Author in Profiles. Can be reused for any relationship needed (i.e. Editorship, Advising Relationship, etc.)
cites               | bibo:cites | document URI | [0,n] | Relates a document to another document that is cited by the first document as reference, comment, review, quotation or for another purpose. 
date of creation    | dct:created | DateTime string, EDTF | [1,1] | Used to describe the creation date of a resource.
description         | vivo:description | string-literal | [0,n] | Description of the resource.
DOI                 | bibo:doi | DOI IRI | [0,1] | Digital Object Identifier for the publication.
editor              | vivo:relatedBy vivo:Editorship vivo:relates | URI for foaf:Agent | [0,n] | Editor of the publication.
identifier          | bibo:identifier | IRI | [1,n] | Identifier for the resource. May be from multiple sources.
funded by           | vivo:hasFundingVehicle | Grant URI | [0,n] | Grant (or contract) providing funding for the publication.
journal issue       | dcterms:hasPart  | Document URI (Article) | [0,n] | Journal is another entity with issue number, label / title, possibly isPartOf URI for the Journal title overall.
link                | bibo:uri | URI / IRI | [0,n] | (Preferably, permanent) URL for accessing the resource on the internet. 
publisher           | vivo:publisher | URI for foaf:Organization | [0,n] |  Publisher of the resource.
sameAs              | owl:sameAs | URI | [0,n] | Other resources (identified via URIs) that are the same as this resource.
sponsor             | vivo:informationResourceSupportedBy | Agent URI | [0,n] | Institution supporting the publication. 
subject             | dcterms:subject | Topic / Concept URI | [0,n] | Topic or concept the resource is about. 
title               | dcterms:title | string-literal | [1,1] | Title for the resource. 
alternate title     | dcterms:alternative | string-literal | [0,n] | Alternative title(s) for the resource. 

## Topics (Concepts)
Topics are subject areas or concepts. Works, grants, or departments may be associated with a Topic. Agents may have a research area that is a Topic.

* **Sources**: Web of Science, SUL-PUB (should be subset of what is in WoS), Profiles
* **Types**: 
  * Top level / generic: Topic: http://www.w3.org/2004/02/skos/core#Concept

Field | Predicate | Expected Data Type | Cardinality | Definition
----- | --------- | ------------------ | ----------- | ----------
label | skos:prefLabel | string-literal | [1,1] | Primary label for the Concept. 
alternate labels | skos:altLabel | string-literal | [0,n] | Alternative labels for the Concept.
broader than | skos:broader | Concept URI | [0,n] | Broader concepts (within a scheme).
narrower than | skos:narrower | Concept URI | [0,n] | Narrower concepts (within a scheme).
vocabulary source | skos:inScheme | skos:ConceptScheme URI | [0,n] | Vocabulary or scheme the concept is in (e.g. MESH Headings, LCCN, AAT, etc.)
identifier | dcterms:identifier |  |  | 
sameAs     | owl:sameAs | URI | [0,n] | Other Concepts (identified via URIs) that are the same as this resource.
scope note | skos:scopeNote | string-literal | [0,1] | Note describing the scope and definition of the Concept.

## Agents

Agents are some sort of actor involved in creating works or projects, or in supporting works or projects via grants or institutional support. 

* **Types**: People, Student, Faculty, Researcher, Academic institutes, Departments, Universities, Colleges, Organizations / Agencies >> Funders
* **Sources**: Stanford LDAP, CAP Profiles API (Stanford Affiliates scholarly record type info), ORCID & ISNI.

Field | Predicate | Expected Data Type | Cardinality | Value Type | Definition
----- | --------- | ------------------ | ----------- | ---------- | ----------
advisor              | vivo:relatedBy vivo:Authorship vivo:relates | URI for foaf:Agent | [0,n] | Author of the publication.

* agent institutional affiliation
* agent department
* agent country
* related topic areas
* role(s) / job(s)
* name
* institution name
* institution country
* funded by (grant)
* email address

## Grants

Grants are awards for some project(s) or work(s), usually attached to one or more lead agents (PIs) whether people or departments, and awarded or funded by an organization or agency.

* **Types**: Governmental << Federal / State / Local, Private, Internal to Stanford, ... 
* **Sources**: Web of Science (funding agency string / grant number in metadata), SERA (not done yet)

Field | Predicate | Expected Data Type | Cardinality | Value Type | Definition
----- | --------- | ------------------ | ----------- | ---------- | ----------

 Grant Name, Name, Grant Amount (if available), Status (awarded yes/no), Start Date

* which publications resulted from which grants

## Projects

Projects here are research projects that are funded by grants or institutions, worked on by agents, and may produce multiple works. 
Sources: SERA (not done yet)

Field | Predicate | Expected Data Type | Cardinality | Value Type | Definition
----- | --------- | ------------------ | ----------- | ---------- | ----------



# Other Representation Needs

- CSV: 
  - One column per year, row for each academic institute, number of publications produced by faculty members associated with that institute in that topic area(s)
  - grant per row, followed by publications underneath it (one per row)
  - per department, department name, department org, institution department's authors has collaborated with, number of collaborations, collaborator org, collaborator name, collaborator country
  - per author, author name, author org, institution author has collaborated with, number of collaborations, collaborator org, collaborator name, collaborator country
  - Author Name, Total Publication Count, Total Profiles-derived Publication Count, Total number of times cited across all publications
  - for department & timeframe, report showing journals in one table, and publishers in another, along with counts of publications for each by authors
  - one column per month, row for each department, number of publications produced by faculty members associated with that department, topic area(s)
- Facets:
  - result entities types
  - years range
  - date range
  - topic areas
  - number of publications
  - institute
  - academic unit or department
  - department or other organizational unit (e.g. school)
  - grants
  - agent (research / faculty member)
- Results:
  - grants with number of resulting connected publications
  - publications
  - projects
  - faculty
- viz:
  - given agent, heat map of the world with color coding on countries to indicate frequency of collaboration.
  - network visualization, showing institutions as nodes, with lines connecting the institutions represented by all co-authors of projects or works. The size of the nodes is determined by the number of authors at that institution. 

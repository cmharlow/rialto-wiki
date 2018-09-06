RIALTO is primarily interested in **Publications** (articles, research output, publications, etc.), **Agents** (people, departments, agencies, organizations, etc.), **Grants**, and **Projects**. Each of these is represented by a data model that defines the scope of the entity and a metadata application profile that shows what information we capture about these entities for RIALTO's usage.

## Publications (aka Documents or Citations)

Publications are representations of articles, research outputs, datasets, etc. If feasible, there should link to manifestations of that Work (i.e. DOI).

* **Sources**: Web of Science, Profiles, Dimensions
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
has instrument      | gcis:hasInstrument | gcis:Instrument URI | [0,n] | A type of tool or device used for a particular task, especially for scientific work, as presented in the publication (specifically for Datasets).
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

* **Sources**: Web of Science, Profiles
* **Types**: 
  * Top level / generic: Topic: http://www.w3.org/2008/05/skos#Concept

Field | Predicate | Expected Data Type | Cardinality | Definition
----- | --------- | ------------------ | ----------- | ----------
@type | rdf:type  | URI from list above | [1,n]      |  Type of the resource.
label | skos:prefLabel, rdfs:label | string-literal | [1,1] | Primary label for the Concept. 
alternate labels | skos:altLabel | string-literal | [0,n] | Alternative labels for the Concept.
broader than | skos:broader | Concept URI | [0,n] | Broader concepts (within a scheme).
narrower than | skos:narrower | Concept URI | [0,n] | Narrower concepts (within a scheme).
vocabulary source | skos:inScheme | skos:ConceptScheme URI | [0,n] | Vocabulary or scheme the concept is in (e.g. MESH Headings, LCCN, AAT, etc.)
identifier | dcterms:identifier | IRI | [1,n] | Identifier for the resource. May be from multiple sources.
sameAs     | owl:sameAs | URI | [0,n] | Other Concepts (identified via URIs) that are the same as this resource.
scope note | skos:scopeNote | string-literal | [0,1] | Note describing the scope and definition of the Concept.

## Agents

Agents are some sort of actor involved in creating works or projects, or in supporting works or projects via grants or institutional support. 

### Persons

* **Sources**: CAP Profiles API (Stanford Affiliates scholarly record type info), Stanford LDAP, ORCID, ISNI
* **Types**: 
  * Top level / generic: Agent: http://xmlns.com/foaf/0.1/Agent
  * Top level / generic: Person: http://xmlns.com/foaf/0.1/Person 
  * Student: http://vivoweb.org/ontology/core#Student
  * Faculty: http://vivoweb.org/ontology/core#FacultyMember
  * Faculty Emeritus: http://vivoweb.org/ontology/core#EmeritusFaculty
  * Non-Academic: http://vivoweb.org/ontology/core#NonAcademic
  * Non-Faculty Academic: http://vivoweb.org/ontology/core#NonFacultyAcademic

Field   | Predicate        | Expected Data Type    | Cardinality | Definition
------- | ---------------- | --------------------- | ----------- | ----------
@type   | rdf:type  | URI from list above | [1,n]      |  Type of the resource.
about   | vivo:overview    | string-literal        | [0,n]       | About the Agent.
address | vcard:hasAddress | URI for vcard:Address | [0,1]       | Address for the Agent.
advisor | vivo:relatedBy vivo:AdvisingRelationship vivo:relates; obo:RO_000053 vivo:AdvisorRole | URI for foaf:Agent | [0,n] | Advisor of the person.
country | dcterms:spatial  | URI for country in address | [0,n]  | Normalized country the Agent resides or is based in.
department | vivo:relatedBy vivo:Position vivo:relates foaf:Organization | URI for foaf:Organization | [0,n] | Organization, at department level, that the person works (or has worked) for.
email address | vcard:hasEmail | string literal | [0,n] | Email address for the individual.
PI of | vivo:relatedBy vivo:Grant | URI for vivo:Grant | [0,n] | Grant the person is currently PI or has been PI for.
funded by (grant) | vivo:hasFundingVehicle | Grant URI | [0,n] | Grant (or contract) providing funding for the Agent (or their Position).
institutional affiliation | vivo:relatedBy vivo:Position vivo:relates foaf:Organization obo:BFO_0000050 foaf:Organization | URI for foaf:Organization | [0,n] | Organization, at institution level, that the person works (or has worked) for.
full name | vcard:fn | String Literal | [1,1] | Full name of the person (some sort of preferred label for the entity).
name | vcard:hasName | URI for vcard:Name | [1,1] | Name (broken into data property components) for the person.
hasResearchArea | vivo:hasResearchArea | URI for skos:Concept | [0,n] | Topical area the person does research on or in.
role(s) / job(s) | vivo:relatedBy vivo:Position | URI for vivo:Position | [0,n] | Position or job the person currently holds or previously held.

### Organizations
  * Top level / generic: Agent: http://xmlns.com/foaf/0.1/Agent
  * Top level / generic: Organization: http://xmlns.com/foaf/0.1/Organization
  * Association: http://vivoweb.org/ontology/core#Association
  * Center: http://vivoweb.org/ontology/core#Center
  * College: http://vivoweb.org/ontology/core#College
  * Consortium: http://vivoweb.org/ontology/core#Consortium
  * Department: http://vivoweb.org/ontology/core#Department
  * Division: http://vivoweb.org/ontology/core#Division
  * Foundation: http://vivoweb.org/ontology/core#Foundation
  * Funding Organization: http://vivoweb.org/ontology/core#FundingOrganization
  * Government Agency: http://vivoweb.org/ontology/core#GovernmentAgency
  * Hospital: http://vivoweb.org/ontology/core#Hospital
  * Institute (Academic): http://vivoweb.org/ontology/core#Institute
  * Laboratory: http://vivoweb.org/ontology/core#Laboratory
  * Library: http://vivoweb.org/ontology/core#Library
  * Museum: http://vivoweb.org/ontology/core#Museum
  * Program: http://vivoweb.org/ontology/core#Program
  * Publisher: http://vivoweb.org/ontology/core#Publisher
  * Research Organization: http://vivoweb.org/ontology/core#ResearchOrganization
  * School: http://vivoweb.org/ontology/core#School
  * Student Organization: http://vivoweb.org/ontology/core#StudentOrganization
  * University: http://vivoweb.org/ontology/core#University

Field   | Predicate        | Expected Data Type    | Cardinality | Definition
------- | ---------------- | --------------------- | ----------- | ----------
@type   | rdf:type  | URI from list above | [1,n]      |  Type of the resource.
address | vcard:hasAddress | URI for vcard:Address | [0,1]       | Address for the Organization.
country | dcterms:spatial  | URI for country in address | [0,n]  | Normalized country the Organization is based in.
email address | vcard:hasEmail | string literal | [0,n] | Email address for the Organization.
administering (grant) | vivo:relatedBy vivo:Grant | URI for vivo:Grant | [0,n] | Grant administered by the Organization.
funded by (grant) | vivo:hasFundingVehicle | Grant URI | [0,n] | Grant (or contract) providing funding for the Agent (or their Position).
children organizations | obo:BFO_0000051 foaf:Organization | URI for foaf:Organization | [0,n] | Organization this organization is contains.
parent organizations | obo:BFO_0000050 foaf:Organization | URI for foaf:Organization | [0,n] | Organization this organization is a part of.
employees | vivo:relatedBy vivo:Position* vivo:relates foaf:Agent | URIs for Agents | [0,n] | Agents that hold a position in the Organization.
name | skos:prefLabel, rdfs:label | string literal | [1,1] | Primary name for the Organization.
alternate name | skos:altLabel | string literal | [0,n] | Alternate names for the Organization.
abbreviation | vivo:abbrevation | string literal | [0,n] | Abbreviated names for the Organization.
related topic areas | vivo:hasResearchArea | URI for skos:Concept | [0,n] | Topical area the Organization does research on or in.

### Groups
  * Top level / generic: Agent: http://xmlns.com/foaf/0.1/Agent
  * Top level / generic: Group: http://xmlns.com/foaf/0.1/Group
  * Committee: http://vivoweb.org/ontology/core#Committee
  * Team: http://vivoweb.org/ontology/core#Team

Field   | Predicate        | Expected Data Type    | Cardinality | Definition
------- | ---------------- | --------------------- | ----------- | ----------
@type   | rdf:type  | URI from list above | [1,n]      |  Type of the resource.
institution | obo:BFO_0000050 foaf:Organization | URI for foaf:Organization | [0,n] | Organization this organization is a part of.
name | skos:prefLabel, rdfs:label | string literal | [1,1] | Primary name for the Organization.
alternate name | skos:altLabel | string literal | [0,n] | Alternate names for the Organization.
abbreviation | vivo:abbrevation | string literal | [0,n] | Abbreviated names for the Organization.

## Grants

Grants are awards for some project(s) or work(s), usually attached to one or more lead agents (PIs) whether people or departments, and awarded or funded by an organization or agency.

* **Sources**: Web of Science (funding agency string / grant number in metadata), SERA (not done yet)
* **Types**: 
  * Top level / generic: http://vivoweb.org/ontology/core#Grant

Field        | Predicate     | Expected Data Type | Cardinality | Definition
------------ | ------------- | ------------------ | ----------- | ----------
@type        | rdf:type  | URI from list above | [1,n]      |  Type of the resource.
Grant Name   | skos:prefLabel, rdfs:label | string-literal     | [1,1]       | Name or title of the grant. 
Abstract     | vivo:abstract | string-literal     | [1,1]       | Description or abstract of the grant. 
Funds        | vivo:fundingVehicleFor | URI for vivo:Position, foaf:Agent, or bibo:Document | [0,n] | What has been funded by the Grant.
Grant Amount | vivo:totalAwardAmount | decimal-literal? | [0,1] | Amount awarded by the Grant.
Principal Investigator | vivo:relates vivo:PrincipalInvestigatorRole obo:RO_0000052 foaf:Person | URI for foaf:Person | [1,n] | Principal Investigator for the grant.
Administered By | vivo:relates vivo:AdminRole obo:RO_0000052 foaf:Organization | URI for foaf:Organization | [1,n] | Administrating Organization for the grant's funds.
Funded By    | vivo:assignedBy | URI for foaf:Organization | [1,n] | Funding Organization for the grant.
Start Date   | frapo:hasStartDate | datetime literal | [0,1] | Date the Grant support / funding starts.
End Date     | frapo:hasEndDate   | datetime literal | [0,1] | Date the Grant support / funding ends.
Award Date   | frapo:hasAwardDate | date literal     | [1,1] | Date the Grant was awarded.

## Projects

Projects here are research projects that are funded by grants or institutions, worked on by agents, and may produce multiple works. 

* **Sources**: SERA (not done yet)
* **Types**: 
  * Top level / generic: Project: http://xmlns.com/foaf/0.1/Project

Field           | Predicate     | Expected Data Type | Cardinality | Definition
--------------- | ------------- | ------------------ | ----------- | ----------
Title           | dcterms:title | string-literal     | [1,1] | Title for the project. 
Alternate title | dcterms:alternative | string-literal | [0,n] | Alternative title(s) for the project. 
Start Date   | frapo:hasStartDate | datetime literal | [0,1] | Date the Project starts.
End Date     | frapo:hasEndDate   | datetime literal | [0,1] | Date the Project ends.

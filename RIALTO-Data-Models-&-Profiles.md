Table of Contents
=================

* [Data Models & Profiles](#data-models)
  * [Publications (aka Documents or Citations)](#publications-aka-documents-or-citations)
  * [Topics (Concepts)](#topics-concepts)
  * [Agents](#agents)
    * [Persons](#persons)
    * [Organizations](#organizations)
    * [Groups](#groups)
  * [Grants](#grants)
  * [Projects](#projects)
* [Source Mappings](#source-mappings)
  * [Named Graphs](#named-graphs)
  * [Namespaces & Schemas](#namespaces--schemas)
  * [Organizations (Profiles) mapping](#organizations-profiles-mapping)
  * [People (Profiles) Mapping](#people-profiles-mapping)
  * [Grants (SeRA) Mapping](#grants-sera-mapping)
  * [Publications (WoS/Web of Science) Mapping](#publications-wosweb-of-science-mapping)
    * [Document Type Mapping](#document-type-mapping)
      * [Unmapped WoS Types](#unmapped-wos-types)
      * [Unrepresented RIALTO Publication Types](#unrepresented-rialto-publication-types)

# Data Models

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
orcid   | vivo:orcidId | String | [0,1] | The researchers ORCID
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

# Source Mappings

## Named Graphs

Create one named graph per data source.

## Namespaces & Schemas

* RIALTO namespace base (not resolvable): http://sul.stanford.edu/rialto/
* Organizations NS: `agents/orgs/`
* People NS: `agents/people/`
* Publications NS: `publications/`
* Concepts NS: `concepts/`
* Grants NS: `grants/`
* Context nodes:
  * `context/addresses/`
  * `context/names/`
  * `context/positions/`
  * `context/relationships/`
  * `context/roles/`
* External:
  * VIVO = Namespace("http://vivoweb.org/ontology/core#")
  * OBO = Namespace("http://purl.obolibrary.org/obo/")
  * VCARD = Namespace("http://www.w3.org/2006/vcard/ns#")
  * RDF, FOAF, SKOS, RDFS, DCTERMS

## Organizations (Profiles) mapping

* Organization Identifier == $.alias (string)
* RDF.type == FOAF.Agent, FOAF.Organization
* Organization URI == RIALTO organizations namespace + organization identifier
* Organization Alias == $.alias (string)
* Children == $.children (array of strings, identifiers for each child), mapped to OBO.BFO_0000051 for each child identifier as a child organization URI
* Organization Name == $.name (string), mapped to SKOS.prefLabel & RDFS.label as a Literal
* Organization Codes == $.orgCodes (array of strings), mapped to DCTERMS.identifier as a Literal
* Parent == $.parent (string, identifier for parent), mapped to OBO.BFO_0000050 for parent identifier as a parent organization URI
* Organization Types == $.type
* Based on $.type
   * "DEPARTMENT": RDF.type, VIVO.Department
   * "DIVISION": RDF.type, VIVO.Division
   * "ROOT": RDF.type, VIVO.University (Always Stanford University)
   * "SCHOOL": VIVO.School
   * "SUB_DIVISION": VIVO.Division

## People (Profiles) Mapping

* Person Identifier == $.profileId (string)
* RDF.type == FOAF.Agent, FOAF.Person
* Person URI == RIALTO people namespace + person identifier
* Person Label == $.names.preferred.firstName (string) + " " + $.names.preferred.middleName (string) + " " +  $.names.preferred.lastName (string), mapped to SKOS.prefLabel & VCARD.fn as a Literal
* Person Name URI == RIALTO names namespace (in contexts) + person identifier
* Person Name
  * Person URI VCARD.hasName Person Name URI . 
  * Person URI RDF.type, VCARD.Name .
  * Person Name URI VCARD.given-name $.names.preferred.firstName (string) .
  * Person Name URI VCARD.middle-name $.names.preferred.middleName (string) .
  * Person Name URI VCARD.family-name $.names.preferred.lastName (string). 
* Person Affiliation:
  * if $.affiliations.capPhdStudent (Boolean) == True or $.affiliations.capMsStudent (Boolean) == True or $.affiliations.capMdStudent (Boolean) == True: Person URI RDF.type VIVO.Student
  * if $.affiliations.capFaculty (Boolean) == True: Person URI RDF.type VIVO.FacultyMember
  * if $.affiliations.capFellow (Boolean) == True or $.affiliations.capResident (Boolean) == True or $.affiliations.capPostdoc (Boolean) == True: Person URI RDF.type VIVO.NonFacultyAcademic
  * if $.affiliations.physician (Boolean) == True or $.affiliations.capStaff (Boolean) == True: Person URI RDF.type VIVO.NonAcademic
  * Ignoring $.affiliations.capRegistry & $.affiliations.capOther at present
* Person Biograph: Person URI VIVO.overview $.bio.text (Literal)
* Person address: if $.contacts.type == "academic":
  * Person Address URI: RIALTO Address NS (contexts) + person identifier
    * Person VCARD.hasAddress Person Address URI . 
    * Person Address URI RDF.type, VCARD.Address .
    * Person Address URI VCARD.street-address $.contacts.address (Literal) 
    * Person Address URI VCARD.locality $.contacts.city (Literal)
    * Person Address URI VCARD.region $.contacts.state (Literal)
    * Person Address URI VCARD.postal-code $.contacts.zip (Literal)
    * Address URI DCTERMS.spatial country_uri (Geonames lookup based on $.contacts.zip)
    * Address URI VCARD.country-name Name (Literal, from Geonames lookup based on $.contacts.zip)
* Department (Organization) URI: use Department label for Organization lookup in CAP data (above) using $.contacts.department (Literal for lookup, URI for end value)
* Person Position URI: Positions context URI + Person ID + Position Label (+ Date...?)
  * Person Position URI RDF.type VIVO.Position .
  * Person URI VIVO.relatedBy Person Position URI .
  * Person Position URI RDFS.label $.contacts.position (Literal, above) .
  * Person Position URI VIVO.relates Department (Organization) URI .
* for each advisee in $.advisees : 
  * Advisee URI: RIALTO People NS + $advisees.advisee.profileId
    * Advisee URI RDF.type FOAF.Agent, FOAF.Person
    * Advisee Name URI: RIALTO Names NS (contexts) + advisee ID
    * Advisee Name URI VCARD.fn $.advisees.advisee.label.text
    * Advisee URI VCARD.hasName Advisee Name URI .
    * Advisee Name URI RDF.type VCARD.Name .
    * Advisee Name URI VCARD.given-name $.advisees.advisee.firstName .
    * Advisee Name URI VCARD.family-name $.advisees.advisee.lastName .
    * Relationship URI: Relationship NS (contexts) + Advisee ID + "_" + Person URI
    * Relationship URI RDF.type VIVO.AdvisingRelationship .
    * Advisor Role URI: Roles NS (contexts) + "AdvisorRole"
    * Advisor Role URI RDF.type VIVO.AdvisorRole
    * Advisee Role URI: Roles NS (contexts) + "AdviseeRole"
    * Advisee Role URI RDF.type VIVO.AdviseeRole
    * Person URI VIVO.relatedBy Relationship URI
    * Advisee URI VIVO.relatedBy Relationship URI
    * Relationship URI VIVO.relates Person URI
    * Relationship URI VIVO.relates Advisee URI
    * Person URI OBO.RO_0000053 Advisor Role URI
    * Advisor Role URI OBO.RO_0000052 Person URI
    * Advisee URI OBO.RO_0000053 Advisee Role URI
    * Advisee Role URI OBO.RO_0000052 Advisee URI
* For keyword in $.keywords:
  * Keyword URI: lookup in ?? (wikidata? lc subjects?) based on $.keywords.keyword (with whitespace stripped):
  * Keyword URI RDF.type SKOS.Concept
  * Keyword Label RDFS.label Literal ($.keywords.keyword)
  * Person URI VIVO.hasResearchArea Keyword URI
* For organization in $.organizations:
  * Organization Label $.organizations.organization.label.text
  * Organization URI: lookup for current organizations (from CAP) based on Label (or ID?)
  * Organization ID: Retrieved from lookup for Organization URI
  * Position URI: Positions namespace (context) + Affiliation + _ + Organization ID + "_" + Person ID
  * Position URI RDF.type VIVO.Position
  * Person URI VIVO.relatedBy Position URI
  * Organization URI VIVO.relatedBy Position URI
  * Position URI VIVO.relates Organization URI
  * Position URI VIVO.relates Person URI
  * Position URI RDFS.label $.organizations.organization.affiliation (Literal)
  * Position URI DCTERMS.date "unknown/2018-08" (Literal) (presuming this is current position)
  * Position URI VIVO.hrJobTitle $.primaryContact.title
* Person URI VCARD.hasEmail $.primaryContact.email

## Grants (SeRA) Mapping

* URI == RIALTO grant namespace + `$.spoNumber`
* RDF.type == `VIVO.Grant`
* RDFS.label, SKOS.prefLabel == `$.projectTitle`
* DC.identifier = `$.spoNumber` + normalized form of `$.spoNumber` to aid entity resolution. normalization includes stripping out non-alphanumeric characters and downcasing alpha characters.
* FRAPO.hasStartDate == `$.projectStartDate` (parse out first 10 characters to get date string)
* FRAPO.hasEndDate == `$.projectEndDate` (parse out first 10 characters to get date string)
* VIVO.assignedBy == run value of `$.directSponsorName` through entity resolution, create entity if no matches
* VIVO.relates == get person URI using entity resolution on `$.piSunetId` or create person if no entity. construct PI role URI using rialto context roles namespace + `$.spoNumber` + `_` + `$.piSunetId`. create node relating PI role (@type of VIVO.PrincipalInvestigatorRole) to grant URI using `VIVO.relatedBy`. relate role to PI using `OBO.RO_0000052`, and relate person back to role using `OBO.RO_0000053`. relate PI to grant using URI of person as `@id` and `VIVO.relatedBy` to the grant URI.

## Publications (WoS/Web of Science) Mapping

* Identifier == `$.UID` (string)
* URI == RIALTO publication namespace + (md5-hashed) publication identifier
* RDF type == map value of `$.static_data.fullrecord_metadata.normalized_doctypes.doctype` to document type mapping (see below)
* Abstract == if value of `$.static_data.fullrecord_metadata.abstracts.abstract.abstract_text.count` is 1, grab `$.static_data.fullrecord_metadata.abstracts.abstract.abstract_text.p` (because string), else loop over `$.static_data.fullrecord_metadata.abstracts.abstract.abstract_text.p` (because array) and build up a string using concatenation (in array order)
* DOI == `$.dynamic_data.cluster_related.identifiers.identifier[?(@.type=='doi')].value`. failing that, `$.dynamic_data.cluster_related.identifiers.identifier[?(@.type=='xref_doi')].value`
* Title == `$.static_data.summary.titles.title[?(@.type=='item')].content`
* Date of Creation == `$.static_data.summary.pub_info.sortdate`
* Identifier == `$.dynamic_data.cluster_related.identifiers.identifier[*].value`
* Journal issue == `$.static_data.summary.titles.title[?(@.type=='source')].content`
* Publisher == `$.static_data.summary.publishers.publisher.names.name.display_name`
* Subject == Send strings from `$.static_data.fullrecord_metadata.category_info.subjects.subject[?(@.ascatype=='extended')].content` along with a string representing the source (Web of Science) to the RIALTO entity resolver, and use the returned URIs
* Sponsor (VIVO.informationResourceSupportedBy) == Send grant ID strings from `$.static_data.fullrecord_metadata.fund_ack.grants.grant.grant_agency` to the RIALTO entity resolver. (**Note** that the `.grant` node may be either an object or an array.) Use the returned URIs, or create new ones for grant-funding agencies that don't already have entities in RIALTO.
* Author == Pull back contributor name strings from `$.static_data.summary.names.name`. For each named contributor, extract
their address if it exists, and pull out their `orcid_id`, `first_name`, `last_name`, and `full_name`. Send these five bits of data to the RIALTO entity resolver, and use the URI if it comes back. Else, create a new URI for this person based on an MD5 hash of their first name, a space, and their last name (all in lowercase).
* Funded by (`VIVO.hasFundingVehicle`) == Send grant ID strings from `$.static_data.fullrecord_metadata.fund_ack.grants.grant.grant_ids.grant_id` to the RIALTO entity resolver. Use the returned URIs, or create new ones for grants that don't already have entities in RIALTO.

* Editor == TBD, requires integration with Profiles source data

* Same as == ???
* Alternative title == ???
* Cites == ???
* Description == ???
* Has instrument == ???
* Link == ???

### Document Type Mapping

WoS document types are from https://images.webofknowledge.com/images/help/WOK/hs_document_types.html

| WoS type | RIALTO type |
|----------|-------------|
| Abstract | http://vivoweb.org/ontology/core#Abstract |
| Article | http://purl.org/ontology/bibo/Article |
| Book | http://purl.org/ontology/bibo/Book |
| Data Set | http://vivoweb.org/ontology/core#Dataset |
| Patent | http://purl.org/ontology/bibo/Patent |
| Report | http://purl.org/ontology/bibo/Report |
| Standard | http://purl.org/ontology/bibo/Standard |
| Thesis/Dissertation | http://purl.org/ontology/bibo/Thesis |
| Other | http://purl.org/ontology/bibo/Document |

#### Unmapped WoS Types

Map to http://purl.org/ontology/bibo/Document if nothing better?

* Art and Literature
* Bibliography
* Biography
* Case Report
* Clinical Trial
* Correction
* Data Paper
* Data Study
* Editorial
* Government Publication
* Legislation
* Letter
* Meeting
* News
* Reference Material
* Repository
* Retracted Publication
* Retraction
* Review

#### Unrepresented RIALTO Publication Types

* Case Study
* Catalog
* Clinical Guideline
* Conference Poster
* Manual
* Manuscript
* Research Proposal
* Score
* Screenplay
* Slideshow
* Speech
* Translation
* Webpage
* Working paper

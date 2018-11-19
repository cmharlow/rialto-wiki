Table of Contents
=================

* [Data Models & Profiles](#data-models)
  * [Publications (aka Documents or Citations)](#publications-aka-documents-or-citations)
  * [Topics (Concepts)](#topics-concepts)
  * [Agents](#agents)
    * [Persons](#persons)
    * [Organizations](#organizations)
  * [Grants](#grants)
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

RIALTO is primarily interested in **Publications** (articles, research output, publications, etc.), **Agents** (people, departments, agencies, organizations, etc.), and **Grants**. Each of these is represented by a data model that defines the scope of the entity and a metadata application profile that shows what information we capture about these entities for RIALTO's usage.

## Publications (aka Documents or Citations)

Publications are representations of articles, research outputs, datasets, etc. If feasible, there should link to manifestations of that Work (i.e. DOI).

* **Sources**: Web of Science
* **Types**: 
  * Top level / generic: Publication or Document: http://purl.org/ontology/bibo/Document
  * Abstract: http://vivoweb.org/ontology/core#Abstract
  * Article: http://purl.org/ontology/bibo/Article
  * Book: http://purl.org/ontology/bibo/Book
  * Dataset: http://vivoweb.org/ontology/core#Dataset
  * Patent: http://purl.org/ontology/bibo/Patent
  * Report: http://purl.org/ontology/bibo/Report
  * Standard: http://purl.org/ontology/bibo/Standard
  * Thesis: http://purl.org/ontology/bibo/Thesis

Field               | Predicate | Expected Data Type | Cardinality | Definition
------------------- | --------- | ------------------ | ----------- | ----------------------
@type               | rdf:type  | URI from list above | [1,2]      |  Type of the resource.
abstract            | bibo:abstract | string-literal | [0,n]       |  A summary of the resource. 
author              | vivo:relatedBy vivo:Authorship vivo:relates | URI for foaf:Agent | [0,n] | Author of the publication.
date of creation    | dct:created | DateTime string, EDTF | [1,1] | Used to describe the creation date of a resource.
DOI                 | bibo:doi | DOI IRI | [0,1] | Digital Object Identifier for the publication.
editor              | vivo:relatedBy vivo:Editorship vivo:relates | URI for foaf:Agent | [0,n] | Editor of the publication.
identifier          | bibo:identifier | IRI | [0,n] | Identifier for the resource. May be from multiple sources.
funded by           | vivo:hasFundingVehicle | Grant URI | [0,n] | Grant (or contract) providing funding for the publication.
journal title       | dcterms:isPartOf  | string-literal | [0,1] | Journal that the publication is part of.
publisher           | vivo:publisher | URI for foaf:Organization | [0,n] |  Publisher of the resource.
sponsor             | vivo:informationResourceSupportedBy | Agent URI | [0,n] | Institution supporting the publication. 
subject             | dcterms:subject | Topic / Concept URI | [0,n] | Topic or concept the resource is about. 
title               | dcterms:title | string-literal | [1,1] | Title for the resource. 
alternate title     | dcterms:alternative | string-literal | [0,n] | Alternative title(s) for the resource. 

## Topics (Concepts)
Topics are subject areas or concepts. Works may be associated with a Topic.

* **Sources**: Web of Science
* **Types**: 
  * Top level / generic: Topic: http://www.w3.org/2008/05/skos#Concept

Field | Predicate | Expected Data Type | Cardinality | Definition
----- | --------- | ------------------ | ----------- | ----------
@type | rdf:type  | URI from list above | [1,1]      |  Type of the resource.
subject | dcterms:subject | string-literal | [1,1]   | Primary label for the Concept.

## Agents

Agents are some sort of actor involved in creating works, or in supporting works via grants or institutional support. 

### Persons

* **Sources**: CAP Profiles API (Stanford Affiliates scholarly record type info)
* **Types**: 
  * Top level / generic: Agent: http://xmlns.com/foaf/0.1/Agent
  * Top level / generic: Person: http://xmlns.com/foaf/0.1/Person 
  * Phd student: http://sul.stanford.edu/rialto/ontology#PhdStudent
  * Ms student:  http://sul.stanford.edu/rialto/ontology#MsStudent
  * Md student:  http://sul.stanford.edu/rialto/ontology#MdStudent
  * Faculty: http://sul.stanford.edu/rialto/ontology#Faculty
  * Fellow: http://sul.stanford.edu/rialto/ontology#Fellow
  * Resident: http://sul.stanford.edu/rialto/ontology#Resident
  * Postdoc: http://sul.stanford.edu/rialto/ontology#Postdoc
  * Physician: http://sul.stanford.edu/rialto/ontology#Physician
  * Staff: http://sul.stanford.edu/rialto/ontology#Staff

Field   | Predicate        | Expected Data Type    | Cardinality | Definition
------- | ---------------- | --------------------- | ----------- | ----------
@type   | rdf:type  | URI from list above | [1,n]      |  Type of the resource.
about   | vivo:overview    | string-literal        | [0,1]       | About the Agent.
advisor | vivo:relatedBy vivo:AdvisingRelationship vivo:relates; obo:RO_000053 vivo:AdvisorRole | URI for foaf:Agent | [0,n] | Advisor of the person.
country | dcterms:spatial  | URI for country in address | [0,n]  | Normalized country the Agent resides or is based in.
department | vivo:relatedBy vivo:Position vivo:relates foaf:Organization | URI for foaf:Organization | [0,n] | Organization, at department level, that the person works (or has worked) for.
email address | vcard:hasEmail | string literal | [0,n] | Email address for the individual.
PI of | vivo:relatedBy vivo:Grant | URI for vivo:Grant | [0,n] | Grant the person is currently PI or has been PI for.
institutional affiliation | vivo:relatedBy vivo:Position vivo:relates foaf:Organization obo:BFO_0000050 foaf:Organization | URI for foaf:Organization | [0,n] | Organization, at institution level, that the person works (or has worked) for.
full name | skos:prefLabel, rdfs:label | String Literal | [1,1] | Full name of the person (some sort of preferred label for the entity).
full name variations | skos:altLabel | String Literal | [0,n] | Variations on the name of the person for the purposes of name matching.
name | vcard:hasName | URI for vcard:Name | [1,1] | Name (broken into data property components) for the person.
role(s) / job(s) | vivo:relatedBy vivo:Position | URI for vivo:Position | [0,n] | Position or job the person currently holds or previously held.
sunetid | dcterms:identifier | string-literal | [0,1] | Stanford Network Id


### Organizations
  * Top level / generic: Agent: http://xmlns.com/foaf/0.1/Agent
  * Top level / generic: Organization: http://xmlns.com/foaf/0.1/Organization
  * Department: http://vivoweb.org/ontology/core#Department
  * Division: http://vivoweb.org/ontology/core#Division
  * Institute (Academic): http://vivoweb.org/ontology/core#Institute
  * School: http://vivoweb.org/ontology/core#School
  * University: http://vivoweb.org/ontology/core#University

Field   | Predicate        | Expected Data Type    | Cardinality | Definition
------- | ---------------- | --------------------- | ----------- | ----------
@type   | rdf:type  | URI from list above | [1,n]      |  Type of the resource.
administering (grant) | vivo:relatedBy vivo:Grant | URI for vivo:Grant | [0,n] | Grant administered by the Organization.
parent organizations | obo:BFO_0000050 foaf:Organization | URI for foaf:Organization | [0,n] | Organization this organization is a part of.
employees | vivo:relatedBy vivo:Position* vivo:relates foaf:Agent | URIs for Agents | [0,n] | Agents that hold a position in the Organization.
name | skos:prefLabel, rdfs:label | string literal | [1,1] | Primary name for the Organization.
organization code | dcterms:identifier | string-literal | [0,n] | Stanford org code

## Grants

Grants are awards for some work(s), usually attached to one or more lead agents (PIs) whether people or departments, and awarded or funded by an organization or agency.

* **Sources**: Web of Science (funding agency string / grant number in metadata), SERA
* **Types**: 
  * Top level / generic: http://vivoweb.org/ontology/core#Grant

Field        | Predicate     | Expected Data Type | Cardinality | Definition
------------ | ------------- | ------------------ | ----------- | ----------
@type        | rdf:type  | URI from list above | [1,n]      |  Type of the resource.
grant name   | skos:prefLabel, rdfs:label | string-literal     | [1,1]       | Name or title of the grant. 
identifier   | dcterms:identifier | string literal | [0,n] | Identifier for the grant, including normalized forms of the identifier for matching.
principal investigator | vivo:relates vivo:PrincipalInvestigatorRole obo:RO_0000052 foaf:Person | URI for foaf:Person | [1,n] | Principal Investigator for the grant.
funded by    | vivo:assignedBy | URI for foaf:Organization | [1,n] | Funding Organization for the grant.
start date   | frapo:hasStartDate | datetime literal | [0,1] | Date the Grant support / funding starts.
end date     | frapo:hasEndDate   | datetime literal | [0,1] | Date the Grant support / funding ends.

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
* Organization Name == $.name (string), mapped to SKOS.prefLabel & RDFS.label as a Literal
* Organization Codes == $.orgCodes (array of strings), mapped to DCTERMS.identifier as a Literal
* Parent == $.parent (string, identifier for parent), mapped to OBO.BFO_0000050 for parent identifier as a parent organization URI
* Organization Types == $.type
* Additional RDF.type based on $.type
   * "DEPARTMENT": VIVO.Department unless a mapped institute, in which case VIVO.Institute
   * "DIVISION" or "SUBDIVISION": VIVO.Division unless a mapped institute, in which case VIVO.Institute
   * "ROOT": VIVO.University (Always Stanford University)
   * "SCHOOL": VIVO.School

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
* Person Affiliation is directly mapped from $.affiliations to http://sul.stanford.edu/rialto/ontology#
* Person Biograph: Person URI VIVO.overview $.bio.text (Literal)
* Country: dcterms:spatial http://sws.geonames.org/6252001/ (United States)
* Department (Organization) URI: $.titles.organization.orgCode through entity resolution otherwise skipped. 
* For each title in $.titles:
  * Person Position URI: Positions context URI + Person ID + "_" + Position Org Code
    * Person Position URI RDF.type VIVO.Position .
    * Person URI VIVO.relatedBy Person Position URI .
    * Person Position URI RDFS.label $.titles.label.text (Literal) .
    * Person Position URI VIVO.hrTitle $.titles.title (Literal) .
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
* Person URI VCARD.hasEmail $.primaryContact.email
* Sunetid: dcterms:identifier $.uid

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
* Abstract == `$.static_data.fullrecord_metadata.abstracts.abstract.abstract_text.p` (because string), else loop over `$.static_data.fullrecord_metadata.abstracts.abstract.abstract_text.p` (because array) and build up a string using concatenation (in array order)
* DOI == `$.dynamic_data.cluster_related.identifiers.identifier[?(@.type=='doi')].value`. failing that, `$.dynamic_data.cluster_related.identifiers.identifier[?(@.type=='xref_doi')].value`
* Title == `$.static_data.summary.titles.title[?(@.type=='item')].content`
* Date of Creation == `$.static_data.summary.pub_info.sortdate`
* Identifier == `$.dynamic_data.cluster_related.identifiers.identifier[*].value`
* Journal issue == `$.static_data.summary.titles.title[?(@.type=='source')].content`
* Publisher == `$.static_data.summary.publishers.publisher.names.name.display_name`
* Subject == Resolve `$.static_data.fullrecord_metadata.category_info.subjects.subject[?(@.ascatype=='extended')].content` with entity resolver or create a new DC.subject
* Sponsor (VIVO.informationResourceSupportedBy) == Resolve `$.static_data.fullrecord_metadata.fund_ack.grants.grant.grant_agency` with entity resolver or create new organization.
* Author / editor == Extract name strings from `$.static_data.summary.names.name`. For each named contributor, extract
their address if it exists, and pull out their `orcid_id`, `first_name`, `last_name`, and `full_name`. Resolved with entity resolver or create a person, where the URI for this person is based on an MD5 hash of their first name, a space, and their last name (all in lowercase).
If `role` is book_editor, then an editor, otherwise an author.
* Funded by (`VIVO.hasFundingVehicle`) == Resolve `$.static_data.fullrecord_metadata.fund_ack.grants.grant.grant_ids.grant_id` with entity resolver or create a new grant.

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

Default if none of the above is http://purl.org/ontology/bibo/Document.

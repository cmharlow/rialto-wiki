# Object Models

RIALTO is primarily interested in **Works** (articles, research output, publications, etc.), **Agents** (people, departments, agencies, organizations, etc.), **Grants**, and **Projects**. Each of these is represented by a data model that defines the scope of the entity and a metadata application profile that shows what information we capture about these entities for RIALTO's usage.

## Works (via Citations)

Works are publications of articles, research outputs, datasets, etc. Citation for a Work is the main reference point / datapoint. If feasible, the citation should link to manifestations of that Work (i.e. DOI).

* **Types**: Publication, Research Output, Articles, Dataset, … 
* **Sources**: Web of Science, SUL-PUB (should be subset of what is in WoS)

## Agents

Agents are some sort of actor involved in creating works or projects, or in supporting works or projects via grants or institutional support. 

* **Types**: People, Departments, Universities, Colleges, Organizations / Agencies >> Funders
* **Sources**: Stanford LDAP, CAP Profiles API (Stanford Affiliates scholarly record type info), ORCID & ISNI.

## Grants

Grants are awards for some project(s) or work(s), usually attached to one or more lead agents (PIs) whether people or departments, and awarded or funded by an organization or agency.

* **Types**: Governmental << Federal / State / Local, Private, Internal to Stanford, ... 
* **Sources**: Web of Science (funding agency string / grant number in metadata), SERA (not done yet)

## Projects

Projects here are research projects that are funded by grants or institutions, worked on by agents, and may produce multiple works. 
Sources: SERA (not done yet)

Domain Resource Application Profiles
Expectation key
Code
Description
M
Mandatory
M+
Mandatory if applicable
R
Recommended
R+
Recommended if applicable

Model Structural Overview
Works
Types: Publication, Research Output, Articles, … ?

Field
Predicate
Exp.
Card.
Value Type
Definition
























Agents
Types: People, Departments, Agencies >> Funders

Field
Predicate
Exp.
Card.
Value Type
Definition
























Grants
Types: Governmental << Federal / State / Local, Private, Internal to Stanford, other?

Field
Predicate
Exp.
Card.
Value Type
Definition
























Projects
Types: ??

Field
Predicate
Exp.
Card.
Value Type
Definition

























RIALTO is primarily interested in **Works** (articles, research output, publications, etc.), **Agents** (people, departments, agencies, organizations, etc.), **Grants**, and **Projects**. Each of these is represented by a data model that defines the scope of the entity and a metadata application profile that shows what information we capture about these entities for RIALTO's usage.

## Works (via Citations)

Works are publications of articles, research outputs, datasets, etc. Citation for a Work is the main reference point / datapoint. If feasible, the citation should link to manifestations of that Work (i.e. DOI).

* **Types**: Publication, Research Output, Articles, Dataset, Student Publication, … 
* **Sources**: Web of Science, SUL-PUB (should be subset of what is in WoS), Profiles

Field | Predicate | Expected Data Type | Cardinality | Value Type | Definition
----- | --------- | ------------------ | ----------- | ---------- | ----------

* subject heading information in publications
* topic area of research / work
* MESH headings
* date of publication / release / create
* authors
* publisher
* journal
* which publications resulted from which grants
* if from Profiles specifically or not (if approved by researcher)

## Agents

Agents are some sort of actor involved in creating works or projects, or in supporting works or projects via grants or institutional support. 

* **Types**: People, Student, Faculty, Researcher, Academic institutes, Departments, Universities, Colleges, Organizations / Agencies >> Funders
* **Sources**: Stanford LDAP, CAP Profiles API (Stanford Affiliates scholarly record type info), ORCID & ISNI.

Field | Predicate | Expected Data Type | Cardinality | Value Type | Definition
----- | --------- | ------------------ | ----------- | ---------- | ----------

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

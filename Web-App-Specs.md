Drawn from use cases written up in [our (private) Jira RIALTO repository](https://jirasul.stanford.edu/jira/secure/RapidBoard.jspa?rapidView=921&projectKey=RIALTO&view=planning).

# Generic Design Feel

https://drive.google.com/drive/u/1/folders/1d-UFRxmHDFsb8vDXQvkNGlR66Tb-KkWp


# Search interface

## Results (i.e. Entities that get indexed)
  - Grants
  - Publications
  - Projects
  - :star: Authors (co-authors), Faculty, Universities, Organizations, Departments < Agents

## Facets
  - result entities types
  - years range
  - :star: date range
  - topic areas
  - number of publications (related to Grant, by a Person, from a Person at an Organization)
  - institute
  - academic unit or department
  - department or other organizational unit (e.g. school)
  - grants
  - agent (research / faculty member)

# CSV Reports

:star: Authors joined with Co-Authors aggregate count of publications

Department | Institution | Author | Author's Co-Author | Co-Author Institution | Co-Author Department | Number of Collaborations | Co-Author Country
--- | --- | --- | --- | --- | --- | --- | ---
Chemistry  | Stanford    | John Smith | Jane Smith  | Harvard  | Biochemistry | 2 | USA
Chemistry  | Stanford    | John Smith | Jane Okoye  | Ghent    | Informatics  | 10 | Belgium
Medicine   | Stanford    | Lady Red   | Jane Okoye  | Ghent    | Informatics  | 10 | Belgium

:star: (this appears to be same as the report above) 

Author     | Institution | Co-Authors' Institution | Institution Country | Number of Collaborations | Co-Authors' Names
---------- | ----------- | ----------------------- | ------------------- | ------------------------ | -----------------
Jane Smith | Stanford    | Harvard                 | USA                 | 10 | Jane Smith, John Doe, Jake Okuma
Jane Smith | Stanford    | Ghent                   | Belgium             | 2 | Patrick Hoch, Richard Sanderson


Year | academic institute | topic area | number of publications by faculty members of institute in that topic area
---- | ------------------ | ---------- | -------------
2002 | school of medicine | biology    | 12
2002 | school of medicine | chemistry  | 30
2003 | school of medicine | chemistry  | 210

Publication   | Grant
------------- | ------
Publication 1 | Grant 1 
Publication 2 | Grant 1 
Publication 3 | Grant 1 
Publication 2 | Grant 2 
Publication 4 | Grant 2 

Author | Publications Count | Profiles-Sourced Publications Count | Number of times Cited
------ | ------------------ | ----------------------------------- | ---------------------
Jane Smith | 120 | 80 | 200
Clifford the Dog | 2 | 1 | 10

Department | Year | Journals | Count of Publications by Authors in Department
---------- | ---- | -------- | ----------------------------------------------
Chemistry  | 2002 | Science  | 5000
Chemistry  | 2003 | Science  | 2000
Biology    | 2016 | n+1      | 2


Department | Year | Publishers | Count of Publications by Authors in Department
---------- | ---- | ---------- | ----------------------------------------------
Chemistry  | 2002 | Elsevier   | 2
Chemistry  | 2014 | Springer   | 5
English    | 2015 | MLA        | 30

Department | # of Faculty Publications in Jan | ... Feb | ... March | ... April | ... May | ... June | ... July | ... Aug | ... Sept | ... Oct | ... Nov | ... Dev
---------- | --- | --- | ----- | ----- | --- | ---- | ---- | --- | ---- | --- | --- | ---
Chemistry  | 12  | 3   | 4     | 5000  |   2 |    0 |    2 |  10 | 2021 |  20 | 305 | 308
English    | 109 |   2 |    43 |   36  |  83 |   49 |    0 | 489 |  981 |  34 | 738 |  21

Department | Topics of Faculty Publications in Jan | ... Feb | ... March | ... April | ... May | ... June | ... July | ... Aug | ... Sept | ... Oct | ... Nov | ... Dev
---------- | --- | --- | ----- | ----- | --- | ---- | ---- | --- | ---- | --- | --- | ---
Chemistry  | Polymers, Astrochemistry  | Biochem   | Topic 2, Topic 3, Topic 4     | Topic 5  |  Topic 5, Topic 1, Topic 56 |    Topic 0 |   Topic 2 | Topic 10 | Topic 2, Topic 0, Topic 21 |  Topic 20 | Topic 3, Topic 0, Topic 5 | Topic 8

# Visualizations
  - given agent, heat map of the world with color coding on countries to indicate frequency of collaboration.  This is determined by looking at the countries in the addresses shown for co-authors of that agent's publications.  Questions: (1) Is an agent an aggregative thing (i.e. can it be a department, a school, a single person, all of Stanford)?  YES (2) Can we filter the publications used to create the heatmap by date range? YES
  - network visualization, showing institutions as nodes, with lines connecting the institutions represented by all co-authors of projects or works. The size of the nodes is determined by the number of authors at that institution. 

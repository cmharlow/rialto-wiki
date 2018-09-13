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
  - result entities types (e.g. publication, grant, person)
  -- number of publications is a value of this facet (related to Grant, by a Person, from a Person at an Organization)
  - date range (similar to "Last Accessioned" facet in Argo)
  - subject/topic area (i.e. dcterms:subject)
  - institute
  - academic unit or department
  - department or other organizational unit (e.g. school)
  - agent (researcher / faculty member)

# Reports

<a name="RIALTO8"></a>**Institution Collaboration Report** ([RIALTO-8](https://jirasul.stanford.edu/jira/browse/RIALTO-8))

Authors joined with Co-Authors aggregate count of publications by institution
```
Output:
A list of institutions the authors in that department have co-authored with, along with number of collaborations.

e.g.
University of California, Berkeley 456
Harvard University 200
etc.
```

***
**Country Collaboration Report** ([RIALTO-8](https://jirasul.stanford.edu/jira/browse/RIALTO-8))

Authors joined with Co-Authors aggregate count of publications by country
```
Output:
A list of countries that the authors in that department have collaborated with, along with the number of collaborations. 

e.g.
USA 1050
Canada 900
Italy 345
etc.
```

***
**Institution/Country Collaboration Raw Data Export** ([RIALTO-8](https://jirasul.stanford.edu/jira/browse/RIALTO-8))

Both of the above reports display a table on the screen.  In each case, the data is displayed on the screen (and used to create the choropleth in the case of the countries).  However, we will also provide the option to download the raw data used to create those aggregated reports in CSV export, so that the user can perform other analysis in a program like Excel.  The CSV export would include the following:
```
1) Stanford faculty member name
2) Stanford faculty member Org
3) Stanford faculty member's co-author name(s) -- could be many if they are at the same institution for a given paper
4) Stanford faculty member's co-author institution name
5) Stanford faculty member's co-author institution country

Note that the csv output below may have multiple rows per paper, if the paper has co-authors across multiple institutions.  In this case, there would be one row per unique institution of co-authorship.  In the case of only one co-authorship institution (i.e. one co-author, or many co-authors but all at the same institution), there will be one row for that publication.  The number of collaborations column counts the name of co-authors at the institution (will be at least one for each row).
```

Department | Institution | Author | Author's Co-Author | Co-Author Institution | Co-Author Department | Number of Collaborations | Co-Author Country
--- | --- | --- | --- | --- | --- | --- | ---
Chemistry  | Stanford    | John Smith | Jane Smith, XXX  | Harvard  | Biochemistry | 2 | USA
Chemistry  | Stanford    | John Smith | Jane Okoye, Patrick Hoch, XX, YY, etc.  | Ghent    | Informatics, Computer Science  | 10 | Belgium
Chemistry  | Stanford    | John Smith | Peter Smith, YY, ZZ, etc.  | Brussels U | Informatics  | 10 | Belgium
Medicine   | Stanford    | Lady Red   | Jane Okoye, YY, ZZ, etc.   | Ghent    | Informatics  | 10 | Belgium
Medicine   | Stanford    | John Doe   | Mary Cary   | Sorbonne    | Oncology  | 1 | France

***
**Research Trends Report** ([RIALTO-13](https://jirasul.stanford.edu/jira/browse/RIALTO-13))

Publication Topic Area(s): chemistry, art

academic institute | 2001 | 2002 | 2003
------------------ | ---- | ---- | ----
school of medicine | 12   |    8 |  92
school of art      | 30   |    0 | 103
hoover institution | 210  |   56 |  3

***
**Grant Publication Report** ([RIALTO-12](https://jirasul.stanford.edu/jira/browse/RIALTO-12))

Publication   | Grant
------------- | ------
Publication 1 | Grant 1 
Publication 2 | Grant 1 
Publication 3 | Grant 1 
Publication 2 | Grant 2 
Publication 4 | Grant 2 

***
**Researcher Publication Report** ([RIALTO-7](https://jirasul.stanford.edu/jira/browse/RIALTO-7))

Author | Publications Count | Profiles-Sourced Publications Count | Number of times Cited
------ | ------------------ | ----------------------------------- | ---------------------
Jane Smith | 120 | 80 | 200
Clifford the Dog | 2 | 1 | 10

***
**Journal Publication and Publisher Reports** ([RIALTO-10](https://jirasul.stanford.edu/jira/browse/RIALTO-10))

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

***
**Monthly Productivity Reports** ([RIALTO-16](https://jirasul.stanford.edu/jira/browse/RIALTO-16))

Department | # of Faculty Publications in Jan | ... Feb | ... March | ... April | ... May | ... June | ... July | ... Aug | ... Sept | ... Oct | ... Nov | ... Dev
---------- | --- | --- | ----- | ----- | --- | ---- | ---- | --- | ---- | --- | --- | ---
Chemistry  | 12  | 3   | 4     | 5000  |   2 |    0 |    2 |  10 | 2021 |  20 | 305 | 308
English    | 109 |   2 |    43 |   36  |  83 |   49 |    0 | 489 |  981 |  34 | 738 |  21

Department | Topics of Faculty Publications in Jan | ... Feb | ... March | ... April | ... May | ... June | ... July | ... Aug | ... Sept | ... Oct | ... Nov | ... Dev
---------- | --- | --- | ----- | ----- | --- | ---- | ---- | --- | ---- | --- | --- | ---
Chemistry  | Polymers, Astrochemistry  | Biochem   | Topic 2, Topic 3, Topic 4     | Topic 5  |  Topic 5, Topic 1, Topic 56 |    Topic 0 |   Topic 2 | Topic 10 | Topic 2, Topic 0, Topic 21 |  Topic 20 | Topic 3, Topic 0, Topic 5 | Topic 8

# Visualizations

**Country Collaboration Visualization** ([RIALTO-8](https://jirasul.stanford.edu/jira/browse/RIALTO-8))

See also the related [CSV and tabular output](#RIALTO8) associated with this visualization above.

Given agent, heat map of the world with color coding on countries to indicate frequency of collaboration.  This is determined by looking at the countries in the addresses shown for co-authors of that agent's publications.  
Questions: 
1. Is an agent an aggregative thing (i.e. can it be a department, a school, a single person, all of Stanford)?  YES 
1. Can we filter the publications used to create the heatmap by date range? YES

***
**Institution Collaboration Visualization** ([RIALTO-17](https://jirasul.stanford.edu/jira/browse/RIALTO-17))

Network visualization, showing institutions as nodes, with lines connecting the institutions represented by all co-authors of projects or works. The size of the nodes is determined by the number of authors at that institution. 

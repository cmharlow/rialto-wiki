RIALTO is built upon data aggregated from other systems, and as such, will largely reflect any data inconsistencies or errors that exists in these source system.  We are documenting here the sources of our data, along with instances of what appear to be inconsistent, missing or bad data and the source of this data.  This will allow for discussions on how to improve the source data, and thus improve its representation in RIALTO.

## People and Stanford Organizations (Departments, Institutes, Schools, etc.)

People data and their Stanford affiliations comes from the Profiles system (https://profiles.stanford.edu and https://cap.stanford.edu/cap-api/console).  In order to harvest this data into RIALTO, we 

* iterate over all Stanford Organizations represented in Profiles (including the hierarchy and unique codes) 
* iterate over all people represented in Profiles (by definition, Stanford only) and use the organization codes represented in their profiles to connect them to Stanford organizations

Thus the people and Stanford organizational units and the connections between these two entities rely on the data coming from the Profiles API.  We have found a handful of cases that appear to be "test users" in Profiles (e.g. people with names like "R25Test 25Live" and "Seriessupport 25Live") and we also have a large number of people which we were unable to connect to academic units due to invalid organization codes.  For now, these groups of people (likely undergraduates, affiliates and other non-Staff or Faculty positions) are associated with an "Unknown or unmapped" department.  

## Grants

Grants data comes from the SeRA API: https://asconfluence.stanford.edu/confluence/display/MaIS/SeRA+API+-+User+Documentation  

We harvest funded projects for Stanford researchers that are recorded in SeRA, including such as data as the name of the grant, the funder, and the PI.  We then attempt to link grants to publications via data pulled from our publications sources (noted below).

## Publications

Publication data comes from the [Web of Science API](https://developer.clarivate.com/apis/wos), a third party subscription product from [Clarivate](https://clarivate.com/).  In order to harvest publications, we iterate over all of the people in the RIALTO (pulled via the Profiles API as noted above), and search the Web of Science using their first and last name, and "Stanford".  The means we will only have publications from researchers that were published when they were affiliated with Stanford (in other words, researchers who came from a previous institution will not have publications returned from their previous institutions).  We will also have issues of false positives and negatives due the inherent ambiguities in name searching.  We hope to leverage unique researcher IDs such as ORCID in the future to help alleviate these issues.

Possible data sources for RIALTO Combine. ⭐️means in scope for RIALTO Phase 1 development work.


Source | URL | Data Example (link) | Notes
------ | --- | ------------------- | -----
⭐️CAP = Profiles API | GUI: https://profiles.stanford.edu/ ; CAP API: https://cap.stanford.edu/cap-api/console Or https://api.stanford.edu | https://gist.github.com/peetucket/07746abaa2b8d9bce7b38499cbeab9bb (for author) | SUL Pub only calls a subset of CAP, we need the full CAP API
⭐️Web of Science |  |  | 
⭐️Dimensions |  |  | 
⭐️SERA |  |  | Not done yet.
Stanford LDAP | [requesting access to LDAP](https://uit.stanford.edu/service/directory/access/requesting) |  | Subset of HR information? API access leveraging sunets only?
HR PeopleSoft Database |  |  | Likely not needed since we should have access to a more complete CAP API that will provide Agent data. No access? Fully included information (relevant for us) is in CAP already? (Some subset feeds into CAP, thus into SUL Pub)
SUL Pub === SUL CAP API | GUI: http://sulcap.stanford.edu/ ; API: ?? | https://gist.github.com/peetucket/f572c9fe678998cb785accc22d5b5b64 (sample results for 3 publications based on author search) | Pulls in subset of Web of Science, Pubmed, Profiles, CAP, Database access exists
US Spending (Not done yet) | https://api.usaspending.gov/ |  | Check Github for the API for the status
Grants.gov (Pointed to by Dept of Labor) | Lookup API? |  |
Data.gov |  |  | Same as or includes Grants.gov?
PubMED |  |  | All captured in SUL Pub already?
ORCID lookup API |  |  | 
ISNI lookup API |  |  | 
DOI lookup API? |  |  | 
SDR Metadata |  |  | (via PURL-Fetcher or write AWS-based API for this use case)

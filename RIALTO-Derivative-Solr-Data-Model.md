# Solr data model
All models have the following fields:

Field               | Expected Data Type | Cardinality | Definition
------------------- | ------------------ | ----------- | ----------------------
`id` | URI | 1 | The identifier of the resource
`type_ssi` | URI | 1 | This is a URI to one of the types in: https://github.com/sul-dlss/rialto/wiki/RIALTO-Data-Models-&-Profiles

## Person

Field               | Expected Data Type | Cardinality | Definition
------------------- | ------------------ | ----------- | ----------------------
`name_ssim` | String | 1 | The person's name

## Organization

Field               | Expected Data Type | Cardinality | Definition
------------------- | ------------------ | ----------- | ----------------------
`title_tesi` | String | 1 | The organization's name. Tokenized so that partial matches will occur.

## Project

Field               | Expected Data Type | Cardinality | Definition
------------------- | ------------------ | ----------- | ----------------------
`title_tesi` | String | 1 | The project's name. Tokenized so that partial matches will occur.
`alternative_title_tesim` | String | 0-n | The project's alternative title. Tokenized so that partial matches will occur.
`start_date_ssi` | String | 1 | The project's starting date.
`end_date_ssi` | String | 1 | The project's ending date.

## Grant

Field               | Expected Data Type | Cardinality | Definition
------------------- | ------------------ | ----------- | ----------------------
`title_tesi` | String | 1 | The grant's name. Tokenized so that partial matches will occur.

## Publication

Field               | Expected Data Type | Cardinality | Definition
------------------- | ------------------ | ----------- | ----------------------
`title_tesi` | String | 1 | The publication's name. Tokenized so that partial matches will occur.
`alternative_title_tesim` | String | 0-n | The publications's alternative title. Tokenized so that partial matches will occur.
`cites_ssim`| URI of a document| 0-n | Relates a document to another document that is cited by the first document as reference, comment, review, quotation or for another purpose.
`doi_ssim`|| 0-1 | Digital Object Identifier for the publication.
`identifier_ssim`| IRI | 1-n | Identifier for the resource. May be from multiple sources.
`link_ssim` | URI | 0-n | (Preferably, permanent) URL for accessing the resource on the internet.
`description_tesim` | String | 0-n | Description of the resource.
`funded_by_ssim` | Grant URI | 0-n | Grant (or contract) providing funding for the publication.
`publisher_label_tsim` | foaf:Organization URI | 0-n | Publisher of the resource.
`sponsor_label_tsim` | Agent URI | 0-n | Institution supporting the publication.
`has_instrument_ssim` | URI | 0-n | gcis:Instrument URI
`same_as_ssim` | URI | 0-n | Other resources (identified via URIs) that are the same as this resource.
`journal_issue_ssim` | URI | 0-n | Document URI (an Article)
`subject_label_ssim` | URI | 0-n | The URI for the subject

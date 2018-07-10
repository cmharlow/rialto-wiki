For production we have been asked (by Operations) to use our in-house DLSS Solr Cloud. However, due to development work being done in the near future on our Solr Cloud, and due to network/firewall requirements, we'll have to use a Solr instance in the AWS cloud for the moment.

## Basic Setup

Let's use a single, EC2-based Solr instance set up just like we would have it on our laptops. This should be good enough for development purposes, at least in the beginning. There are two Solr documentation pages that are relevant:

[SolrCloud AWS Tutorial](https://lucene.apache.org/solr/guide/7_2/aws-solrcloud-tutorial.html)<br/>
[Solr Installation Docs](https://lucene.apache.org/solr/guide/7_2/installing-solr.html)

The first URL shows how to configure and set up Solr to run in "cloud" mode in AWS. This could be a backup for us if we find that a single-instance EC2 box isn't beefy enough (until we can use the DLSS Solr Cloud).
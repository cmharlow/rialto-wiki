Michael Klein from Northwestern agreed to share some notes on how they are deploying Solr to AWS.

# Architecture

![Northwestern AWS Solr Architecture Diagram](https://user-images.githubusercontent.com/131982/42899244-4d1b3ece-8a7a-11e8-8b55-579c24757b3f.png)

# Notes

> `solrcloud-solr` and `solrcloud-zookeeper` are both Elastic Beanstalk environments running the Multicontainer Docker platform.
> 
> 3 solr containers point to 2 zookeeper containers via a round-robin Route53 record. All containers are hosted on their own instances, _but_ I have some ideas about changing this.
> 
> `solr-backup-volume` is an EFS volume that is mounted onto all three solr instances and then projected into their containers. This happens via an idempotent `.ebextensions` config script that runs when the app is deployed. Since the same volume is visible to all three solr containers, the Solr Collections API can be used to backup and restore collections.
>
> The volume is also mounted to our bastion host, which is where the cron job runs that performs our twice daily solr backups.
> 
> Our Elastic Beanstalk applications (which is where the `.ebextensions` stuff lives) are all under https://github.com/nulib/nulterra/tree/master/stack/applications. They’re only “applications” in the sense that they include EB configuration and deployment info. The actual applications are in Docker containers that these things point to.
> 
> Our containers are hosted at https://hub.docker.com/u/nulib/ and our Dockerfiles etc. are at https://github.com/nulib/docker-images (which is thus far lacking in documentation).
> 
> We run _everything_ under docker now – Solr, Zookeeper, Fedora, Cantaloupe, and our Samvera Rails applications.
> 
> Zookeeper has a built in mechanism to write its backups to S3, so we just use an environment variable to point it to the bucket and we’re good to go.
> 
> We also have automated docker builds and deployments to both staging and production triggered by pushes to magic branch names.

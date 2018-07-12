For production we have been asked (by Operations) to use our in-house DLSS Solr Cloud. However, due to development work being done in the near future on our Solr Cloud, and due to network/firewall requirements, we'll have to use a Solr instance in the AWS cloud for the moment.

## EC2 Setup

We are using a single EC2 instance to run Solr. "Instance" is the Amazon word for "server". You can't call it a "server" if it runs in the cloud, because that word is old-school and implies that somewhere there is hardware that runs your code.

1. Log in at [https://console.aws.amazon.com](https://console.aws.amazon.com) and be sure to switch to the "DevelopersRole"
2. Make sure you're using AWS region `us-east-1` (N. Virginia). This is where we run everything RIALTO-related, so don't provision anything in any other regions.
3. Choose the EC2 service, and press "Launch Instance". Your configuration choices should be:
   * `Amazon Linux 2 AMI (HVM), SSD Volume Type`
   * `t2.medium`
   * `rialto-core` Subnet (we use this VPC for everything, so everything RIALTO that lives in AWS can talk to everything else)
   * 24G of `General Purpose SSD (GP2)`
   * Add a Name tag for your new EC2 instance (this is optional, but makes life easier later)
   * Select the existing `rialto-core` security group
4. You should now see your instance starting up in the EC2 console. Confirm in the `Description` tab that there is an assigned address under the `Public DNS (IPv4)` field. If this is not the case, follow the steps in [https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-ip-addressing.html#subnet-public-ip](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-ip-addressing.html#subnet-public-ip) to enable auto-assignment of public IP addresses for your instances.
5. Assign a persistent IP address. This is done by associating an [Elastic IP](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html#ip-addressing-eips) with your instance.
6. Set up outside network access. It's easiest to require users/team members to use **full tunnel** Stanford VPN. The IP ranges for the Stanford VPN are documented [here](https://uit.stanford.edu/guide/lna/network-numbers). Under the `Network & Security` heading in the left sidebar of the AWS Console page, choose the `Security Groups` link. Then choose the `rialto-core` security group and click `Actions` - `Edit Inbound Rules`.
   * Add one SSH rule per Stanford VPN IP range (port 22)
   * Add one TCP rule per Stanford VPN IP range for accessing the Solr admin page (we'll use the Solr default of port 8983)
7. Check if the storage on your EC2 instance is persistent or not.
   * `aws ec2 describe-instances --instance-ids <instance_id> --region us-east-1 --profile dlss-DevelopersRole`
   * If the returned JSON has `DeleteOnTermination` set to `true` under `BlockDeviceMappings` then storage is NOT persistent and you need to complete step 8 below.
8. Set your EC2 storage to be persistent by changing the `DeleteOnTermination` property to `false`.
   *  `aws ec2 modify-instance-attribute --instance-id <instance_id> --block-device-mappings file://ec2_persist_mapping.json --region us-east-1 --profile dlss-DevelopersRole`
   * The contents of `ec2_persist_mapping.json`: 
```
[
  {
    "DeviceName": "/dev/xvda",
    "Ebs" : {
        "DeleteOnTermination": false
    }
  }
]
```

## Solr Setup

You should now be able to SSH into your EC2 instance, provided that you've [created a key pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html). Copy the command you get when you press the `Connect` button under `Instances` in the EC2 console, and run it to get a shell on your instance.

1. Install Java: `sudo yum install java`
2. Set the maximum number of open files and processes available to the solr user to be 65000 for both. Edit `/etc/security/limits.conf` to achieve this.
3. Download and install Solr as described on the [Taking Solr to Production](https://lucene.apache.org/solr/guide/7_4/taking-solr-to-production.html#run-the-solr-installation-script) page.



Let's use a single, EC2-based Solr instance set up just like we would have it on our laptops. This should be good enough for development purposes, at least in the beginning. There are two Solr documentation pages that are relevant:

[SolrCloud AWS Tutorial](https://lucene.apache.org/solr/guide/7_2/aws-solrcloud-tutorial.html)<br/>
[Solr Installation Docs](https://lucene.apache.org/solr/guide/7_2/installing-solr.html)

The first URL shows how to configure and set up Solr to run in "cloud" mode in AWS. This could be a backup for us if we find that a single-instance EC2 box isn't beefy enough (until we can use the DLSS Solr Cloud).

Key setup steps:

* Choose _Amazon Linux AMI, SSD Volume Type_ as the AMI when setting up the EC2 instance
* t2.medium should be sufficient
* Follow the [SolrCloud AWS Tutorial](https://lucene.apache.org/solr/guide/7_2/aws-solrcloud-tutorial.html) but just install a single Solr instance on one node.
* Once you've verified that you can reach the EC2 Solr, manually set the EC2's storage to be persistent:

`aws ec2 modify-instance-attribute --instance-id <instance_id> --block-device-mappings file://ec2_persist_mapping.json --region us-east-2 --profile dlss-DevelopersRole`

Contents of `ec2_persist_mapping.json`:

```
[
  {
    "DeviceName": "/dev/xvda",
    "Ebs" : {
        "DeleteOnTermination": false
    }
  }
]
```
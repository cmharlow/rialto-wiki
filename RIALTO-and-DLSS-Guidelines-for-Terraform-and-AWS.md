We prefer to use the open source [Terraform](https://www.terraform.io/docs/index.html) tool to define our Amazon Web Service [infrastructure as code](https://www.thoughtworks.com/insights/blog/infrastructure-code-reason-smile). Terraform can work with all the major cloud computing providers, not just AWS.

## AWS Guidelines

### AWS Regions

* **Dev environment:** Any US-based region is fine, with a preference to us-west-2 (Oregon) as the default, just so it's easier to find stuff.
* **Stage & Production:** Use us-west-2 (Oregon), unless:
  * The service you require isn't available in that region OR
  * You're implementing a multi-region service and already have the stack spun up in us-west-2, in which case, your second region is us-east-1.
  * If you need 3 or more regions, pick whatever makes sense to you for the 3rd region and above, as long as it's documented.
* In all cases, DO NOT use any region outside the United States. If you have a use case that may require an international region, bring it to Direct.


### The Stage Environment

* Stage is to verify production code, prior to deploying into production.
* Stage is transient. We do not leave systems (ECS instances, EC2 instances, RDS instances)  running in stage. We either:
  * Push to stage, verify code works, then tear down OR
  * Push to stage, verify code works, then push to prod and tear down.
* We explicitly DO NOT push to stage, then leave it running over the weekend. However, it is OK to let S3 buckets and EFS content persist in stage, if it's got sample data in it that's different from production and would be a pain to re-populate for every deploy.


### Containerize Whenever Possible

Our default plan is to follow [UIT's principles for server/infrastructure management](https://uit.stanford.edu/cloud-transformation/principles-and-practices-all-servers), and only deviate where necessary. In particular, observe the following guidelines:

* Consider Docker first. Can you do it with a Docker container? Then do it that way.
* If Docker won't work, build a [custom AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html). The running EC2 instance isn't patched; instead, rebuild the AMI with necessary updates and redeploy.
* If neither of the above options work then run an EC2 instance with puppet on it, and manage it as a traditional VM. This is not a good choice, so we should really try avoid this.


## Terraform Guidelines

### Modules

In Terraform, [modules](https://www.terraform.io/docs/modules/index.html) are essentially special directories that let you group together infrastructure definitions in order to reuse them later. The recommended structure for a module is laid out [here](https://www.terraform.io/docs/modules/create.html#standard-module-structure).

At DLSS, we observe the following guidelines regarding modules:

* When writing significant chunks of Terraform code, organize them in modules whenever possible.
* Consider breaking modules up into stand-alone GitHub repositories for versioning, for example the [terraform-aws-lambda repository](https://github.com/sul-dlss-labs/terraform-aws-lambda), which is used to create lambda functions.

### Pull Requests

Just as for regular application code, we require PR review for changes to our Terraform code. We observe the following guidelines:

* Anyone with access can merge & apply PRs on dev or stage. The person who merges is also responsible for running terraform-apply.
* Only Ops can merge and apply PRs against the production environment. The person who merges is also responsible for running terraform-apply. Production merge privileges will be granted to anyone who wishes and is capable of being on the ops on-call rotation.
* Note that the use of Terraform is only required for stage and production. In the development organization you can use whatever you want.
* At this time, we have decided not to automate `terraform apply`. We explicitly want a firebreak between approving a PR in the GUI and a change making it into production and potentially breaking things.

### State Locking

[State locking](https://www.terraform.io/docs/state/locking.html) is already configured in Terraform.  We used [Terragrunt](https://github.com/gruntwork-io/terragrunt) internally earlier, but then Terraform itself added locking.


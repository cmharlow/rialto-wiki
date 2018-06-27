For AWS work at DLSS, we are attempting a new process:
- all DLSS folks have user accounts within a AWS Organization call `sul-dlss-users`;
- for a 'Dev' AWS environment, there is a `sul-dlss-development` organization, within with a shared `DevelopersRole` has all the permissions for developers working in that environment;
- for a 'Stage' AWS environment, there is a `sul-dlss-stage` organization, which is built via Terraform;
- and for the 'Prod' AWS environment, there is a `sul-dlss-prod` organization, which is built via Terraform.

The instructions below go through setting up access to `sul-dlss-development` after Ops has made you a user of `sul-dlss-users`. If you do not have a `sul-dlss-users` login, chat with our friendly Ops colleagues. This will eventually be open to all of DLSS via a mechanism like shib, but right now, it is limited to projects needing AWS development access right away.

# Accessing your `sul-dlss-users` & `sul-dlss-development` User Accounts

1. Go to http://console.aws.amazon.com/.
2. Log into `sul-dlss-users` with your relevant account, with the Account Alias (top field) as `sul-dlss-users`, then your username and password. *NB: this does not correspond with user accounts in `sul-dlss` or other DLSS projects in AWS (like dlme, hybox, or others).*
3. Once in your user account, you can assume the DevelopersRole in `sul-dlss-development` (our AWS development environment) by going to `your username @ sul-dlss-users`, clicking to expand the menu, then selecting `switch role`.
4. In the `Switch Role` login page, enter Account: `sul-dlss-development`, Role: `DevelopersRole` (case sensitive), and optionally rename the role in Display Name. Then click `Switch Role`.
5. The top right corner should now show `DevelopersRole @ sul-dlss-development` (or whatever you changed the Display Name to in the last step). You now have access to the `sul-dlss-development` environment as a generic `DevelopersRole` user.
6. To switch back to your username in the `sul-dlss-users` console, go to `DevelopersRole @ sul-dlss-development` in the top right corner, click to expand the menu, then select `Back to [your username]`.

# Set up AWSCLI for `sul-dlss-user`

NB: You need to do this before you can set up AWSCLI (or AWS command line access) to the `sul-dlss-development` environment.

![](https://files.slack.com/files-pri/T7SAV7LAD-FBEKSL602/image.png)

- for awscli (aws command line) setup - first of all, you have the aws command line tool installed?
- here's the installation instructions in case now: https://docs.aws.amazon.com/cli/latest/userguide/installing.html

once installed, you're going to set up 2 profiles: 1 for your new sul-dlss-users account, then one from the developersRole in the sul-dlss-dev account
rad
to set up for sul-dlss-users awscli account, under your sul-dlss-users login in the console. go to iam > users > your name (click on it)
on the summary page for you as a use, go to the security credentials tab
then under Access Keys, create access key, which will create a CSV that downloads to your computer with your access id and access secret key
once you have that, go to your terminal and run `aws configure --profile your-user-profile-name`
enter the keys from your csv as requested by the prompt, then for region enter `us-east-1`, and for data output, `json`
once done, if you run this: `aws sts get-caller-identity --profile your-user-profile-name`
you should get something like this:
```{
    "UserId": "fsajfkela;ks",
    "Account": "390882271260",
    "Arn": "arn:aws:iam::390882271260:user/jgreben"
}```
or whatever your username is.

/Users/jgreben/Projects> aws sts get-caller-identity --profile jgreben
{
    "Account": "390882271260", 
    "UserId": "AIDAI5IHA76O2LAOYX3W6", 
    "Arn": "arn:aws:iam::390882271260:user/jgreben"
}
so now we're going to set up a separate awscli profile for the developer role
so enter this: `aws sts assume-role --role-session-name DevelopersRole --role-arn arn:aws:iam::418214828013:role/DevelopersRole --profile jgreben`
and that will give you the info back you need to set up the new profile for the devRole
then next enter `aws configure --profile your-dev-role-profile-name`
and for the access key, secret access key use what was returned in the previous (sts assume-role) command (edited)
region still `us-east-1` and output `json`

cool, now, we're going to edit your awscli config to allow the assumption of the role
edit your .aws config file - `vi ~/.aws/config` (or however)
at the bottom of that file you'll see the devRole you just added
update to be this:
```[profile dev-role-name]
output = json
role_arn = arn:aws:iam::418214828013:role/DevelopersRole
region = us-east-1
source_profile = jgreben```
close + save, then run:
`aws sts get-caller-identity --profile dev-role-profile`
and should get:
```{
    "Arn": "arn:aws:sts::418214828013:assumed-role/DevelopersRole/botocore-session-1530058103",
    "Account": "418214828013",
    "UserId": "AROAJ7JRYIGG6BTR27C6G:botocore-session-1530058103"
}```
now you can run the aws cli with the assumed role
so as for the permissions on that developersRole - its meant to be open but its not entirely open yet
you can see here any example PR for adding permissions to the role: https://github.com/sul-dlss/terraform-aws/pull/45
and tag kam or jon to review those
some things they can give blanket access to (i.e. neptune:*) but other things they can't (iam or the user management stuff)
so for things like iam, we're trying to add specific permissions as we run into them, and in the PR, mention what exactly we were trying to do when hitting the block
for anything else you run into an error for that isn't a clear permissions PR, i've been trying to put them on the ops channel in slack so they can know and multiple people can follow along with fixing
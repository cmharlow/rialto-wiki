For AWS work at DLSS, we are attempting a new process:
- all DLSS folks have user accounts within a AWS Organization call `sul-dlss-users`;
- for a 'Dev' AWS environment, there is a `sul-dlss-development` organization, within with a shared `DevelopersRole` has all the permissions for developers working in that environment;
- for a 'Stage' AWS environment, there is a `sul-dlss-stage` organization, which is built via Terraform;
- and for the 'Prod' AWS environment, there is a `sul-dlss-prod` organization, which is built via Terraform.

The instructions below go through setting up access to `sul-dlss-development` or `sul-dlss-staging` after Ops has made you a user of `sul-dlss-users`. If you do not have a `sul-dlss-users` login, chat with our friendly Ops colleagues. This will eventually be open to all of DLSS via a mechanism like shib, but right now, it is limited to projects needing AWS development access right away.

# Accessing your `sul-dlss-users` & `sul-dlss-development` User Accounts

1. Go to http://console.aws.amazon.com/.
2. Log into `sul-dlss-users` with your relevant account, with the Account Alias (top field) as `sul-dlss-users`, then your username and password. *NB: this does not correspond with user accounts in `sul-dlss` or other DLSS projects in AWS (like dlme, hybox, or others).*
3. Once in your user account, you can assume the DevelopersRole in `sul-dlss-development` (our AWS development environment) by going to `your username @ sul-dlss-users`, clicking to expand the menu, then selecting `Switch Role`.
4. In the `Switch Role` login page, enter Account: `sul-dlss-development`, Role: `DevelopersRole` (case sensitive), and optionally rename the role in Display Name. Then click `Switch Role`.
5. The top right corner should now show `DevelopersRole @ sul-dlss-development` (or whatever you changed the Display Name to in the last step). You now have access to the `sul-dlss-development` environment as a generic `DevelopersRole` user.
6. To switch back to your username in the `sul-dlss-users` console, go to `DevelopersRole @ sul-dlss-development` in the top right corner, click to expand the menu, then select `Back to [your username]`.
7. To set this up for `sul-dlss-staging`, do the same as step four, but choose Account: `sul-dlss-staging`.  
8. The past 4-5 accounts you have set up will stay in the menu there, letting you select them without having to retype. 

# Set up AWSCLI for `sul-dlss-user`

NB: You need to do this before you can set up AWSCLI (or AWS command line access) to the `sul-dlss-development` environment. You will end up with **2 awscli profiles**, one for your user account in `sul-dlss-users`, and one for the shared `DevelopersRole` in `sul-dlss-development`.
 
NB: Install the AWS command line tool (awscli) if you haven't already before proceeding: https://docs.aws.amazon.com/cli/latest/userguide/installing.html

1. In the AWS console (i.e. webpage), log in as your user account within `sul-dlss-users` (see above).
2. Using the top left `Services` dropdown, select `IAM`. 
3. In the "Identity and Access Management" (IAM) console page, using the side navigation, select `Users`. 
4. Find your username and click on it.
5. On the summary page for your username account, go to the `Security Credentials` tab, then under Access Keys, click `Create access key`, which will create & download a CSV to your computer with your access id and access secret key.
6. Once you have that, go to your terminal and run `aws configure --profile your-user-profile-name` (`your-user-profile-name` can be whatever you want for labeling your `sul-dlss-users` account).
7. When prompted, enter the keys from your downloaded CSV as requested, then for region enter `us-east-1`, and for data output, `json` (unless you want something other than json).
8. Once done, if you run this: `aws sts get-caller-identity --profile your-user-profile-name`
you should get something like this (except with real UserId & Account entries):

```json
{
    "UserId": "fsajfkela;ks",
    "Account": "fjkdl;afjsakl;",
    "Arn": "arn:aws:iam::390882271260:user/your-sul-dlss-users-username"
}
``` 

You can now use awscli with your `sul-dlss-users` account by applying the `--profile your-user-profile-name` flag to your commands.

# Set up AWSCLI for `sul-dlss-development`

Now we're going to set up a separate awscli profile for the shared developer role within `sul-dlss-development`. You must have done the awscli setup above for your account in `sul-dlss-users` first!

1. In your terminal, enter: 
```bash
aws sts assume-role --role-session-name DevelopersRole --role-arn arn:aws:iam::418214828013:role/DevelopersRole --profile your-user-profile-name
``` 
where `your-user-profile-name` is what you set above for awscli to `sul-dlss-users`. Save the response somewhere handy, as that gives you the information back you need for the next steps.
2. Again in your terminal, enter `aws configure --profile your-dev-role-profile-name` (`your-dev-role-profile-name` can be whatever you want for labeling your use of the shared DevelopersRole within `sul-dlss-development`).
3. When prompted, enter the access key and secret access key based on the keys returned in the step 1 (`sts assume-role`) command. Leave region as `us-east-1` and output as `json` (unless you prefer some other output).
4. Now we're going to edit your local awscli config to allow the assumption of the role via awscli profile. Edit your aws config file by using in the terminal `vi ~/.aws/config` (or whatever editor you want to use).
5. at the bottom of that config file, you'll see the `your-dev-role-profile-name` you just added. Update that entry to be this, entering `your-user-profile-name` from the above `sul-dlss-users` awscli configuration in the `source_profile` field: 

```ini
[profile your-dev-role-profile-name]
output = json
role_arn = arn:aws:iam::418214828013:role/DevelopersRole
region = us-west-2
source_profile = your-user-profile-name
```

6. Close + save the update config file, then in a terminal, run `aws sts get-caller-identity --profile your-dev-role-profile-name`. You should get a response like (except with real identifiers):

```json
{
    "Arn": "arn:aws:sts::418214828013:assumed-role/DevelopersRole/botocore-session-47478484848",
    "Account": "418214828013",
    "UserId": "AFSJDKSAFJKFDJSAK:botocore-session-47478484848"
}
``` 

Now you can run the awscli with the shared DevelopersRole within the `sul-dlss-development` environment by using the `--profile your-dev-role-profile-name` flag at the end of the awscli commands.

# A Note on Shared DevelopersRole Permissions

As for the permissions on that shared DevelopersRole within `sul-dlss-development` environment - its meant to be open for development usage, but its not entirely open yet. You can see here an example PR for adding permissions to the role: https://github.com/sul-dlss/terraform-aws/pull/45

Usually Ops can give blanket access to resources (i.e. `neptune:*`), but there may be things where they only wish to give access to specific operations for that research (such as read but not write).  In the PR, mention what exactly we were trying to do when hitting the block so Ops can adequately decide if to grant full development environment permissions for that scenario.

For anything else you run into or errors that aren't a clear permissions PR, put them on the Ops channel in Slack so they can know and multiple people can follow along with fixing.
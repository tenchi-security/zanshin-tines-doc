# Zanshin AWS Accounts Auto Onboarding with Tines

### The goal of this story is to search for your AWS Accounts missing in the Zanshin and import them into Zanshin as scan targets pending.


## Necessary Permissionss

* Zanshin: The API key needs to be owned by an admin of the organization.
* AWS: An assume role with list.accounts only in the administration account.


##  Credentials Variables

* aws: The assume role ARN ID.
* zanshin: API Key from Zanshin portal.
* zanshin_org_id: The organization ID from Zanshin dashboard.


## In Zanshin

* Create an API key in the Zanshin Portal
  1) Go to Settings.
  2) Click on "API Keys".
  3) New API Key.
  4) For easy identification, put "Tines" in the name field and click on save.
  5) Copy the API key and put it in a safe place. (We will use it later).

* Organization ID
  1) Go to Settings.
  2) Take a look at the top of the page and you will see the Organization ID, copy it.

## In AWS

* Create an Assume Role
  1) Log into administration/organization account in the AWS.
  2) Go to IAM and create this policy:
```
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "organizations:ListAccounts",
            "Resource": "*"
        }
    ]
}
```
  3) Go to IAM and create a new role for Tines use it.
  4) Select the "AWS Account" option.
  5) Select "Another AWS account" and insert the Tines account number (See in "In Tines" Session).
  6) Flag the option that requires the External ID and insert the Tines External ID (See in "In Tines" Session).
  7) Select the policy you created above.
  8) Give the name to the role and click on create.
  9) Copy the ARN of this role.

## In Tines

* Create a New Story
  1) Click on New Story it will open a new window, click on "More Examples" and search for "Zanshin" and select the "Automate AWS Accounting onboarding to Zanshin" and click on "Import to tenant".
  2) Or click on this link: https://www.tines.com/story-library/1187255/automate-aws-accounting-onboarding-to-zanshin and click on "Import to tenant".

* Create the Credentials Variables
  1) Click out of actions and you will see "Credentials" and "Resources" with missing alerts.
  2) aws: 
  - Click on "+" to add a new credential, select AWS.
  - Give this name "aws_arn_role".
  - Left "Authentication type" as "Role-based access".
  - Left the others default options and click on save.
  - Click on "aws_arn_role" -> Details and copy the Account ID and External ID (You will need to use this in the "In AWS" session above).
  - Insert the ARN of the role that you created in the "In AWS" session above.
  - Click on Save.
  3) zanshin:
  - Click on "+" to add a new credential, select Text.
  - Give this name "zanshin_api".
  - In the value field, insert the API Key that you created in the "In Zanshin" session above.
  - Left the other options default and click on save.
  4) zanshin_org_id:
  - In "Ressources" click on "+" to add a new resource.
  - Give this name "org_id".
  - On the builder field, insert the Organization ID that you saw in the "In Zanshin" session.

    Email:
  - Go to "Send Email" action.
  - On recipients, choose List and put the emails to receive alerts about new accounts.
  - On Reply to, put the email that will receive replies to enable replies.
  - Keep the sender as Zanshin.

## Schedule

To schedule the story, click on the first action "List accounts in AWS Organization", click on "Status" and finaly click on "+" schedule.


## Now, you should be able to run the story and see the missing accounts appears in Zanshin.


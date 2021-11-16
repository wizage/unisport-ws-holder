## Setting up Amplify CLI
In this workshop we will be using the Amplify CLI to orchestrate the spinning up of resources in our AWS Accounts. To provide the account details and to spin up the resources you will need to configure your AWS CLI credentials.

  <details>
      <summary>Event Engine Setup</summary>

  1. Navigate to your Event Engine dashboard: https://dashboard.eventengine.run/dashboard (Login details will be provided ahead of the workshop)
  1. Click on `AWS Console` button
  1. A popover will appear with your AWS console access federation link and AWS CLI commands
  1. Open up your AWS profile folder on your computer ( `~/.aws/` for Mac and Linux and `C:\Users\USERNAME \.aws\` for windows)
  1. If you don't have a AWS profile folder you need to create it and add in two files. One file called `credentials` and `config`.
  1. Edit your `credentials` file by adding in a new profile like so (copying the values from the popover in event engine). Please note that the credentials file is all lowercase (in Event Engine it is uppercase).
      ```
      [ee]
      aws_access_key_id = XXXXXXXXXXXXXXXX
      aws_secret_access_key = XXXXXXXXXXXXXXXXXXXXXXXXX
      aws_session_token = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
      ```
  1. Edit your `config` file by adding default values (changing your region to the assigned region of your event)
      ```
      [ee]
      region = us-west-2
      output = json
      ```
  1. When running `amplify init` choose the newly created profile called `ee` (**Note:** please don't select default)
  </details>
  <details>
      <summary>Cloud 9 Setup (both Event Engine or Personal Account)</summary>

  1. You should of setup a Cloud9 environment in the previous instructions. If you have not navigate back [here](./)
  1. To properly configure the Amplify CLI you will need to run a command to setup the CLI.
      ```
      cp ~/.aws/credentials ~/.aws/config
      ```
  </details>
  <details>
      <summary>Cloud 9 Setup (both Event Engine or Personal Account)</summary>

  1. Using a personal account means you need to configure your AWS CLI to the right account you are using for the workshop.
  1. If you have the AWS CLI installed you can simply configure your credentials via with your new credentials.
      ```
      aws configure --profile <profilename>
      ```
  1. If you do not have the AWS CLI installed you can open up your AWS profile folder on your computer ( `~/.aws/` for Mac and Linux and `C:\Users\USERNAME \.aws\` for windows)
  1. f you don't have a AWS profile folder you need to create it and add in two files. One file called `credentials` and `config`.
  1. Edit your `credentials` file by adding in a new profile like so
      ```
      [ee]
      aws_access_key_id = XXXXXXXXXXXXXXXX
      aws_secret_access_key = XXXXXXXXXXXXXXXXXXXXXXXXX
      ```
  1. Edit your `config` file by adding default values. Note you might need to change your region
      ```
      [ee]
      region = us-west-2
      output = json
      ```
  </details>

## Amplify CLI Questions

In this section you will be creating an Amplify Project that will be using for the duration of the workshop.

1. Navigate to the project folder you downloaded at the beginning of this workshop and open up a terminal window at the root folder.

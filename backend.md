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
      <summary>Local Desktop</summary>

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

1. Navigate to the UnicornSports folder you downloaded at the beginning of this workshop and open up a terminal window at the root folder.

    | ![Project Starting LS](/backend-screenshots/startLS.png) |
    | :--: |
    | <b>Sample `ls` command in the UnicornSports directory </b> |

1. Now that you are in the UnicornSports folder, you can run 
    ```
    amplify init
    ```
1. You will be asked to provide a project name. The default project name will work for this. You can just press `<Enter>`
    <pre>
    ? Enter a name for the project <b>unicornsports</b>
    </pre>
1. The CLI will identify which type of project you will be building. The default should look like what is below. If you don't see the correct information check that you are in the right folder.
    <pre>
    Project information
    | Name: <b>unicornsports</b>
    | Environment: <b>dev</b>
    | Default editor: <b>Visual Studio Code</b>
    | App type: <b>javascript</b>
    | Javascript framework: <b>react</b>
    | Source Directory Path: <b>src</b>
    | Distribution Directory Path: <b>build</b>
    | Build Command: <b>npm run-script build</b>
    | Start Command: <b>npm run-script start</b>
    </pre>
    > Note: `Default Editor` can be changed or maybe different.
1. If everything is correct you can answer the CLI prompt with `y`
    <pre>
    ? Initialize the project with the above configuration? <b>Y</b>
    </pre>
1. Next it will prompt you to provide a authentication method you would like to use for setting up your AWS resources and select which profile you would like to use. If you are using Cloud9 select `default`, otherwise select the profile you configured earlier.
    <pre>
    ? Select the authentication method you want to use: <b>AWS profile</b>
    ? Please choose the profile you want to use <b>default</b>
    </pre>
1. At this point we will wait for the initialization of our AWS Account to happen. This inital CloudFormation will spin up a brand new S3 bucket to hold the CloudFormation files and create a few placeholder roles for Auth'd and Unauth'd users.
1. When the Cloudformation is completed you should some text like below. If you do not, check out the FAQ section in the wiki.
    ```
    ✔ Successfully created initial AWS cloud resources for deployments.
    ✔ Initialized provider successfully.
    Initialized your environment successfully.

    Your project has been successfully initialized and connected to the cloud!

    Some next steps:
    "amplify status" will show you what you've added already and if it's locally configured or deployed
    "amplify add <category>" will allow you to add features like user login or a backend API
    "amplify push" will build all your local backend resources and provision it in the cloud
    "amplify console" to open the Amplify Console and view your project status
    "amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

    Pro tip:
    Try "amplify add api" to create a backend API and then "amplify publish" to deploy everything
    ```
1. Now that we have our environment stood up lets get to adding our backend responsable to creating our live streams and holding our metadata. To start we will run this command:
    ```
    amplify add video
    ```
1. After running the commands it will prompt you with some questions to spin up the right video resources.
    <pre>
    ? Select from one of the below mentioned services: <b>Live Streaming</b>
    ? Provide a firendly name for your resource to be used as a label for this category in the project: <b>myivs</b>
    </pre>

    > Today we will be focusing on building out a Live Streaming Video Management System. If you are interested in building out Video-On-Demand checkout our workshop Unicornflix

    <pre>
    ? Do you want to create a single channel or an API to manager multiple channels? <b>Video Management Service</b>
    ? Choose the default stream quality: <b>Basic (SD Stream)</b>
    ? Choose the default stream latency type: <b>Ultra-low latency (~5 seconds)</b>
    </pre>

    > Today for the workshop we will be setting up the stream quality to SD Stream to save on bandwith due to a lot of users spinning up streams. You can also use Amplify Video to create a single channel as well.

    <pre>
    ? Select your Auth Model: <b>Auth</b>
    </pre>

    > This will configure Cognito to be used for your authentication model. In an extension we will talk about using API Key to do advanced Auth method to allow Unauth'd users to browse chanels.
1. Now that you have configured your projects backend you can now push your resources by running this command: 
    ```
    amplify push
    ```
    <pre>

    </pre>

1. Now you are prompted with a few question for codegen and to verify you want to push. 
    <pre>
    ✔ All resources copied.

        Current Environment: dev
        
    ┌──────────┬────────────────────┬───────────┬───────────────────┐
    │ Category │ Resource name      │ Operation │ Provider plugin   │
    ├──────────┼────────────────────┼───────────┼───────────────────┤
    │ Auth     │ VideoAuth          │ Create    │ awscloudformation │
    ├──────────┼────────────────────┼───────────┼───────────────────┤
    │ Api      │ VideoManagementApi │ Create    │ awscloudformation │
    ├──────────┼────────────────────┼───────────┼───────────────────┤
    │ Video    │ myivs              │ Create    │ awscloudformation │
    └──────────┴────────────────────┴───────────┴───────────────────┘
    ? Are you sure you want to continue? (Y/n) <b> Y </b>
    ? Do you want to generate code fro your newly created GraphQL API <b> Y </b>
    ? Choose your code generation language target <b> javascript </b>
    ? Enter the file name pattern of graphql queries, mutations and subscriptions <b>src/graphql/**/*.js</b>
    ? Do you want to generate/update all possible GraphQL operations - queries, mutations and subscriptions <b>Y</b>
    ? Enter maximum statement depth [increase from default if your schema is deeply nested] <b>2</b>
    </pre>

1. Now wait for the push to succeed. This should take around 4-5 minutes.
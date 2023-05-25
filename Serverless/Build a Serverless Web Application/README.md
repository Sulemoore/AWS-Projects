# Build a Serverless Web Application
## with AWS Lambda, Amazon API Gateway, AWS Amplify, Amazon DynamoDB, and Amazon Cognito


## Introduction:
This is a project that guides you on step-by-step instructions to create a simple serverless web application that enables users to equest unicorn rides from the Wild Rydes fleet.

## Overview:
In this beginner friendly tutorial, you will create a simple serverless web application that enables users to request unicorn rides from the Wild Rydes fleet. The application will present users with an HTML-based user interface for indicating the location where they would like to be picked up and will interact with a RESTful web service on the backend to submit the request and dispatch a nearby unicorn. The application will also provide facilities for users to register with the service and log in before requesting rides.

## Prerequisites:
1. AWS account
2. An account with ArcGIS to add mapping to your app, a text editor, and a web browser
3. Text editor

## Application architecture:
![Serverless_Architecture](https://github.com/Sulemoore/AWS-Projects/assets/101164153/0272f6fb-f234-4457-ba59-19ed26d3b5e4)

## Tech Stack:
The application architecture uses;
1. AWS Lambda
2. Amazon API Gateway
3. Amazon DynamoDB
4. Amazon Cognito
5. AWS Amplify Console

- Amplify Console provides continuous deployment and hosting of the static web resources including HTML, CSS, JavaScript, and image files which are loaded in the user's browser. JavaScript executed in the browser sends and receives data from a public backend API built using Lambda and API Gateway. Amazon Cognito provides user management and authentication functions to secure the backend API. Finally, DynamoDB provides a persistence layer where data can be stored by the API's Lambda function.

## Cost to complete:
Each service used in this architecture is eligible for the AWS Free Tier. If you are outside the usage limits of the Free Tier, completing this tutorial will cost you less than $0.25*.

## Time to complete:
2 hours broken down as follows;

This tutorial is divided into five modules. Each module describes a scenario of what we're going to build and step-by-step directions to help you implement the architecture and verify your work. 

1. Host a Static Website (15 minutes): Configure AWS Amplify to host the static resources for your web application with continuous deployment built in
2. Manage Users (30 minutes): Create an Amazon Cognito user pool to manage your users' accounts
3. Build a Serverless Backend (30 minutes): Build a backend process for handling requests for your web application
4. Deploy a RESTful API (15 minutes): Use Amazon API Gateway to expose the Lambda function you built in the previous module as a RESTful API
5. Terminate Resources (10 minutes): Terminate all the resources you created throughout this tutorial


# Module 1: Static Web Hosting with Continuous Deployment

![Serverless_Web_App_LP_assets-03 1403870f0fabeb6a11d3e4116092aa6b19b6a924](https://github.com/Sulemoore/AWS-Projects/assets/101164153/17b3920d-cd8e-4e64-8edc-df7282bed56e)


In this module, you will configure AWS Amplify to host the static resources for your web application with continuous deployment built in. The Amplify Console provides a git-based workflow for continuous deployment and hosting of full-stack web apps.
The architecture for this module is straightforward. All of your static web content including HTML, CSS, JavaScript, images, and other files will be managed by AWS Amplify Console. Your end users will then access your site using the public website URL exposed by AWS Amplify Console. You don't need to run any web servers or use other services to make your site available.

## Step 1: Select Region
1. This web application can be deployed in any AWS Region that supports all the services used in this application, which include AWS Amplify, AWS CodeCommit, Amazon Cognito, AWS Lambda, Amazon API Gateway, and Amazon DynamoDB.

![Screenshot 2023-05-24 at 9 13 11 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/38b4236e-e6f0-4c53-bac1-0b8daca55f93)


## Step 2: Create a Git repository
You have two options to manage the source code for this module: AWS CodeCommit (included in the AWS Free Tier) or GitHub. In this tutorial, we will use CodeCommit to store our application code, but you can do the same by creating a repository on GitHub.

a. Open the AWS CodeCommit console
![Screenshot 2023-05-24 at 9 18 28 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/18480823-d760-4f0e-9396-152ba7056490)

b. Select Create Repository
c. Set the Repository name to "wildrydes-site"
d. Select Create
![Screenshot 2023-05-24 at 9 18 49 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/8420e669-c01a-405f-8532-3f0de3ef81c5)

d. Select Create
e. Now that the repository is created, set up an IAM user with Git credentials in the IAM console following these instructions.
![Screenshot 2023-05-24 at 9 19 13 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/bd4a9efd-3798-47b2-a103-c3301735b97a)

f. Back in the CodeCommit console, from the Clone URL dropdown, select Clone HTTPS
g. From a terminal window run git clone and the HTTPS URL of the repository:
<img width="571" alt="Screenshot 2023-05-24 at 9 27 18 PM" src="https://github.com/Sulemoore/AWS-Projects/assets/101164153/263cce5d-2578-406f-af79-622503bb8730">


Note: You may need to generate HTTPS Git credentials if you have not done so.
![Screenshot 2023-05-24 at 9 27 38 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/17c01248-aabe-46fe-a342-387d8b6766d7)
<img width="843" alt="Screenshot 2023-05-24 at 9 35 22 PM" src="https://github.com/Sulemoore/AWS-Projects/assets/101164153/d19cf876-168c-4429-a5a8-9c7953bdaeed">


$ git clone https://git-codecommit.us-east1.amazonaws.com/v1/repos/wildrydes-site
Cloning into 'wildrydes-site'...
Username for 'https://git-codecommit.us-east-1.amazonaws.com':XXXXXXXXXX
Password for 'USERID': XXXXXXXXXXXX
warning: You appear to have cloned an empty repository.

## Step 3: Populate the Git Repository
Once you've used either AWS CodeCommit or GitHub.com to create your git repository and clone it locally, you'll need to copy the website content from an existing publicly accessible S3 bucket associated with this workshop and add the content to your repository.

a. Change directory into your repository and copy the static files from S3:

```

cd wildrydes-site
aws s3 cp s3://wildrydes-us-east-1/WebApplication/1_StaticWebHosting/website ./ --recursive

```
b. Commit the files to your Git service

```
$ git add .
$ git commit -m 'new'
$ git push

```

Counting objects: 95, done.
Compressing objects: 100% (94/94), done.
Writing objects: 100% (95/95), 9.44 MiB | 14.87 MiB/s, done.
Total 95 (delta 2), reused 0 (delta 0)
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/wildrydes-site
* [new branch] master -> master

## Step 4: Enable Web Hosting with the AWS Amplify console

a. Launch the Amplify Console console page
![Screenshot 2023-05-24 at 9 49 29 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/0dbf60a2-4f76-4151-961c-d15f818b768f)
![Screenshot 2023-05-24 at 9 49 46 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/f99937cc-d042-4fb4-91c6-9aa79ad22678)
![Screenshot 2023-05-24 at 9 50 21 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/11855e58-6672-4b8c-a132-18898db9ec86)

b. Click Get Started under Deploy with Amplify Console
c. Go to New App on the top right and choose Host Web App
d. Select CodeCommit under Get started with Amplify Hosting
![Screenshot 2023-05-24 at 9 50 48 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/897a032d-9446-4176-92a0-d24d780c8197)

e. Select the Repository service provider used today and select Continue
f. If you used GitHub, you'll need to authorize AWS Amplify to your GitHub account
g. From the dropdown, select the Repository and Branch you just created and select Next
![Screenshot 2023-05-24 at 9 52 18 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/312fbde3-6f1c-4a75-a675-b688f68f83f9)

h. On the Configure build settings page, leave all the defaults, Select Allow AWS Amplify to automatically deploy all files hosted in your project root directory and select Next.
![Screenshot 2023-05-24 at 9 53 45 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/b1472a45-cac5-4641-88bf-c1887381b20e)

i. On the "Review" page select Save and deploy
![Screenshot 2023-05-24 at 9 54 22 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/248448d4-1fbe-4b4e-9a1b-8fd0d04e2b7b)

j. The process takes a couple of minutes for Amplify Console to create the necessary resources and to deploy your code.
![Screenshot 2023-05-24 at 9 54 55 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/553b703d-0879-45bb-8e54-1793562288df)


-Once completed, click on the site image to launch your Wild Rydes site.
![Screenshot 2023-05-24 at 9 57 11 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/6ef9e521-9dfe-4868-a99b-227f97d91683)

-If you click on the link for Master you'll see the build and deployment details related to your branch, and screenshots of the app on various devices:

## Step 5: Modify Your Site
The AWS Amplify Console will rebuild and redeploy the app when it detects changes to the connected repository. Make a change to the main page to test out this process.

a. From your local machine, open `wildryde-site/index.html` in a text editor of your choice and modify the title line so that it says: <title>Wild Rydes - Rydes of the Future!</title>

b. Save the file and commit to your git repository again. Amplify Console will begin to build the site again soon after it notices the update to the repository. It will happen pretty quickly! Head back to the Amplify Console page to watch the process.

```
$ git add index.html 
$ git commit -m "updated title"
[master dfec2e5] updated title
 1 file changed, 1 insertion(+), 1 deletion(-)

$ git push
Counting objects: 3, done.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 315 bytes | 315.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: processing 
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/wildrydes-site
   2e9f540..dfec2e5  master -> master

```
## Recap: Module 1. 
In this module, you've created static website which will be the base for our Wild Rydes business. AWS Amplify Console makes it really easy to deploy static websites following a continuous integration and delivery model. It has capabilities for "building" more complicated Javascript framework based applications and has features such as feature branch deployments, easy custom domain setup, instant deployments, and password protection.


## Module 2: User Management (create an Amazon Cognito user pool to manage your users' accounts)

In this module you'll create an Amazon Cognito user pool to manage your users' accounts. You'll deploy pages that enable customers to register as a new user, verify their email address, and sign into the site.
![Screenshot 2023-05-24 at 10 15 09 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/d369a63b-590f-4ee0-8cd5-6c069e0e5758)


When users visit your website they will first register a new user account. For the purposes of this workshop we'll only require them to provide an email address and password to register. However, you can configure Amazon Cognito to require additional attributes in your own applications.

After users submit their registration, Amazon Cognito will send a confirmation email with a verification code to the address they provided. To confirm their account, users will return to your site and enter their email address and the verification code they received. You can also confirm user accounts using the Amazon Cognito console with a fake email addresses for testing.

After users have a confirmed account (either using the email verification process or a manual confirmation through the console), they will be able to sign in. When users sign in, they enter their username (or email) and password. A JavaScript function then communicates with Amazon Cognito, authenticates using the Secure Remote Password protocol (SRP), and receives back a set of JSON Web Tokens (JWT). The JWTs contain claims about the identity of the user and will be used in the next module to authenticate against the RESTful API you build with Amazon API Gateway.

## Step 1: Create an Amazon Cognito User Pool and Integrate an App to your User Pool

Amazon Cognito provides two different mechanisms for authenticating users. You can use Cognito User Pools to add sign-up and sign-in functionality to your application or use Cognito Identity Pools to authenticate users through social identity providers such as Facebook, Twitter, or Amazon, with SAML identity solutions, or by using your own identity system. For this module you'll use a user pool as the backend for the provided registration and sign-in pages.
a. In the AWS Console, enter Cognito in the search bar and select Cognito from the search results. 
b. Choose Create user pool.
c. On the Configure sign-in experience page, in the Cognito user pool sign-in options section, select User name. Keep the defaults for the other settings, such as Provider types in the Authentication providers section. Choose Next.
![Screenshot 2023-05-24 at 10 16 13 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/2c1151ca-7d6e-45cb-bae9-1a1603bdb362)

d. On the Configure security requirements page, keep the Password policy mode as Cognito defaults. You can choose to configure multi-factor authentication (MFA) or choose No MFA and keep other configurations as default. Choose Next.
![Screenshot 2023-05-24 at 10 18 31 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/25f30fb3-2805-44dc-9f54-5d1e3e9f253b)

e. On the Configure sign-up experience page, keep everything as default. Choose Next.
![Screenshot 2023-05-24 at 10 19 49 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/ad089f61-c9db-4a46-9978-bc124f9a926f)

f. On the Configure message delivery page, for Email provider, confirm that Send email with Amazon SES - Recommended is selected. In the FROM email address field, select an email address that you have verified with Amazon SES, following these instructions from the Amazon SES Developer Guide.
![Screenshot 2023-05-24 at 10 24 20 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/82854bc8-7a5f-49c8-9c99-1057f9545385)
![Screenshot 2023-05-24 at 10 28 54 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/67cef528-f464-4199-8faf-1953662642ac)

g. On the Integrate your app page, provide a name for your user pool such as WildRydes. Under Initial app client, give the app client a name such as WildRydesWebApp and keep other settings as default.
h. On the Review and create page, choose Create user pool.
![Screenshot 2023-05-24 at 10 30 28 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/37bcd7fc-a7d3-4b7d-bf8e-784ea1676430)

i. Note the Pool ID and the App client ID on the Pool details page of your newly created user pool.

## Step 2: Update the Website Config

The /js/config.js file contains settings for the user pool ID, app client ID and Region. Update this file with the settings from the user pool and app you created in the previous steps and upload the file back to your bucket

a. From your local machine, open `wildryde-site/js/config.js` in a text editor of your choice.
![Screenshot 2023-05-24 at 10 44 43 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/2b583e8a-4ac7-4ee8-b5ff-e7c9f4f4d90b)

a. From your local machine, open `wildryde-site/js/config.js` in a text editor of your choice.

b. Update the cognito section with the correct values for the user pool and app you just created.

You can find the value for userPoolId on the Pool details page of the Amazon Cognito console after you select the user pool that you created.

You can find the value for userPoolClientId by selecting App clients from the left navigation bar. Use the value from the App client id field for the app you created in the previous section.

The value for region should be the AWS Region code where you created your user pool. E.g. us-east-1 for the N. Virginia Region, or us-west-2 for the Oregon Region. If you're not sure which code to use, you can look at the Pool ARN value on the Pool details page. The Region code is the part of the ARN immediately after arn:aws:cognito-idp:.
The updated config.js file should look like this. Note that the actual values for your file will be different:

```
window._config = {
    cognito: {
        userPoolId: 'us-west-2_uXboG5pAb', // e.g. us-east-2_uXboG5pAb
        userPoolClientId: '25ddkmj4v6hfsfvruhpfi7n4hv', // e.g. 25ddkmj4v6hfsfvruhpfi7n4hv
        region: 'us-west-2' // e.g. us-east-2
    },
    api: {
        invokeUrl: '' // e.g. https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod',
    }
};

```
d. Save the modified file and push it to your Git repository to have it automatically deploy to Amplify Console.

```
$ git add .
$ git commit -m "new_config"
$ git push

```

## Step 3: Validate your implementation

a. Visit /register.html under your website domain, or choose the Giddy Up! button on the homepage of your site.

b. Complete the registration form and choose Let's Ryde. You can use your own email or enter a fake email. Make sure to choose a password that contains at least one upper-case letter, a number, and a special character. Don't forget the password you entered for later. You should see an alert that confirms that your user has been created.

c. Confirm your new user using one of the two following methods.

d. If you used an email address you control, you can complete the account verification process by visiting /verify.html under your website domain and entering the verification code that is emailed to you. Please note, the verification email may end up in your spam folder. For real deployments we recommend configuring your user pool to use Amazon Simple Email Service to send emails from a domain you own.

e. If you used a dummy email address, you must confirm the user manually through the Cognito console.

f. From the AWS console, click Services then select Cognito under Security, Identity & Compliance.

g. Choose Manage your User Pools

h. Select the WildRydes user pool and click Users and groups in the left navigation bar.

i. You should see a user corresponding to the email address that you submitted through the registration page. Choose that username to view the user detail page.

j. Choose Confirm user to finalize the account creation process.

k. After confirming the new user using either the /verify.html page or the Cognito console, visit /signin.html and log in using the email address and password you entered during the registration step.
![Screenshot 2023-05-24 at 10 30 28 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/ea77d1cb-8152-44ee-9e50-c23d2e2ce91a)


l. If successful you should be redirected to /ride.html. You should see a notification that the API is not configured.


## Module 3: Serverless Service Backend (use AWS Lambda and Amazon DynamoDB to build a backend process for handling requests for your web application)

![Serverless_Web_App_LP_assets_04 76030d61413ff43bd6aa75fbd16e02ad23aec67a](https://github.com/Sulemoore/AWS-Projects/assets/101164153/3177d9f9-9305-4724-926c-5a71e896c1a2)


In this module, you will use AWS Lambda and Amazon DynamoDB to build a backend process for handling requests for your web application. The browser application that you deployed in the first module allows users to request that a unicorn be sent to a location of their choice. To fulfill those requests, the JavaScript running in the browser will need to invoke a service running in the cloud.

You will implement a Lambda function that will be invoked each time a user requests a unicorn. The function will select a unicorn from the fleet, record the request in a DynamoDB table, and then respond to the frontend application with details about the unicorn being dispatched.

The function is invoked from the browser using Amazon API Gateway. You'll implement that connection in the next module. For this module, you will just test your function in isolation.

## Step 1: Create an Amazon DynamoDB Table

Use the Amazon DynamoDB console to create a new DynamoDB table. Call your table Rides and give it a partition key called RideId with type String. The table name and partition key are case sensitive. Make sure you use the exact IDs provided. Use the defaults for all other settings.

After you've created the table, note the ARN for use in the next step.

a. From the AWS Management Console, choose Services then select DynamoDB under Databases.
b. Choose Create table.
![Screenshot 2023-05-24 at 11 03 56 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/946e7857-68b3-4f3e-8df5-1438cbc0129c)

 ![Screenshot 2023-05-24 at 11 04 36 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/3b30b7fb-15ce-4667-96dd-59300a465f6f)

c. Enter Rides for the Table name. This field is case sensitive.
d. Enter RideId for the Partition key and select String for the key type. This field is case sensitive.
e. Check the Use default settings box and choose Create. Navigate to the Tables page in the DynamoDB console and wait for your table creation to complete. Once it is completed, select your table name.
f. Scroll to the bottom of the Overview section of your new table and choose Additional info. Note the ARN. You will use this in the next section.
![Screenshot 2023-05-24 at 11 06 53 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/57f8547a-d413-4687-8011-860c98895779)


## Step 2: Create an IAM role for your Lambda function

Every Lambda function has an IAM role associated with it. This role defines what other AWS services the function is allowed to interact with. For the purposes of this workshop, you'll need to create an IAM role that grants your Lambda function permission to write logs to Amazon CloudWatch Logs and access to write items to your DynamoDB table.

Use the IAM console to create a new role. Name it WildRydesLambda and select AWS Lambda for the role type. You'll need to attach policies that grant your function permissions to write to Amazon CloudWatch Logs and put items to your DynamoDB table.

Attach the managed policy called AWSLambdaBasicExecutionRole to this role to grant the necessary CloudWatch Logs permissions. Also, create a custom inline policy for your role that allows the ddb:PutItem action for the table you created in the previous section.
a. From the AWS Management Console, click on Services and then select IAM in the Security, Identity & Compliance section.

b. Select Roles in the left navigation pane and then choose Create Role.
![Screenshot 2023-05-24 at 11 09 32 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/bbd02bd6-1840-48f7-9f0c-73516dc3307d)


c. Underneath Trusted Entity Type, select AWS service. For Use case, select Lambda, then choose Next.
![Screenshot 2023-05-24 at 11 09 57 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/b560ab51-06d5-4f81-aa3a-82e0fd8779a6)


Note: Selecting a role type automatically creates a trust policy for your role that allows AWS services to assume this role on your behalf. If you were creating this role using the CLI, AWS CloudFormation or another mechanism, you would specify a trust policy directly.

d. Begin typing AWSLambdaBasicExecutionRole in the Filter text box and check the box next to that role.

e. Choose Next Step.
![Screenshot 2023-05-24 at 11 11 51 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/2237ca07-10ae-4291-9c1f-464a54289f57)


f. Enter WildRydesLambda for the Role Name. Keep other parameters as default.

g. Choose Create Role.
![Screenshot 2023-05-24 at 11 12 20 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/560507cf-7868-4895-8521-846075771b82)


h. Type WildRydesLambda into the filter box on the Roles page and choose the role you just created.

i. On the Permissions tab, on the left under Add permissions, choose Create Inline Policy.
![Screenshot 2023-05-24 at 11 15 09 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/bae90a3b-3b75-4bfa-be2b-3cb92df880fc)


j. Select Choose a service.
![Screenshot 2023-05-24 at 11 15 47 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/c00d9ff2-dd7d-4cad-9cda-cdcba935f4d9)


k. Begin typing DynamoDB into the search box labeled Find a service and select DynamoDB when it appears..

l. Choose Select actions.

m. Begin typing PutItem into the search box labeled Filter actions and check the box next to PutItem when it appears.
![Screenshot 2023-05-24 at 11 16 43 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/40fdb48e-c5f7-46f8-81e8-0b4304b99fc5)


n. Select the Resources section.

o. With the Specific option selected, choose the Add ARN link in the table section.

p. Paste the ARN of the table you created in the previous section in the Specify ARN for table field, and choose Add.

q. Choose Review Policy.
![Screenshot 2023-05-24 at 11 19 21 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/92bbdfe5-5f89-4298-9356-56b076fde913)


r. Enter DynamoDBWriteAccess for the policy name and choose Create policy.

## Step 3: Create a Lambda Function for Handling requests

AWS Lambda will run your code in response to events such as an HTTP request. In this step you'll build the core function that will process API requests from the web application to dispatch a unicorn. In the next module you'll use Amazon API Gateway to create a RESTful API that will expose an HTTP endpoint that can be invoked from your users' browsers. You'll then connect the Lambda function you create in this step to that API in order to create a fully functional backend for your web application.
![Screenshot 2023-05-24 at 11 21 43 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/cff70038-33be-4730-b3a2-8f6d73c2e50a)

Use the AWS Lambda console to create a new Lambda function called RequestUnicorn that will process the API requests. Use the provided requestUnicorn.js example implementation for your function code. Just copy and paste from that file into the AWS Lambda console's editor.

Make sure to configure your function to use the WildRydesLambda IAM role you created in the previous section.
a. Choose Services then select Lambda in the Compute section.

b. Click Create function.

c. Keep the default Author from scratch card selected.

d. Enter RequestUnicorn in the Name field.

e. Select Node.js 16.x for the Runtime (newer versions of Node.js will not work in this tutorial)

f. Ensure Use an existing role is selected from the Change default execution role dropdown.

g. Select WildRydesLambda from the Existing Role dropdown.

h. Click on Create function.
![Screenshot 2023-05-24 at 11 25 26 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/e5a4fbd6-7319-4f09-a95b-b965a6901f53)

i. Scroll down to the Code source section and replace the existing code in the index.js code editor with the contents of requestUnicorn.js.

j. Choose Deploy.

## Step 4: Validate Your Implementation

For this module you will test the function that you built using the AWS Lambda console. In the next module you will add a REST API with API Gateway so you can invoke your function from the browser-based application that you deployed in the first module.

a. From the main edit screen for your function, select Test and choose Configure test event from the dropdown.
b. Keep Create new event selected.
c. Enter TestRequestEvent in the Event name field
![Screenshot 2023-05-24 at 11 29 04 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/8cb1393f-e557-4b37-9b46-f5975ca9a995)

d. Copy and paste the following test event into the editor:

```
{
    "path": "/ride",
    "httpMethod": "POST",
    "headers": {
        "Accept": "*/*",
        "Authorization": "eyJraWQiOiJLTzRVMWZs",
        "content-type": "application/json; charset=UTF-8"
    },
    "queryStringParameters": null,
    "pathParameters": null,
    "requestContext": {
        "authorizer": {
            "claims": {
                "cognito:username": "the_username"
            }
        }
    },
    "body": "{\"PickupLocation\":{\"Latitude\":47.6174755835663,\"Longitude\":-122.28837066650185}}"
}

```

e. Choose Save.
f. On the main function edit screen click Test with TestRequestEvent selected in the dropdown.
g. Scroll to the top of the page and expand the Details section of the Execution result section.
h. Verify that the execution succeeded and that the function result looks like the following:
![Screenshot 2023-05-24 at 11 33 36 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/60ae17b9-ffb6-4536-a26d-9d2fc964dbfa)


```
{
    "statusCode": 201,
    "body": "{\"RideId\":\"SvLnijIAtg6inAFUBRT+Fg==\",\"Unicorn\":{\"Name\":\"Rocinante\",\"Color\":\"Yellow\",\"Gender\":\"Female\"},\"Eta\":\"30 seconds\"}",
    "headers": {
        "Access-Control-Allow-Origin": "*"
    }
}

```

## Module 4: (use Amazon API Gateway to expose the Lambda function you built in the previous module as a RESTful API)

![Serverless_Web_App_LP_assets_05 d1ecdfaab160d7dc00ddbc9e0245fa34b8d8f26b](https://github.com/Sulemoore/AWS-Projects/assets/101164153/8c02efd1-8d9c-4d47-92d2-a244b7e4eec1)


In this module, you will use Amazon API Gateway to expose the Lambda function you built in the previous module as a RESTful API. This API will be accessible on the public Internet. It will be secured using the Amazon Cognito user pool you created in the previous module. Using this configuration, you will then turn your statically hosted website into a dynamic web application by adding client-side JavaScript that makes AJAX calls to the exposed APIs.

The diagram above shows how the API Gateway component you will build in this module integrates with the existing components you built previously. The grayed out items are pieces you have already implemented in previous steps.

The static website you deployed in the first module already has a page configured to interact with the API you will build in this module. The page at /ride.html has a simple map-based interface for requesting a unicorn ride. After authenticating using the /signin.html page, your users will be able to select their pickup location by clicking a point on the map and then requesting a ride by choosing the "Request Unicorn" button in the upper right corner.

This module will focus on the steps required to build the cloud components of the API, but if you're interested in how the browser code works that calls this API, you can inspect the ride.js file of the website. In this case, the application uses jQuery's ajax() method to make the remote request.

## Step 1: Create a New REST API

a. In the AWS Management Console, click Services then select API Gateway under Application Services.
![Screenshot 2023-05-24 at 11 33 36 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/b69f3894-48a0-40d1-a598-f311f996be86)

a. In the AWS Management Console, click Services then select API Gateway under Application Services.
b. Choose Create API. Underneath the Create new API section, make sure New API is selected.
c. Select Build under REST API and enter WildRydes for the API Name.
![Screenshot 2023-05-24 at 11 37 35 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/35ed423b-c229-49cf-8a48-5416efe55b53)

d. Choose Edge optimized in the Endpoint Type dropdown. 
![Screenshot 2023-05-24 at 11 37 35 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/929a9f8f-462d-46ed-b670-a8aa13e80dc7)

Note: Edge optimized are best for public services being accessed from the Internet. Regional endpoints are typically used for APIs that are accessed primarily from within the same AWS Region.
e. Choose Create API

#Step 2: Create a new resource and method

Create a new resource called /ride within your API. Then create a POST method for that resource and configure it to use a Lambda proxy integration backed by the RequestUnicorn function you created in the first step of this module.

a. In the left nav, click on Resources under your WildRydes API.

b. From the Actions dropdown select Create Resource.

c. Enter ride as the Resource Name.

d. Ensure the Resource Path is set to ride.

e. Select Enable API Gateway CORS for the resource.

f. Click Create Resource.
![Screenshot 2023-05-24 at 11 37 35 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/17b8b987-8bd4-4d56-a50e-f2201cde27a3)


g. With the newly created /ride resource selected, from the Action dropdown select Create Method.

h. Select POST from the new dropdown that appears, then click the checkmark.
![Screenshot 2023-05-24 at 11 39 34 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/d19aed19-b431-47ba-b6f1-ed2d2bb07790)


i. Select Lambda Function for the integration type.

j. Check the box for Use Lambda Proxy integration.

k. Select the Region you are using for Lambda Region.

l. Enter the name of the function you created in the previous module, RequestUnicorn, for Lambda Function.

m. Choose Save. Please note, if you get an error that your function does not exist, check that the region you selected matches the one you used in the previous module.

n. When prompted to give Amazon API Gateway permission to invoke your function, choose OK.
![Screenshot 2023-05-24 at 11 41 47 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/0e22e536-f2ef-41d4-a28e-e13e43dab299)


o. Choose on the Method Request card.

p. Choose the pencil icon next to Authorization.
![Screenshot 2023-05-24 at 11 41 47 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/d8ba60d9-ddcc-4817-bf79-7ab7f19def14)


q. Select the WildRydes Cognito user pool authorizer from the drop-down list, and click the checkmark icon.

## Step 3: Deploy your API

From the Amazon API Gateway console, choose Actions, Deploy API. You'll be prompted to create a new stage. You can use prod for the stage name.

a. In the Actions drop-down list select Deploy API.
![Screenshot 2023-05-24 at 11 43 34 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/7847d05f-11c6-4907-9d78-4401d92760c3)

b. Select [New Stage] in the Deployment stage drop-down list.
c. Enter prod for the Stage Name.
d. Choose Deploy.
e. Note the Invoke URL. You will use it in the next section.
![Screenshot 2023-05-24 at 11 44 32 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/3c4474fa-c73f-4302-8f4f-18fb21b0cfbb)

e. Note the Invoke URL. You will use it in the next section.

## Step 4: Update the Website Config

Update the /js/config.js file in your website deployment to include the invoke URL of the stage you just created. You should copy the invoke URL directly from the top of the stage editor page on the Amazon API Gateway console and paste it into the _config.api.invokeUrl key of your sites /js/config.js file. Make sure when you update the config file it still contains the updates you made in the previous module for your Cognito user pool.

a. Open the config.js file in a text editor.
b. Update the invokeUrl setting under the api key in the config.js file. Set the value to the Invoke URL for the deployment stage your created in the previous section.

An example of a complete config.js file is included below. Note, the actual values in your file will be different.

```
window._config = {

    cognito: {

        userPoolId: 'us-west-2_uXboG5pAb', // e.g. us-east-2_uXboG5pAb         

        userPoolClientId: '25ddkmj4v6hfsfvruhpfi7n4hv', // e.g. 25ddkmj4v6hfsfvruhpfi7n4hv

        region: 'us-west-2' // e.g. us-east-2 

    }, 

    api: { 

        invokeUrl: 'https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod' // e.g. https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod, 

    } 

};
```

Save the modified file and push it to your Git repository to have it automatically deploy to Amplify Console.

```
$ git add .
$ git commit -m "new_configuration"
$ git push

```

## Step 5: Validate your implementation

Note: It is possible that you will see a delay between updating the config.js file in your S3 bucket and when the updated content is visible in your browser. You should also ensure that you clear your browser cache before executing the following steps.

a. Update the ArcGIS JS version from 4.3 to 4.6 (newer versions will not work in this tutorial) in the ride.html file as:

```
<div id="noApiMessage" class="configMessage" style="display: none;">
        <div class="backdrop"></div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <h3 class="panel-title">Successfully Authenticated!</h3>
            </div>
            <div class="panel-body">
                <p>This page is not functional yet because there is no API invoke URL configured in <a href="/js/config.js">/js/config.js</a>. You'll configure this in Module 3.</p>
                <p>In the meantime, if you'd like to test the Amazon Cognito user pool authorizer for your API, use the auth token below:</p>
                <textarea class="authToken"></textarea>
            </div>
        </div>
    </div>

    <div id="noCognitoMessage" class="configMessage" style="display: none;">
        <div class="backdrop"></div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <h3 class="panel-title">No Cognito User Pool Configured</h3>
            </div>
            <div class="panel-body">
                <p>There is no user pool configured in <a href="/js/config.js">/js/config.js</a>. You'll configure this in Module 2 of the workshop.</p>
            </div>
        </div>
    </div>

    <div id="main">
        <div id="map">
        </div>
    </div>

    <div id="authTokenModal" class="modal fade" tabindex="-1" role="dialog" aria-labelledby="authToken">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
                    <h4 class="modal-title" id="myModalLabel">Your Auth Token</h4>
                </div>
                <div class="modal-body">
                    <textarea class="authToken"></textarea>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                </div>
            </div>
        </div>
    </div>


    <script src="js/vendor/jquery-3.1.0.js"></script>
    <script src="js/vendor/bootstrap.min.js"></script>
    <script src="js/vendor/aws-cognito-sdk.min.js"></script>
    <script src="js/vendor/amazon-cognito-identity.min.js"></script>
    <script src="https://js.arcgis.com/4.6/"></script>
    <script src="js/config.js"></script>
    <script src="js/cognito-auth.js"></script>
    <script src="js/esri-map.js"></script>
    <script src="js/ride.js"></script>
</body>

</html>
```

b. Save the modified file and push it to your Git repository to have it automatically deploy to Amplify Console.

c. Visit /ride.html under your website domain.
d. If you are redirected to the ArcGIS sign-in page, sign in with the user credentials you created previously in the Introduction section as a prerequisite of this tutorial.
e. After the map has loaded, click anywhere on the map to set a pickup location.
f. Choose Request Unicorn. You should see a notification in the right sidebar that a unicorn is on its way and then see a unicorn icon fly to your pickup location.


## Module 5: Cleanup

1. Delete your Amplify app.

a. In the AWS Management Console choose Services then select AWS Amplify under Mobile.

b. Select the app you created in module 1.
![Screenshot 2023-05-25 at 12 04 16 AM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/afa5d44f-81f0-452c-9c92-1325f49319df)


c. On the app landing page, choose ‘Actions > Delete app’. Enter ‘delete’ when prompted to confirm, then choose confirm.

2. Delete Amazon Cognito user pool

a. From the AWS Console click Services then select Cognito under Mobile Services.

b. Choose Manage your User Pools.

c. Select the WildRydes user pool you created in module 2.

d. Choose Delete Pool in the upper right corner of the page.
![Screenshot 2023-05-25 at 12 06 01 AM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/4bfb6db5-3c03-4859-9430-62320ab2d393)


e. Type delete and choose Delete Pool when prompted to confirm.

3. Delete serverless backend

Delete the AWS Lambda function, IAM role and Amazon DynamoDB table you created in module 3.

Lambda Function

a. In the AWS Management Console, click Services then select Lambda under Compute.

b. Select the RequestUnicorn function you created in module 3.

c. From the Actions drop-down, choose Delete function.
![Screenshot 2023-05-25 at 12 08 22 AM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/633f9eb8-e8d4-4fff-a461-051a4d0b2818)


d. Enter delete and choose Delete pool when prompted to confirm.


IAM Role

a. In the AWS Management Console, click Services then select IAM under Security, Identity & Compliance.

b. Select Roles from the left navigation pane.

c. Enter WildRydesLambda into the filter box.

d. Select the role you created in Module 3.
![Screenshot 2023-05-25 at 12 09 23 AM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/b79f780a-83be-4610-b218-3cd78a07befd)


e. Select the Role and choose Delete. Confirm the role name that needs to be deleted by entering WildRydesLambda. Choose Delete role. 
f. Choose Yes, Delete when prompted to confirm.


DynamoDB Table

a. In the AWS Management Console, click Services then select DynamoDB under Databases

b. Choose Tables in the navigation menu.

c. Choose the Rides table you created in module 3.

d. Choose Delete at the top right.
![Screenshot 2023-05-25 at 12 10 05 AM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/ec7a28a3-854c-4ae4-8402-a9d633d24ad1)


e. Leave the checkbox to Delete all CloudWatch alarms for this table selected, enter delete, and choose Delete.

4. Delete your REST API

Delete the REST API created in module 4. There is a Delete API option in the Actions drop-down when you select your API in the Amazon API Gateway Console.

a. In the AWS Management Console, click Services then select API Gateway under Application Services.
b. Select the API you created in module 4.
c. Expand the Actions drop-down and choose Delete API.
![Screenshot 2023-05-25 at 12 11 44 AM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/886db672-2ead-4179-a35f-fd5eed9ff7cc)

d. Enter the name of your API when prompted and choose Delete API.

5. Delete your Cloudwatch Logs

AWS Lambda automatically creates a new log group per function in Amazon CloudWatch Logs and writes logs to it when your function is invoked. You should delete the log group for the RequestUnicorn function. 

a. From the AWS Console click Services then select CloudWatch under Management Tools.
b. Choose Logs in the navigation menu.
c. Select the /aws/lambda/RequestUnicorn log group. If you have many log groups in your account, you can type /aws/lambda/RequestUnicorn into the Filter text box to easily locate the log group.
d. Choose Delete log group from the Actions drop-down.
e. Choose Yes, Delete when prompted to confirm.
![Screenshot 2023-05-25 at 12 15 03 AM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/7c2e1847-7466-4362-89b0-323962a6d8f9)

f. If you launched any CloudFormation templates to complete a module, repeat steps 3-5 for any log groups which begin with /aws/lambda/wildrydes-webapp.

# Congratulations! You built and terminated a serverless web application using AWS.

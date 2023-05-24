# How to Set Up an Email-Receiving Pipeline Cost-Effectively
/Users/mosuleiman/Desktop/AWS Hands-on Projects/Compute/Image.png



## Task:

In this project, you will set up an email-receiving pipeline for your domain using Amazon Simple Email Service (Amazon SES), a cost-effective email service built on the reliable and scalable infrastructure. Amazon SES handles the underlying mail-receiving operations involved in communicating with other mail servers, scanning for spam and viruses, rejecting mail from untrusted sources, and accepting mail for recipients in your domain. Amazon SES then passes your emails to an endpoint where your applications can access the emails for archiving, decoding and displaying to end users, triggering autoresponders, generating support tickets, or any number of ways your applications might use email. Using Amazon SES enables you to leverage AWS products and services like Amazon S3, Amazon SNS, AWS Lambda, and Amazon WorkMail to create scalable email solutions for your organization.


## What you will accomplish:

1. Set up your domain to receive email using Amazon SES, and then confirm the email-receiving setup by sending a test email to an address in your domain.

2. Save the email in raw format to an Amazon S3 bucket. Amazon SES saves the email to the Amazon S3 bucket in raw format, so that you have the flexibility to process and display the email with your own application.


## Prerequisites:

1. An AWS account: You need an AWS account to use AWS services.

2. A domain registered with Amazon Route 53

3. Knowledge about domain name server (DNS) records is recommended, but not required, to complete this project.

4. AWS experience: Familiarity with hosting a domain on Amazon Route 53 and retrieving an item from an Amazon S3 bucket is recommended, but not required.


## Billing estimate:

The total cost of this project varies depending on the size of the email you receive and the type of domain you own. Let's assume that the test email you receive is less than 256 KB (a simple email with a few lines of text is well under this size), the email does not have an attachment, your domain is a ".com", and you delete the email from the Amazon S3 bucket within a month after you receive it. In this case, the cost incurred by doing this project will be $12.00 if you are inside the free tier limits, and $12.03 if you are outside the free tier limits.
The cost breakdown is: Amazon SES ($0 to receive the email), Amazon S3 ($0.03/month to store the email if you are outside the free tier limits, and $0 if you are within the free tier limits), and Amazon Route 53 ($12/year to register a ".com" domain). For more information about the pricing of the individual services, see Services Used and Costs.
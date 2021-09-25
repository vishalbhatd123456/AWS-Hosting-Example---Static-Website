# AWS-Hosting-Example---Static-Website

Creating a Static Website Using Amazon S3
Introduction
In this AWS hands-on lab, we will create and configure a simple static website. We will go through configuring that static website with a custom error page. This will demonstrate how to create a cost-efficient website hosting for sites that consist of files like HTML, CSS, JavaScript, fonts, and images.

Solution
Log in to the live AWS environment using the credentials provided. Make sure you're in the N. Virginia (us-east-1) region throughout the lab.

The code for the static site is here.

Create S3 Bucket
Navigate to S3.

Click Create bucket.

Set the following values:

Bucket name: scubasyndrome- with the AWS account number or another series of numbers at the end to make it globally unique
Region: US East (N. Virginia) us-east-1
In the Bucket settings for Block Public Access section, un-check Block all public access.

Ensure all four permissions restrictions beneath it are also un-checked.
Check the box to acknowledge that turning off all public access might result in the bucket and its objects becoming public.

Leave the rest of the settings as their defaults.

Click Create bucket.

Select the bucket name.

Click Upload.

Click Add files, and upload your own or the error.html and index.html files from the lab GitHub repo.

Leave the rest of the settings as their defaults.

Click Upload.

Click Exit in the upper right.

Enable Static Website Hosting
Click the Properties tab.

Scroll to the bottom of the screen to find the Static website hosting section.

On the right in the Static website hosting section, click Edit.

On the Edit static website hosting page, set the following values:

Static website hosting: Enable
Hosting type: Host a static website
Index document: index.html
Error document: error.html
Click Save changes.

Scroll back down to the Static website hosting section.

Open the listed endpoint URL in a new browser tab. We'll see a 403 Forbidden error message.

Apply Bucket Policy
Back in S3, click the Permissions tab.

In the Bucket policy section, click Edit.

In the Policy box, enter the following JSON statement (replacing <BUCKET_ARN> with the bucket ARN provided right above the Policy box):

{
  "Version":"2012-10-17",
  "Statement":[{
     "Sid":"PublicReadGetObject",
     "Effect":"Allow",
     "Principal": "*",
     "Action":["s3:GetObject"],
     "Resource":["<BUCKET_ARN>/*"]
  }]
}
Note: Ensure the trailing /* is present so the policy applies to all objects within the bucket.

Click Save changes.

Refresh the browser tab with the static website (the endpoint URL we opened a minute ago). This time, it should load the site correctly.

Add a / at the end of the URL and some random letters (anything that's knowingly an error). This will display our error.html info.

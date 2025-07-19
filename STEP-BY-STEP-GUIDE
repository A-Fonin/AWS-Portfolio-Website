#  Overview and Objectives

**Project Overview:**

Welcome to the capstone project on building a server-based resume (CV) and AWS Latest News website.    

You will find these in the **Prerequisite and Setup** section below.



## The Project Brief

The customer, a start-up known as exampleCorp, is in the process of migrating their AWSPortolio website into the cloud. They have been running this application as a monolithic app for the past ten years, on a single server with all of the code and the functionality bundled on a single server running in a server in the head office.

For many reasons, including performance issues, the cost of operating and managing the server, and technical debt - exampleCorp has decided to migrate this application to the cloud. Anytime they needed to make a change to the website, they would accrue many hours of downtime whilst they gained access to the web server and made their changes - and because of the application's monolithic nature, any changes were fraught with risk - could this change in one aspect of the application cause a problem in the rest of the application? This needed to change.

Their in-house software development team has taken the application code and separated it into the main website files (HTML, css, javascript for server-side functionality) and split out the microservices (AWS Latest news page, Blog Post addition service, View Counter and the Contact Form) into CloudFormation templates including services like Lambda, DynamoDB, and Amazon Eventbridge. They have also taken the application code and put it onto an Amazon Machine Image (AMI).

Your job as the migration lead is to bring up the application on AWS and integrate the EC2-based website with the microservices and APIs. Additionally, the company wants to ultimately reduce costs and migrate all application components to serverless services. 

Therefore, there are two stages to the project:

## Stage 1 - Migrate to a server-based highly available website

In stage 1 you must deploy the web application in a highly available server-based deployment.

**Key Objectives & Requirements:**

- Take the AMI and deploy the application on it, which is highly scalable, fault-tolerant, and well-architected - using services like Application Load Balancers, CloudFront, and Route 53 for DNS resolution. 

- Integrate the microservices into the web application using the code for these services without embedding them into the web servers themselves. 

- Securely do this - i.e., no public IP addresses on the EC2 instances, effective use of Security groups, using the principle of least privilege, etc. 

## Stage 2 - Migrate the website to serverless infrastructure

In stage 2 you must migrate the web application onto to an S3 static website.

**Key Objectives & Requirements:**

- Migrate the website assets to an S3 bucket configured as a static website.

- Update the CloudFront distribution ensuring that a custom domain name is maintained for the website.

- Update Amazon Route 53 records.


## Prerequisites and Setup

**Important:** Ensure you are in the "N. Virginia" AWS Region, "us-east-1".


#### Step 1 - Deploy the AMI

The first step is to take the public ami (ami-0aa954d8500984aee, you'll find it under community AMIs) and launch an instance from this AMI. If you SSH into your machine and go to the /var/www/html directory, you should see there are several website files waiting for you to interact with:

- index.html
- index.js
- blog.html
- blog.js
- aws.html 
- aws.js
- style.css

Feel free to look around at your initial webpage by going to the public IP of your instance.

This web server now has all of the server-side web application code for you to start building upon to add functionality to the webpage.

You then need to launch the 'Microservice' stacks, all of which include event-driven or serverless components, which will be used to increase the functionality of the website. Feel free to look into each stack to see the components and the Lambda code to try to understand what's going on in the stack. Once they are deployed, you will create various endpoints (API / Function URLS) and embed these into the application code on the EC2 instances. 

This will allow the end users to interact with the microservices in AWS by using the website. 


#### Step 2 - Deploy CloudFormation stacks

The next step is to install all the CloudFormation stacks (in any order), ensuring you are in the AWS Region us-east-1 region.  You can write any value you like for any parameters you are asked to include.


#### Step 3 - Creating microservice endpoints

> NOTES: The Google Chrome developer tools will be very useful when troubleshooting.  Be wary of the fact that when you update a web server file, it may not immediately be reflected on the pages (especially when viewing JavaScript files, as web browsers often cache these files).  If you make changes to the site and do not see any changes in your browser, the browser shows you cached files.  To remove the cache, right-click on the refresh button within developer tools and click 'Empty cache and hard reload.'  This will test any latest changes on your browser.
 

##### Blog Microservice

CF template: https://cloud-mastery-bootcamp.s3.amazonaws.com/capstones/saa-capstone-1-cf-templates/blog.yaml


1. Setup a HTTP API with a GET method integrated with the **FetchPostFunction** Lambda function. Enable CORS and as follows;

- Access-Control-Allow-Origin = *
- Access-Control-Allow-Headers = *
- Access-Control-Allow-Methods = *
- Access-Control-Expose-Headers = *

Add the invoke URL to your application code (line 6 in the file blog.js).

2. After the initial stack creation, update the Upload Bucket to add the Event notification for triggering the **CreatePostFunction** Lambda function. This sets the S3 event notification for the Lambda function and allows the microservice to work. (**TIP:**  It should only work when .txt files are uploaded using the API call **S3:PutObject** events, triggering the **CreatePostFunction** function. 

##### View Counter

CF template: https://cloud-mastery-bootcamp.s3.amazonaws.com/capstones/saa-capstone-1-cf-templates/viewcounter.yaml

You must set up a Lambda function URL, with CORS enabled as a trigger for the **ViewsFunction** Lambda function.

> Note: for each Lambda function URL in the solution you can set the authentication type to "NONE". Also, CORS should be enabled, to expose all headers, allow all headers, and allow all methods).

Take the time to explore these settings, as multiple HTTP Methods are involved. Expose all headers and allow all headers too.

You will then add this to your application code (line 3 in the file **index.js**, replace the example URL). You can test the function URL works simply by clicking on it - if it does, add it in your **index.js** file. 

##### Contact Form

CF template: https://cloud-mastery-bootcamp.s3.amazonaws.com/capstones/saa-capstone-1-cf-templates/contactform.yaml

Again, use a function URL (CORS enabled, expose all headers, allow all headers, and allow all methods). Update line 34 in the index.js file.

##### AWS Latest News

CF template: https://cloud-mastery-bootcamp.s3.amazonaws.com/capstones/saa-capstone-1-cf-templates/awslatestnews.yaml

Use a function URL for the **UpdateWebpageFunction** Function (CORS enabled, expose all headers, allow all headers, and allow all methods). Update line 2 of the aws.js file.  

>  **Note:** It's worth running a manual test on the RSS Lambda function before you add the microservice to your webpage. This will populate the DynamoDB table with news stories.  Otherwise, your page will be blank until the EventBridge rule runs for the first time, which will be 9 AM UTC. 

#### Testing

At this point you should be able to test the functionality of the website.


#### Step 4 - Create AMI, and build out full network architecture (VPC, ALB, SGs, etc)

You can now follow the target architectural diagram and build a fully operational, scalable, well-architected application. This should include the Auto Scaling group, Application Load Balancer, CloudFront distribution, and Route 53 domain.


##### Step 5 - Migrate to a serverless website

Once you have fully tested the server-based deployment and validated full functionality you can proceed to migrate the website to a fully serverless solution using an S3 static website

# AWS Portfolio Website 

![Architecture Diagram](https://imgur.com/FH0UuvR.png)

![Monolithic website](https://imgur.com/LsZ1YNi.png).


## 📘 Project Overview

This project is a capstone exercise in designing and deploying a cloud-native resume (CV) and AWS Latest News website. The project was completed in two phases: a server-based deployment for high availability and scalability, and a migration to a fully serverless architecture using AWS services.

---

## 🧩 The Project Brief

The client, **exampleCorp**, is migrating their monolithic AWSPortfolio website to AWS. For ten years, the application ran on a single physical server at their head office, with tightly coupled code and backend functionality. Over time, the architecture caused performance bottlenecks, high operational costs, and an inability to iterate quickly.

To resolve this, their development team:
- Extracted static assets (HTML, CSS, JS)
- Converted server-side features into independent **microservices**
- Used AWS services like **Lambda**, **DynamoDB**, and **Amazon EventBridge**
- Packaged the legacy version into an **Amazon Machine Image (AMI)**
- Created **CloudFormation templates** for microservice provisioning

As the **Migration Lead**, my role was to:
- Deploy the EC2-hosted web application using the AMI
- Integrate all microservices via APIs
- Implement security best practices
- Transition the website to a **serverless architecture** using S3, CloudFront, and Route 53

---

## 🚀 Project Stages

### ✅ Stage 1 – Server-Based Highly Available Website

**Key Objectives:**
- Launch the website from the AMI using EC2
- Ensure scalability, fault tolerance, and secure architecture with:
  - **Application Load Balancer**
  - **Auto Scaling Group**
  - **CloudFront CDN**
  - **Route 53 for DNS**
- Integrate microservices using **Lambda** and **API Gateway/Function URLs**
- Apply security principles: no public IPs on EC2 instances, least privilege IAM, strict security groups

---

### ⏭️ Stage 2 – Migration to Serverless Infrastructure

**Key Objectives:**
- Migrate static assets to an **S3 bucket** configured for website hosting
- Update **CloudFront distribution** to serve the S3 site under a custom domain
- Modify **Route 53 DNS records** to point to the new serverless setup

---

## ⚙️ Prerequisites and Setup

> 📍 Region: All resources are deployed in **us-east-1 (N. Virginia)**

---

## 🛠️ Step-by-Step Deployment

### Step 1 – Launch EC2 from AMI

Use the public AMI: `ami-0aa954d8500984aee`  
- SSH into the instance
- Navigate to `/var/www/html`  
- You should see files like:
  - `index.html`, `index.js`
  - `blog.html`, `blog.js`
  - `aws.html`, `aws.js`
  - `style.css`

Access the public IP to preview the site.

---

### Step 2 – Deploy CloudFormation Stacks

Deploy the following CloudFormation templates (in any order):

- [Blog Microservice](https://cloud-mastery-bootcamp.s3.amazonaws.com/capstones/saa-capstone-1-cf-templates/blog.yaml)
- [View Counter](https://cloud-mastery-bootcamp.s3.amazonaws.com/capstones/saa-capstone-1-cf-templates/viewcounter.yaml)
- [Contact Form](https://cloud-mastery-bootcamp.s3.amazonaws.com/capstones/saa-capstone-1-cf-templates/contactform.yaml)
- [AWS Latest News](https://cloud-mastery-bootcamp.s3.amazonaws.com/capstones/saa-capstone-1-cf-templates/awslatestnews.yaml)

---

### Step 3 – Microservice Endpoint Integration

> 💡 Tip: Use Chrome DevTools > Empty Cache + Hard Reload if changes are not reflected.

#### 🔸 Blog Microservice
- Create HTTP API with GET method integrated to `FetchPostFunction`
- Enable CORS with:

Access-Control-Allow-Origin = *
Access-Control-Allow-Headers = *
Access-Control-Allow-Methods = *
Access-Control-Expose-Headers = *

- Add the API URL to `blog.js` (line 6)
- Update the S3 upload bucket to trigger `CreatePostFunction` on `.txt` uploads

#### 🔸 View Counter
- Use Lambda **Function URL** with CORS enabled
- Set auth type to `NONE`
- Add the function URL to `index.js` (line 3)

#### 🔸 Contact Form
- Use Function URL (CORS enabled)
- Add the function URL to `index.js` (line 34)

#### 🔸 AWS Latest News
- Use Function URL for `UpdateWebpageFunction`
- Add to `aws.js` (line 2)
- Run the Lambda manually once to populate DynamoDB before first page load (EventBridge runs at 9 AM UTC)

---

### Step 4 – Create AMI & Deploy Full Architecture

Build out the following:
- VPC
- Public/Private Subnets
- Application Load Balancer
- Security Groups
- Auto Scaling Group
- CloudFront
- Route 53

Reference your architecture diagram for guidance.

---

### Step 5 – Migrate to Serverless Website

Once fully tested:
- Upload static assets to **S3**
- Configure S3 as a static website
- Update CloudFront to use S3 as the origin
- Update **Route 53** DNS to point to CloudFront

---

## ✅ Final Thoughts

This project demonstrates end-to-end cloud migration from a monolithic application to a fully managed, serverless AWS architecture — following the principles of scalability, security, fault-tolerance, and cost optimization.

---

## 🧰 Technologies Used

- AWS EC2, AMI
- S3, CloudFront, Route 53
- Lambda, DynamoDB, EventBridge
- API Gateway, Function URLs
- CloudFormation
- IAM, Security Groups




# AWS Portfolio Website 

![Architecture Diagram](https://imgur.com/FH0UuvR.png)

![Monolithic website](https://imgur.com/LsZ1YNi.png).

A scalable, serverless, and cost-optimized AWS portfolio website showcasing dynamic blog functionality, resume hosting, a contact form, and integration with AWS news via RSS—all built using modern AWS services.

## Table of Contents
- [Architecture Overview](#architecture-overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Deployment Workflow](#deployment-workflow)
- [Cost Optimization Note](#cost-optimization-note)
- [Lessons Learned](#lessons-learned)

  ## Architecture Overview

### Frontend Delivery
- **Amazon CloudFront** with SSL via **ACM**
- Custom Domain: `https://yourdomain.com`

### Content Storage
- **Upload S3 Bucket** (for blog text, resumes)
- **Transformed HTML S3 Bucket** (for frontend)

### Compute Layer
- **EC2 Auto Scaling Group** in private subnets
- **Application Load Balancer** (ALB)

### Serverless Features
- **AWS Lambda**: for blog uploads, contact form, blog fetch, and AWS news
- **API Gateway HTTP APIs** for frontend interaction

### Data & Automation
- **DynamoDB** for view tracking
- **EventBridge** scheduled jobs
- **SNS** email notification from contact form

*See the full architecture diagram above.*

## Features

✅ Upload blog content (via S3 → Lambda)  
✅ View dynamic blog list via Lambda + API Gateway  
✅ Contact form with SNS email alerts  
✅ Auto-scaled EC2 for dynamic processing (private subnet)  
✅ Page view counter stored in DynamoDB  
✅ Daily AWS News RSS Fetcher  
✅ HTTPS-secured with custom domain  
✅ Event-driven architecture (S3 triggers, EventBridge)


## Tech Stack

- AWS S3 (Static hosting, content storage)
- Amazon CloudFront (CDN)
- AWS Lambda (Serverless compute)
- Amazon EC2 + Auto Scaling Group (dynamic processing)
- Amazon ALB (load balancing)
- Amazon API Gateway (HTTP APIs)
- Amazon SNS (email notifications)
- Amazon DynamoDB (view tracking)
- Amazon EventBridge (scheduled events)
- ACM (SSL certificates)
- CloudFormation (Infrastructure as Code)
- Route 53 (Domain routing)


## Deployment Workflow

1. 🔧 Created VPC, private/public subnets, route tables (via CloudFormation)
2. 🚀 Launched EC2 web servers in Auto Scaling Group with ALB
3. 🗂️ Set up S3 buckets for content upload and transformed HTML
4. ⚙️ Created Lambda functions for:
    - Uploading blogs/resumes
    - Fetching blog list
    - Sending contact form messages
    - Fetching AWS news daily
5. 🌐 Configured API Gateway with Lambda integrations
6. 🔔 Enabled EventBridge rules and S3 triggers
7. 📬 Set up SNS topic for contact form email
8. ✅ Connected CloudFront to S3 + ACM SSL + Route 53 domain




## Cost Optimization Note

To minimize AWS charges after project completion, the live website and certain resources (e.g., CloudFront distribution, EC2 instances) should deleted at the end. 

## Lessons Learned

- Building real-world architectures using multiple AWS services
- Managing IAM roles and permissions for secure communication
- Debugging Lambda, S3, and API Gateway integrations
- Working with event-driven architecture (S3, EventBridge)
- Using CloudFormation for reproducible infrastructure



# Sample-3-Tier-Application-Architecture-Deployment-on-AWS

## Overview
This project demonstrates the deployment of a highly scalable and secure 3-Tier Architecture on AWS, utilizing services such as VPC, EC2, RDS, ALB, ASG, S3, and Route 53. The architecture is designed for high availability, security, and scalability, using Auto Scaling Groups (ASG), load balancing, and secure networking.

## Tech Stack
AWS Services: EC2, VPC, RDS, ALB, ASG, S3, IAM, Route 53, ACM

Web Tier: Nginx, Node.js (React frontend)

Application Tier: Node.js (Express backend), PM2

Database Tier: Amazon RDS (MySQL)

Security: IAM Roles, Security Groups, Private Subnets

# Deployment Steps

## 1. Create VPC and Network Setup
- Created a custom VPC (sample: 192.168.0.0/16)

- 2 Public Subnets for web servers.

- 4 Private Subnets (2 for application servers, 2 for RDS).

- NAT Gateway for private subnet internet access.


## 2. Configure Security Groups

- Web ALB-SG: Allows HTTP/HTTPS traffic from the internet.

- Web-SG: Allows traffic from Web ALB.

- App ALB-SG: Allows traffic from Web Servers.

- App-SG: Allows traffic on port 4000 from App ALB.

- Database-SG: Restricts access to App Servers.

## 3. Setup S3 bucket for code storage

- Created S3 bucket (sample: 3-tier-project).
  
- Uploaded application and configuration files.

## 4. IAM Role for EC2 Instances

- Created IAM Role (3-tier-role) with EC2 + SSM permissions for remote access.

## 5. Deploy Application Tier

- Created Amazon RDS (MySQL) instance:

  - Placed in private subnets for security.

  - Assigned Database-SG.

  - Updated credentials in DbConfig.js and re-uploaded to S3.

## 6. Deploy Application tier

- Launched EC2 instances in private subnets for the app tier.

- Configured Node.js and PM2 for backend process management.

- Connected to RDS and set up the webappdb database.

- Created an internal ALB to route traffic to app servers.

## 7. Deploy Web Tier

- Launched EC2 instances in public subnets for the web tier.

- Installed Nginx as a reverse proxy.

- Connected Nginx to the internal ALB for app requests.

## 8. Configure Load Balancers

- Internal ALB: Directs traffic to app servers on port 4000.

- External ALB: Directs internet traffic to web servers.

## 9. Setup Auto Scaling

- Created launch templates for both web and app servers.

- Configured Auto Scaling Groups (ASG) with:

  - Min instances: 2

  - Max instances: 6

- Scaling trigger: 70% CPU utilization

# Future Improvements

- Implement CloudFront for CDN caching.

- Enable WAF (Web Application Firewall) for security.

- Use Terraform for Infrastructure as Code (IaC).

# Conclusion

This project showcases expertise in AWS cloud architecture, infrastructure automation, security best practices, and high-availability system design. The 3-Tier Architecture ensures scalability, security, and resilience, making it suitable for enterprise applications.






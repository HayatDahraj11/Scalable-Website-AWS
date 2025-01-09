# Credentials & Certifications
<img width="794" alt="image" src="https://github.com/user-attachments/assets/92437a04-6e38-4621-a962-c2109eec37a0" />

![aws-academy-graduate-aws-academy-cloud-web-applicat-2](https://github.com/user-attachments/assets/7c00e4b3-ebb6-452e-a5f2-d7bd72903537)




## Description
This project implements a highly available, scalable, and secure student records management system using AWS cloud infrastructure. The architecture leverages multiple AWS services to create a robust application environment that can handle varying loads while maintaining security and performance. By utilizing services like VPC, EC2, RDS, and Auto Scaling Groups, we've created a production-ready infrastructure that demonstrates cloud-native architectural principles.

## Architecture Overview
The system is built using a multi-tier architecture approach:

### Networking Layer (VPC)
The foundation starts with a carefully planned Virtual Private Cloud that creates a secure, isolated network environment:
- CIDR Block: 10.0.0.0/16 providing 65,536 IP addresses
- Public Subnets: 10.0.0.0/20 (us-east-1a) and 10.0.16.0/20 (us-east-1b)
- Private Subnets: Dedicated subnets for RDS with restricted access
- Internet Gateway for public access
- NAT Gateway enabling private resources to access the internet securely

### Application Layer
The application tier implements a scalable design using:
- EC2 instances running Node.js applications
- Application Load Balancer distributing traffic
- Auto Scaling Group maintaining optimal instance count
- Health checks ensuring system reliability

### Database Layer
A secure and managed database implementation using:
- Amazon RDS running MySQL 8.0
- Private subnet placement for enhanced security
- Automated backups and maintenance
- Secrets Manager integration for credential management

## Key Features
- High Availability: Multi-AZ deployment across us-east-1a and us-east-1b
- Auto Scaling: Dynamic instance adjustment based on CPU utilization
- Security: Layered security groups and network isolation
- Managed Database: RDS with automated maintenance and backups
- Load Balancing: Intelligent traffic distribution across instances
- Secret Management: Secure credential handling through AWS Secrets Manager

## Technical Configuration

### Security Groups
1. Web Server Security Group (StudentRecords-WebServer-SG):
   - HTTP (80): Allow all incoming
   - SSH (22): Restricted to specific IP
   - MySQL (3306): Allow from DB security group

2. Database Security Group (StudentRecords-DB-SG):
   - MySQL (3306): Allow from Web Server security group only

### Auto Scaling Configuration
- Minimum: 1 instance
- Maximum: 3 instances
- Target CPU Utilization: 50%
- Health Check Grace Period: 300 seconds

### Load Balancer Setup
- Type: Application Load Balancer
- Listeners: HTTP on port 80
- Health Check Path: '/'
- Target Group: StudentRecordsApp-TG

## Deployment Instructions
1. Network Setup:
   ```bash
   # Create VPC and subnets
   aws ec2 create-vpc --cidr-block 10.0.0.0/16
   aws ec2 create-subnet --vpc-id <vpc-id> --cidr-block 10.0.0.0/20
   ```

2. Database Initialization:
   ```sql
   -- Create required schemas
   CREATE DATABASE studentrecords;
   USE studentrecords;
   ```

3. Application Deployment:
   ```bash
   # Install dependencies
   npm install
   
   # Start application
   npm start
   ```

## What I Learned
Throughout this project, I gained deep insights into cloud architecture and AWS services:

### Infrastructure as Code
Understanding how to design and implement cloud infrastructure taught me:
- The importance of proper network segmentation
- How to balance security with accessibility
- The value of automation in infrastructure management

### Database Management
Working with RDS provided lessons in:
- Database migration strategies
- Secure credential management
- High availability database configuration

### Load Balancing and Scaling
Implementing ALB and ASG taught me:
- How to design for variable workloads
- The importance of proper health checks
- Strategies for maintaining application availability

### Security Best Practices
Through implementing security measures, I learned:
- The principle of least privilege
- Network security design patterns
- Secure secret management strategies

## Monitoring and Maintenance
The infrastructure includes several monitoring points:
- Load balancer metrics
- Instance health status
- Database performance metrics
- Auto scaling events

## Troubleshooting Guide
Common issues and their solutions:
1. Database Connectivity:
   - Check security group rules
   - Verify network connectivity through VPC
   - Validate credentials in Secrets Manager

2. Application Scaling:
   - Monitor CPU utilization metrics
   - Check ALB health check configurations
   - Verify launch template settings

## Future Enhancements
- Implement CloudFront for content delivery
- Add WAF for enhanced security
- Implement blue-green deployment strategy
- Add database read replicas for scaling




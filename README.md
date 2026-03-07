# AWS Highly Available Web Architecture

This project demonstrates a production-style **AWS 3-tier architecture** designed for **high availability, scalability, and secure networking**.

## Architecture Overview

```text
Internet
   ↓
Application Load Balancer
   ↓
Auto Scaling EC2 (private subnets)
   ↓
RDS MySQL Database
```

# AWS Highly Available Web Architecture

This project demonstrates a production-style AWS 3-tier architecture designed for high availability, scalability, and secure networking.

## Architecture Diagram

![Architecture Diagram](architecture/architecture-diagram.png)


## AWS Services Used

- VPC
- Public Subnets
- Private Subnets
- Internet Gateway
- NAT Gateway
- Application Load Balancer
- Target Groups
- EC2 Launch Templates
- Auto Scaling Groups
- RDS MySQL
- IAM Role for EC2
- Session Manager
- CloudWatch Monitoring

## Network Layout

```text
VPC CIDR: 10.0.0.0/16

Public Subnets
10.0.1.0/24
10.0.2.0/24

Private App Subnets
10.0.11.0/24
10.0.12.0/24

Private DB Subnets
10.0.21.0/24
10.0.22.0/24
```

## Security Model

- Internet → ALB
- ALB → EC2 instances
- EC2 → RDS database

Direct internet access to EC2 and RDS is not allowed.

## Auto Scaling Configuration

- Minimum capacity: 2
- Desired capacity: 2
- Maximum capacity: 4

Health checks are performed through the Application Load Balancer.

## Application Layer

Each EC2 instance automatically installs Apache and serves a web page displaying the instance ID.

## Database Layer

Amazon RDS MySQL is deployed in private DB subnets.

Tested successfully:
- EC2 → RDS connection
- database creation
- table creation
- insert and select queries

## Monitoring

Metrics observed using:
- CloudWatch EC2 metrics
- Load Balancer health checks
- Auto Scaling activity

## Resilience Test

An EC2 instance was manually terminated to simulate failure.

Result:
- Auto Scaling launched a replacement instance
- target group returned to healthy state
- application remained available

## Screenshots

### 1. VPC Resource Map
![VPC Resource Map](screenshots/01-vpc-resource-map.png)

### 2. Application Load Balancer
![Application Load Balancer](screenshots/02-application-load-balancer.png)

### 3. Target Group Health
![Target Group Health](screenshots/03-target-group-healthy-instances.png)

### 4. Auto Scaling Group
![Auto Scaling Group](screenshots/04-auto-scaling-group.png)

### 5. Launch Template
![Launch Template](screenshots/05-ec2-launch-template.png)

### 6. Web Application Through Load Balancer
![Web Application](screenshots/06-alb-webpage-instance-response.png)

### 7. RDS MySQL Instance
![RDS MySQL Instance](screenshots/07-rds-mysql-instance.png)

### 8. EC2 to RDS MySQL Connection
![EC2 to RDS MySQL Connection](screenshots/08-ec2-to-rds-mysql-connection.png)

### 9. Database Created
![Database Created](screenshots/09-mysql-database-created.png)

### 10. Query Results
![Query Results](screenshots/10-mysql-query-results.png)

## Key Outcomes

This project demonstrates practical experience with:
- VPC networking
- high availability architecture
- secure subnet design
- load balancing
- Auto Scaling
- RDS connectivity
- Session Manager access
- monitoring and resilience testing

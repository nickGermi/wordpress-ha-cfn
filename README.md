# Overview

Creates a highly available Wordpress website using CloudFormation within ap-southeast-2 region*.

### AWS Resources Created:

- Amazon Virtual Private Cloud
- Internet Gateway
- NAT Gateway with Elastic IP address
- 2 Public and 2 Private subnets across ap-southeast-2a & ap-southeast-2b
- Routing tables for public subnets routing through Internet Gateway
- Routing tables for private subnets routing through NAT Gateway
- Mulitple VPC Security Groups for RDS, EFS, Wordpress instances & ALB
- IAM Role and associated instance profile
- Amazon RDS Aurora cluster in private subnets with a read replica
- Amazon EFS file system in both private subnets
- Amazon ELB Application Load Balancer in both public subnets
- Auto Scaling Group launching Wordpress instances in both private subnets

### Input Parameters

|Name                   |Value                  |
|-----------------------|-----------------------|
|Stack name             |Wordpress              |
|VPC CIDR               |10.0.0.0/16            |
|Public Subnet 0        |10.0.10.0/24           |
|Public Subnet 1        |10.0.11.0/24           |
|Private Subnet 0       |10.0.0.0/24            |
|Private Subnet 1       |10.0.1.0/24            |
|Database Username      |dbadmin                |
|Database Password      |********               |
|Database Instance Class|db.t2.medium           |
|Auto Scaling Max       |4                      |
|Auto Scaling Min       |2                      |
|Wordpress Version      |latest                 |
|Site title             |HA WordPress site      |
|Admin Username         |admin                  |
|Admin Password         |********               |
|Email Address          |email@example.com      |
|Wordpress Directory    |technical-challenge    |

### Development enviroment

You may set auto scaling max and min values to `1` and use a modified template which only utilizes a single AZ reducing the RDS instance to 1 without a read replica & EFS with only a single AZ target.

`
*Region restriction is due to hard coded Wordpress AMI id
`
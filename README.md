# Project1-aws-3-tier-web-application
AWS 3-Tier Architecture Project | VPC | EC2 | RDS MariaDB | NAT Gateway | Security Groups | Bastion Host | Web Server | application Server 

**Project Overview**
______________________________________________________________________________________________________________________
This project demonstrates the deployment of a secure 3-Tier Architecture on AWS using industry-standard networking and security practices.
______________________________________________________________________________________________________________________
The architecture consists of:

**Bastion Host (Administration Layer)
Web Server (Presentation Layer)
Application Server (Business Logic Layer)
Amazon RDS MariaDB (Database Layer)**

The infrastructure is deployed within a custom VPC using public and private subnets, Internet Gateway, NAT Gateway, Route Tables, and Security Groups.

Architecture Diagram
## Architecture Diagram

                     Internet
                        │
                        ▼
                Elastic IP Address
                        │
                        ▼
                 EC2 Web Server
              (Apache + PHP App)
                        │
                        ▼
                  Amazon RDS
                     MariaDB
                        │
                        ▼
                  Automated Backup


## Traffic Flow


                      Internet Users
                             │
                             ▼
                    Internet Gateway
                             │
                             ▼
                    Web Server (EC2)
                         Port 80/443
                             │
                             ▼
                   App Server (EC2)
                     Internal Traffic
                             │
                             ▼
                Amazon RDS MariaDB
                         Port 3306





Architecture Components
1) **VPC**

A custom VPC was created with CIDR block:

192.168.0.0/16

Subnets
Subnet	CIDR
Public Subnet	192.168.1.0/24
Private Subnet 1 (App Tier)	192.168.2.0/24
Private Subnet 2 (DB Tier)	192.168.3.0/24
Private Subnet 3	192.168.4.0/24

2) **Internet Gateway**

Provides internet access to resources deployed within the public subnet.

3) **NAT Gateway**

Allows resources deployed in private subnets to access the internet for software updates while remaining inaccessible from the public internet.

4) **Security Groups**

Separate security groups were created for:

Bastion Host
Web Server
Application Server
Database Server

Traffic was restricted based on the principle of least privilege.
________________________________________________________________________________________________________________________

**AWS Services Used**
Amazon VPC
Subnet
Elastic IP
Internet Gateway
NAT Gateway
Route Tables
Security Groups
Amazon EC2
Amazon RDS (MariaDB)
-----------------------------------------------------------------------------------------------------------------------


## Project Workflow

1. Design VPC Architecture
2. Create Networking Components
3. Configure Security Groups
4. Deploy EC2 Instances
5. Provision Amazon RDS
6. Configure Routing
7. Validate Connectivity
8. Document Architecture

________________________________________________________________________________________________________________________
**Implementation Steps**

**1. Created Network Infrastructure**
Created a custom VPC with CIDR block 192.168.0.0/16
Created one public subnet and three private subnets
Distributed subnets across multiple Availability Zones
Configured Internet Gateway for public internet access
Allocated Elastic IP and configured NAT Gateway
Created Public and Private Route Tables
Associated subnets with their respective route tables

**2. Configured Security Controls**
Created dedicated Security Groups for:
Bastion Host
Web Server
Application Server
Database Server
Configured controlled communication between tiers using Security Group references.

**3. Deployed Compute Resources**
Provisioned EC2 instances for:
Bastion Host (Public Subnet)
Web Server (Public Subnet)
Application Server (Private Subnet)
Configured Apache HTTP Server on the Web Server using EC2 User Data.
Configured MariaDB client packages on the Application Server.

**4. Provisioned Database Layer**
Created a DB Subnet Group
Configured Amazon RDS MariaDB
Deployed database in private subnets
Disabled public access
Associated Database Security Group

**5. Configured Routing**
Public Route Table:
Internet Gateway Route (0.0.0.0/0)
Private Route Table:
NAT Gateway Route (0.0.0.0/0)

**6. Performed Connectivity Validation**
Validated:
SSH access through Bastion Host
Communication between Web Server and Application Server
Connectivity from Application Server to Amazon RDS
Successful execution of SQL queries against MariaDB

Executed:

MariaDB [(none)]> SHOW DATABASES;

+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| appdb              |
+--------------------+

**This confirmed:**

Network connectivity
Security Group configuration
Database authentication
Successful application-to-database communication

---------------------------------------------------------------------------------------------------------------------------

Screenshots attached in a seperate file

---------------------------------------------------------------------------------------------------------------------------

**Key Learnings**

AWS VPC Design
Public and Private Subnet Architecture
Route Table Configuration
NAT Gateway Implementation
Security Group Design
Bastion Host Administration
Amazon RDS Connectivity
Linux Server Administration
EC2 User Data Automation
----------------------------------------------------------------------------------------------------------------------------
Challenges Faced

Understanding subnet routing behavior
Configuring secure communication between application tiers
Troubleshooting Security Group rules
Establishing RDS connectivity from private resources

**Future Improvements**
Application Load Balancer
Auto Scaling Groups
Infrastructure as Code using Terraform
Monitoring with Amazon CloudWatch
CI/CD using GitHub Actions
Multi-AZ High Availability Deployment

Conclusion
-------------------------------------------------------------------------------------------------------------------------
This project demonstrates the implementation of a secure and scalable AWS 3-Tier Architecture using cloud networking, compute, and database services. The deployment follows cloud security best practices and provides a strong foundation for production-grade application hosting environments.

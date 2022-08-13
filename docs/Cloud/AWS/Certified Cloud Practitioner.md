# AWS Certified Cloud Practitioner

[🔗Udemy Course](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/?couponCode=AUG_22_GET_STARTED)

## IAM

### Users & Groups

> IAM: Identity and Access Management, A Global service

* Root account created by default, shouldn’t be used or shared
* Users are people within your organization, and can be grouped
* Groups only contain users, not other groups
* Users don’t have to belong to a group, and user can belong to multiple groups

### Permissions

* Users or Groups can be assigned JSON documents called **policies**
* These policies define the permissions of the users
* In AWS you apply the least privilege principle: don’t give more permissions than a user needs

### IAM Policies Structure

* `Version`: policy language version,always include“2012-10-17”
* `Id`: an identifier for the policy(optional)
* `Statement`: one or more individual statements(required)
  * `Sid`: an identifier for the statement(optional)
  * `Effect`: whether the statement allows or denies access (Allow, Deny)
  * `Principal`: account/user/role to which this policy applied to
  * `Action`: list of actions this policy allows ordenies
  * `Resource`: list of resources to which the actions applied to
  * `Condition`: conditions for when this policy is ineffect (optional)

### IAM Security Tools

* IAM Credentials Report (account-level)
  * a report that lists all your account's users and the status of their various credentials
* IAM Access Advisor (user-level)
  * Access advisor shows the service permissions granted to a user and when those services were last accessed.
  * You can use this information to revise your policies.

## EC2

> EC2: Elastic Compute Cloud  
> EC2 Instance: AMI (OS) + Instance Size (CPU + RAM) + Storage + security groups + EC2 User Data

### Sizing & Configuration Options

* Operating System (OS): Linux, Windows or Mac OS
* Compute power & Cores (CPU)
* Random-access Memory (RAM)
* Storage Space:
  * Network-attached (EBS & EFS)
  * Hardware (EC2 Instance Store)
* Network Card: speed of the card, Public IP address
* Firewall Rules: security group
* Bootstrap Script (configure at first launch): EC2 User Data

### Instance Types

[🔗Homepage](https://aws.amazon.com/ec2/instance-types/)

* General Purpose: Great for a diversity of workloads such as web servers or code repositories
* Compute Optimized: Great for compute-intensive tasks that require high performance processors
* Memory Optimized: Fast performance for workloads that process large data sets in memory
* Storage Optimized: Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage

### Security Groups

* Security groups **only contain allow** rules
* Security groups rules can reference by IP or by security group
* Security groups are acting as a “firewall” on EC2 instances
* They regulate:
  * Type + Protocol
    * Control of inbound network (from other to the instance)
    * Control of outbound network (from the instance to other)
  * Source: Authorised IP ranges – IPv4 and IPv6 / other security group
  * Port Range
* Locked down to a region / VPC combination
* It’s good to maintain one separate security group for SSH access
* All inbound traffic is **blocked** by default
* All outbound traffic is **authorised** by default

### Instances Purchasing Options

* `On-Demand Instances`
  * short workload, predictable pricing, pay by second
  * highest cost but no upfront payment
* `Reserved` (1 & 3 years)
  * Reserved Instances – long workloads
  * Convertible Reserved Instances – long workloads with flexible instances
* `Savings Plans` (1 & 3 years)
  * commitment to an amount of usage, long workload
  * usage beyond EC2 Savings Plans is billed at the On-Demand price
  * locked to a specific instance family & AWS region
* `Spot Instances`
  * the **most cost-efficient** instances in AWS
  * short workloads, cheap, can lose instances (less reliable)
* `Dedicated Hosts`
  * book an entire physical server, control instance placement
  * allows address compliance requirements and use existing server- bound software licenses
  * The **most expensive** option
* `Dedicated Instances`
  * no other customers will share your hardware
  * may share hardware with other instances in same account
  * no control over instance placement
* `Capacity Reservations`
  * reserve capacity in a specific AZ for any duration
  * no time commitment (create/cancel anytime), no billing discounts
  * suitable for short-term, uninterrupted workloads that needs to be in a specific AZ

### AMI

> AMI: Amazon Machine Image

* AMI are a customization of an EC2 instance
  * You add your own software, configuration, operating system, monitoring...
  * Faster boot / configuration time because all your software is pre-packaged
* AMI are built for a specific region (and can be copied across regions)
* You can launch EC2 instances from:
  * A Public AMI: AWS provided
  * Your own AMI: you make and maintain them yourself
  * An AWS Marketplace AMI: an AMI someone else made (and potentially sells)

### EC2 Image Builder

* Used to **automate the creation** of Virtual Machines or container images
* Automate the creation, maintain, validate and test EC2 AMIs
* Can be run on a schedule (weekly, whenever packages are updated, etc...)
* Free service (only pay for the underlying resources)

### EC2 Instance Store

> high-performance hardware disk

* Better I/O performance
* EC2 Instance Store **lose** their storage if they’re stopped (ephemeral)
* Good for buffer / cache / scratch data / temporary content
* Risk of data loss if hardware fails
* Backups and Replication are your responsibility

### EBS Volume

> An EBS (Elastic Block Store) Volume is a network drive you can attach to your instances while they run

* It’s a network drive (i.e. not a physical drive)
  * It uses the network to communicate the instance, which means there might be a bit of latency
  * It can be detached from an EC2 instance and attached to another one quickly
* It’s locked to an Availability Zone (AZ)
  * To move a volume across, you first need to snapshot it
* Have a provisioned capacity (size in GBs, and IOPS)
  * You get billed for all the provisioned capacity
  * You can increase the capacity of the drive over time
* Delete on Termination attribute: Controls the EBS behaviour when an EC2 instance terminates
  * By default, the root EBS volume is deleted (attribute enabled)
  * By default, any other attached EBS volume is not deleted (attribute disabled)
  * This can be controlled by the AWS console / AWS CLI
* EBS Snapshots
  * Make a backup (snapshot) of your EBS volume at a point in time
  * Not necessary to detach volume to do snapshot, but recommended
  * Can copy snapshots across AZ or Region

### EFS

> Elastic File System

* Managed NFS (network file system) that can be mounted on 100s of EC2
* EFS works with **Linux** EC2 instances in multi-AZ
* Highly available, scalable, expensive (3x gp2), pay per use, no capacity planning
* EFS Infrequent Access (EFS-IA): Storage class that is cost-optimized for files not accessed every day

### Amazon FSx

* Launch 3rd party high-performance file systems on AWS
* Fully managed service
* `Amazon FSx for Windows File Server`: A fully managed, highly reliable, and scalable Windows native shared file system
  * Built on Windows File Server
  * Supports SMB protocol & Windows NTFS
  * Integrated with Microsoft Active Director y
  * Can be accessed from AWS or your on-premise infrastructure
* `Amazon FSx for Lustre`: A fully managed, high-performance, scalable file storage for High Performance Computing (HPC)
  * The name Lustre is derived from “Linux” and “cluster”
  * Machine Learning, Analytics,Video Processing, Financial Modeling, ...
  * Scales up to 100s GB/s, millions of IOPS, sub-ms latencies

## ELB & ASG

> ELB: Elastic Load Balancing  
> ASG: Auto Scaling Group

### High Availability & Scalability For EC2

* Vertical Scaling: Increase instance size (= scale up / down)
* Horizontal Scaling: Increase number of instances (= scale out / in)
* High Availability: Run instances for the same application across multi AZ
  * Auto Scaling Group multi AZ
  * Load Balancer multi AZ

### Scalability vs Elasticity vs Agility

* `Scalability`: ability to accommodate a larger load by making the hardware stronger (scale up), or by adding nodes (scale out)
* `Elasticity`: once a system is scalable, elasticity means that there will be some “auto-scaling” so that the system can scale based on the load.This is “cloud-friendly”: pay-per-use, match demand, optimize costs
* `Agility`: new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes.

### Elastic Load Balancer

* An ELB (Elastic Load Balancer) is a managed load balancer
  * AWS guarantees that it will be working
  * AWS takes care of upgrades, maintenance, high availability
  * AWS provides only a few configuration knobs
* It costs less to setup your own load balancer but it will be a lot more effort on your end (maintenance, integrations)
* 3 kinds of load balancers offered by AWS:
  * `Application Load Balancer` (HTTP / HTTPS only) – Layer 7
  * `Network Load Balancer` (ultra-high performance, allows for TCP) – Layer 4
  * `Classic Load Balancer` (slowly retiring) – Layer 4 & 7

### Auto Scaling Group

* In real-life, the load on your websites and application can change
* In the cloud, you can create and get rid of servers very quickly
* The goal of an Auto Scaling Group (ASG) is to:
  * Scale out (add EC2 instances) to match an increased load
  * Scale in (remove EC2 instances) to match a decreased load
  * Ensure we have a minimum and a maximum number of machines running
  * Automatically register new instances to a load balancer
  * Replace unhealthy instances
* Cost Savings: only run at an optimal capacity (principle of the cloud)
* Scaling Strategies
  * Manual Scaling: Update the size of an ASG manually
  * Dynamic Scaling: Respond to changing demand
    * Simple / Step Scaling
    * TargetTracking Scaling
    * Scheduled Scaling
  * Predictive Scaling: Uses Machine Learning to predict future traffic ahead of time

## S3

### Use Cases

* Backup and storage
* Disaster Recovery
* Archive
* Hybrid Cloud storage
* Application hosting
* Media hosting
* Data lakes & big data analytics
* Software delivery
* Static website

### Buckets

* Amazon S3 allows people to store objects (files) in “buckets” (directories)
* Buckets must have a globally unique name (across all regions all accounts)
* Buckets are **defined at the region level**
* S3 looks like a global service but buckets are **created in a region**
* Naming convention
  * No uppercase
  * No underscore
  * 3-63 characters long
  * Not an IP
  * Must start with lowercase letter or number

### Objects

* Objects (files) have a `Key`
  * The key is the **FULL path**
  * The key is composed of **prefix + object name**
  * There’s no concept of “directories” within buckets despite of UI
  * Just keys with very long names that contain slashes (“/”)
* Object `Values` are the content of the body
* `Metadata` (list of text key / value pairs – system or user metadata)
* `Tags` (Unicode key / value pair – up to 10) – useful for security / lifecycle
* `Version ID` (if versioning is enabled)

### Security

* User based
  * IAM policies - which API calls should be allowed for a specific user from IAM console
* Resource Based
  * Bucket Policies - bucket wide rules from the S3 console - allows cross account
  * Object Access Control List (ACL) – finer grain
  * Bucket Access Control List (ACL) – less common
* Note: an IAM principal can access an S3 object if
  * the user IAM permissions allow it OR the resource policy ALLOWS it
  * AND there’s no explicit DENY
* Encryption: encrypt objects in Amazon S3 using encryption keys

### Versioning

* You can version your files in Amazon S3
* It is enabled at the bucket level
* Same key overwrite will increment the “version”: 1, 2, 3....
* It is best practice to version your buckets
  * Protect against unintended deletes (ability to restore a version)
  * Easy roll back to previous version
* Notes:
  * Any file that is not versioned prior to enabling versioning will have version “null”
  * Suspending versioning does not delete the previous versions

### Replication

* Must enable versioning in source and destination
* Must give proper IAM permissions to S3
* Buckets can be in different accounts
* Copying is asynchronous
* Cross Region Replication (CRR): compliance, lower latency access, replication across accounts
* Same Region Replication (SRR): log aggregation, live replication between production and test accounts

### Storage Classes

* Standard: General Purpose
* Infrequent Access (IA)
* One Zone: Infrequent Access
* Glacier Instant Retrieval
* Glacier Flexible Retrieval
* Glacier Deep Archive
* Intelligent Tiering

### S3 Object Lock & Glacier Vault Lock

* S3 Object Lock
  * Adopt a WORM (Write Once Read Many) model
  * Block an object version deletion for a specified amount of time
* Glacier Vault Lock
  * Adopt a WORM (Write Once Read Many) model
  * Lock the policy for future edits (can no longer be changed)
  * Helpful for compliance and data retention

### Snow Family

> Highly-secure, portable devices to collect and process data at the edge, and migrate data into and out of AWS

* Data migration:
  * Snowcone(TB)
  * Snowball Edge(TB/PB)
  * Snowmobile(PB): Better than Snowball if you transfer more than 10 PB
* Edge Computing:
  * Snowcone
  * Snowball Edge

`AWS OpsHub`: A software installed on your computer to manage Snow Family Decives

### AWS Storage Gateway

* Bridge between on-premise data and cloud data in S3
* Hybrid storage service to allow on-premises to seamlessly use the AWS Cloud
* Use cases:
  * disaster recovery
  * backup & restore
  * tiered storage
* Types of Storage Gateway:
  * File Gateway
  * Volume Gateway
  * Tape Gateway

## Databases

### AWS RDS

> RDS stands for Relational Database Service

* It’s a managed DB service for DB use SQL as a query language.
* It allows you to create databases in the cloud that are managed by AWS
  * Postgres
  * MySQL
  * MariaDB
  * Oracle
  * Microsoft SQL Server
  * Aurora (AWS Proprietary database)
* RDS is a managed service:
  * Automated provisioning, OS patching
  * Continuous backups and restore to specific timestamp (Point in Time Restore)!
  * Monitoring dashboards
  * Read replicas for improved read performance
  * Multi AZ setup for DR (Disaster Recovery)
  * Maintenance windows for upgrades
  * Scaling capability (vertical and horizontal)
  * Storage backed by EBS (gp2 or io1)
* BUT you can’t SSH into your instances

### Amazon Aurora

* Aurora is a proprietary technology from AWS (not open sourced)
* PostgreSQL and MySQL are both supported as Aurora DB
* Aurora is “AWS cloud optimized” and claims 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
* Aurora storage automatically grows in increments of 10GB, up to 64 TB.
* Aurora costs more than RDS (20% more) – but is more efficient
* Not in the free tier

### Amazon ElasticCache

* `ElastiCache` is to get managed **Redis or Memcached**
* Caches are in-memory databases with high performance, low latency
* Helps reduce load off databases for read intensive workloads
* AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups

### DynamoDB

* Fully Managed Highly available with replication across 3 AZ
* **NoSQL** database(key/value)
* Scales to massive workloads, distributed “serverless” database
* Millions of requests per seconds, trillions of row, 100s of TB of storage
* Fast and consistent in performance
* Single-digit millisecond latency – low latency retrieval
* Integrated with IAM for security, authorization and administration
* Low cost and auto scaling capabilities
* Standard & Infrequent Access (IA) Table Class

#### DynamoDB Accelerator - DAX

* Fully Managed in-memory cache for DynamoDB
* 10x performance improvement – single- digit millisecond latency to microseconds latency – when accessing your DynamoDB tables
* Secure, highly scalable & highly available
* Difference with ElastiCache at the CCP level:
  * DAX is **only** used for and is integrated with DynamoDB
  * ElastiCache **can** be used for other databases

#### Global Tables

* Make a DynamoDB table accessible with low latency in multiple-regions
* Active-Active replication (read/write to any AWS Region)

### Redshift

* Redshift is based on PostgreSQL, but it’s not used for OLTP
* It’s OLAP – online analytical processing (analytics and data warehousing)
* Load data once every hour, not every second
* 10x better performance than other data warehouses, scale to PBs of data
* Columnar storage of data (instead of row based)
* Massively Parallel Query Execution (MPP), highly available
* Pay as you go based on the instances provisioned
* Has a SQL interface for performing the queries
* BI tools such as AWS Quicksight or Tableau integrate with it

### Amazon EMR

> EMR stands for “Elastic MapReduce”

* EMR helps creating Hadoop clusters (Big Data) to analyze and process vast amount of data
* The clusters can be made of hundreds of EC2 instances
* Also supports Apache Spark, HBase, Presto, Flink...
* EMR takes care of all the provisioning and configuration
* Auto-scaling and integrated with Spot instances
* Use cases: data processing, machine learning, web indexing, big data...

### Amazon Athena

* Serverless query service to analyze data stored in Amazon S3
* Uses standard SQL language to query the files
* Supports CSV, JSON, ORC, Avro, and Parquet(builtonPresto)
* Pricing: $5.00 per TB of data scanned
* Use compressed or columnar data for cost-savings (less scan)
* Use cases: Business intelligence / analytics / reporting, analyze & query VPC Flow Logs, ELB Logs, CloudTrail trails, etc...

### Amazon QuickSight

* Serverless machine learning-powered business intelligence service to **create interactive dashboards**
* Fast, automatically scalable, embeddable, with per-session pricing
* Use cases:
  * Business analytics
  * Building visualizations
  * Perform ad-hoc analysis
  * Get business insights using data
  * Integrated with RDS, Aurora, Athena, Redshift, S3...

### DocumentDB

* MongoDB is used to store, query, and index JSON data • Similar “deployment concepts” as Aurora
* Fully Managed, highly available with replication across 3 AZ
* Automatically scales to workloads with millions of requests per seconds

### Amazon Neptune

> Fully managed **graph** database

* A popular graph dataset would be a social network
  * Users have friends
  * Posts have comments
  * Comments have likes from users
  * Users share and like posts...
* Highly available across 3 AZ, with up to 15 read replicas
* Build and run applications working with highly connected datasets – optimized for these complex and hard queries
* Can store up to billions of relations and query the graph with milliseconds latency
* Highly available with replications across multiple AZs
* Great for knowledge graphs (Wikipedia), fraud detection, recommendation engines, social networking

### Amazon Managed Blockchain

* Blockchain makes it possible to build applications where multiple parties can execute transactions without the need for a trusted, central authority.
* Amazon Managed Blockchain is a managed service to:
  * Join public blockchain networks
  * Or create your own scalable private network
* Compatible with the frameworks Hyperledger Fabric & Ethereum

### Amazon QLDB

> QLDB stands for ”Quantum Ledger Database”

* A ledger is a book recording financial transactions
* Fully Managed, Serverless, Highavailable, Replication across 3AZ
* Used to review history of all the changes made to your application data over time
* Immutable system: no entry can be removed or modified, cryptographically verifiable
* 2-3x better performance than common ledger blockchain frameworks, manipulate data using SQL
* Difference with Amazon Managed Blockchain: no decentralization component, in accordance with financial regulation rules

### AWS Glue

* Managed extract, transform, and load (ETL) service
* Useful to prepare and transform data for analytics
* Fully serverless service

### DMS

> DMS: Database Migration Service

* Quickly and securely migrate databases to AWS, resilient, self healing
* The source database remains available during the migration
* Supports:
  * Homogeneous migrations: ex Oracle to Oracle
  * Heterogeneous migrations: ex Microsoft SQL Server to Aurora

## Other Compute Services

### ECS

> ECS: Elastic Container Service

* Launch Docker containers on AWS
* You **must** provision & maintain the infrastructure (the EC2 instances)
* AWS takes care of starting / stopping containers
* Has integrations with the Application Load Balancer

### Fargate

* You **do not** provision the infrastructure (no EC2 instances to manage) – simpler!
* Serverless offering
* AWS just runs containers for you based on the CPU / RAM you need

### ECR

> ECR: Elastic Container Registry

* Private Docker Registry on AWS
* This is where you store your Docker images so they can be run by ECS or Fargate

### AWS Lambda

* Easy Pricing:
  * Pay per request and compute time
  * Free tier of 1,000,000 AWS Lambda requests and 400,000 GBs of compute time
* Integrated with the whole AWS suite of services
* Event-Driven: functions get invoked by AWS when needed
* Integrated with many programming languages
* Easy monitoring through AWS CloudWatch
* Easy to get more resources per functions (up to 10GB of RAM!)
* Increasing RAM will also improve CPU and network!

### Amazon API Gateway

* Fully managed service for developers to easily create, publish, maintain, monitor, and secure APIs
* Serverless and scalable
* Suppor ts RESTful APIs and WebSocket APIs
* Suppor t for security, user authentication, API throttling, API keys, monitoring...

### AWS Batch

* Fully managed batch processing at any scale
* Efficiently run 100,000s of computing batch jobs on AWS
* A “batch” job is a job with a start and an end (opposed to continuous)
* Batch will dynamically launch EC2 instances or Spot Instances
* AWS Batch provisions the right amount of compute / memory
* You submit or schedule batch jobs and AWS Batch does the rest!
* Batch jobs are defined as Docker images and run on ECS
* Helpful for cost optimizations and focusing less on the infrastructure

### Batch VS Lambda

* Lambda:
  * Time limit
  * Limited runtimes
  * Limited temporary disk space
  * Serverless
* Batch:
  * No time limit
  * Any runtime as long as it’s packaged as a Docker image
  * Rely on EBS / instance store for disk space
  * Relies on EC2 (can be managed by AWS)

### Amazon Lightsail

* Virtual servers, storage, databases, and networking
* Low & predictable pricing
* Simpler alternative to using EC2, RDS, ELB, EBS, Route 53...
* Great for people with little cloud experience!
* Can setup notifications and monitoring of your Lightsail resources
* Use cases:
  * Simple web applications (has templates for LAMP, Nginx, MEAN, Node.js...)
  * Websites (templates for WordPress, Magento, Plesk, Joomla)
  * Dev /Test environment
* Has high availability but no auto-scaling, limited AWS integrations

## Deploying and Managing Infrastructure at Scale

### CloudFormation

> CloudFormation is a declarative way of outlining your AWS Infrastructure

* Infrastructure as code
  * No resources are manually created, which is excellent for control
  * Changes to the infrastructure are reviewed through code
* Cost
  * Each resources within the stack is tagged with an identifier so you can easily see how much a stack costs you
  * You can estimate the costs of your resources using the CloudFormation template
  * Savings strategy: In Dev, you could automation deletion of templates at 5 PM and recreated at 8 AM, safely
* Productivity
  * Ability to destroy and re-create an infrastructure on the cloud on the fly
  * Automated generation of Diagram for your templates!
  * Declarative programming (no need to figure out ordering and orchestration)
* Don’t re-invent the wheel
  * Leverage existing templates on the web!
  * Leverage the documentation
* Supports (almost) all AWS resources:
  * You can use “custom resources” for resources that are not supported

### AWS Cloud Development Kit (CDK)

* Define your cloud infrastructure using a familiar language:
  * JavaScript/TypeScript
  * Python
  * Java
  * .NET
* The code is “compiled” into a CloudFormation template (JSON/YAML)
* You can therefore deploy infrastructure and application runtime code together
* Great for Lambda functions
* Great for Docker containers in ECS / EKS

### AWS Elastic Beanstalk Overview

* Elastic Beanstalk is a developer centric view of deploying an application on AWS
* We still have full control over the configuration
* Platform as a Service (PaaS)
* Beanstalk is free but you pay for the underlying instances

### Elastic Beanstalk

* Managed service:
  * Instance configuration / OS is handled by Beanstalk
  * Deployment strategy is configurable but performed by Elastic Beanstalk • Capacity provisioning
  * Load balancing & auto-scaling
  * Application health-monitoring & responsiveness
* Just the application code is the responsibility of the developer
* Three architecture models:
  * Single Instance deployment: good for dev
  * LB + ASG: great for production or pre-production web applications
  * ASG only: great for non-web apps in production (workers, etc..)

### AWS CodeDeploy

* We want to deploy our application automatically
* Works with EC2 Instances
* Works with On-Premises Servers
* Hybrid service
* Servers / Instances must be provisioned and configured ahead of time with the CodeDeploy Agent

### AWS CodeCommit

* Source-control service that hosts Git-based repositories • Makes it easy to collaborate with others on code
* The code changes are automatically versioned
* Benefits:
  * Fully managed
  * Scalable & highly available
  * Private, Secured, Integrated with AWS

### AWS CodeBuild

* Code building service in the cloud
* Compiles source code, run tests, and produces packages that are ready to be deployed
* Fully managed, serverless
* Continuously scalable & highly available
* Secure
* Pay-as-you-go pricing – only pay for the build time

### AWS CodePipeline

* Orchestrate the different steps to have the code automatically pushed to production
  * Code => Build => Test => Provision => Deploy
  * Basis for CICD (Continuous Integration & Continuous Delivery)
* Benefits:
  * Fully managed, compatible with CodeCommit, CodeBuild, CodeDeploy, ElasticBeanstalk, CloudFormation, GitHub, 3rd-party services (GitHub...) & custom plugins...
  * Fast delivery & rapid updates

### AWS CodeArtifact

* CodeArtifact is a secure, scalable, and cost-effective artifact management for software development
* Works with common dependency management tools such as Maven, Gradle, npm, yarn, twine, pip, and NuGet
* Developers and CodeBuild can then retrieve dependencies straight from CodeArtifact

### AWS CodeStar

* Unified UI to easily manage software development activities in one place
* “Quick way” to get started to correctly set-up CodeCommit, CodePipeline, CodeBuild, CodeDeploy, Elastic Beanstalk, EC2, etc...
* Can edit the code ”in-the-cloud” using AWS Cloud9

### AWS Cloud9

* AWS Cloud9 is a cloud IDE (Integrated Development Environment) for writing, running and debugging code
* Allows for code collaboration in real-time (pair programming)

### AWS Systems Manager (SSM)

* Helps you manage your EC2 and On-Premises systems at scale
* Another Hybrid AWS service
* Get operational insights about the state of your infrastructure
* Suite of 10+ products
* Most important features are:
  * Patching automation for enhanced compliance
  * Run commands across an entire fleet of servers
  * Store parameter configuration with the SSM Parameter Store
  * Works for both Windows and Linux OS

### AWS OpsWorks

* Chef & Puppet help you perform server configuration automatically, or repetitive actions
* They work great with EC2 & On-PremisesVM
* AWS OpsWorks = Managed Chef & Puppet
* It’s an alternative to AWS SSM
* Only provision standard AWS resources: EC2 Instances, Databases, Load Balancers, EBS volumes...

## Global Applications

### Amazon Route 53 Overview

* Route53 is a **Managed DNS** (Domain Name System)
  * DNS is a collection of rules and records which helps clients understand how to reach a server through URLs
* Routing Policies:
  * SIMPLE ROUTING POLICY
  * WEIGHTED ROUTING POLICY
  * LATENCY ROUTING POLICY
  * FAILOVER ROUTING POLICY

### AWS CloudFront

* Content Delivery Network (CDN):
  * Improves read performance, content is cached at the edge
  * Improves users experience
* 216+ Point of Presence globally (edge locations)
* DDoS protection, integration with Shield, AWS Web Application Firewall
* Origins:
  * S3 bucket
    * For distributing files and caching them at the edge
    * Enhanced security with CloudFront Origin Access Identity (OAI)
    * CloudFront can be used as an ingress (to upload files to S3)
  * Custom Origin (HTTP)
    * Application Load Balancer
    * EC2 instance
    * S3 website (must first enable the bucket as a static S3 website)
    * Any HTTP backend you want

#### CloudFront vs S3 Cross Region Replication

* CloudFront:
  * Global Edge network
  * Files are cached for a TTL (maybe a day)
  * Great for static content that must be available everywhere •
* S3 Cross Region Replication:
  * Must be setup for each region you want replication to happen
  * Files are updated in near real-time
  * Read only
  * Great for dynamic content that needs to be available at low-latency in few regions

### S3 Transfer Acceleration

> Increase transfer speed by transferring file to an AWS edge location which will forward the data to the S3 bucket in the target region

### AWS Global Accelerator

* Improve global application availability and performance using the AWS global network
* Leverage the AWS internal network to optimize the route to your application (60% improvement)
* 2 Anycast IP are created for your application and traffic is sent through Edge Locations
* The Edge locations send the traffic to your application

#### AWS Global Accelerator vs CloudFront

* They both use the AWS global network and its edge locations around the world
* Both services integrate with AWS Shield for DDoS protection.
* CloudFront – Content Delivery Network
  * Improves performance for your cacheable content (such as images and videos)
  * Content is served at the edge
* Global Accelerator
  * No caching, proxying packets at the edge to applications running in one or more AWS Regions.
  * Improves performance for a wide range of applications over TCP or UDP
  * Good for HTTP use cases that require static IP addresses, deterministic, fast regional failover

### AWS Outposts

* Hybrid Cloud: businesses that keep an on-premises infrastructure alongside a cloud infrastructure
* Therefore, two ways of dealing with IT systems:
  * One for the AWS cloud (using the AWS console, CLI, and AWS APIs)
  * One for their on-premises infrastructure
* AWS Outposts are “server racks” that offers the same AWS infrastructure, services, APIs & tools to build your own applications on-premises just as in the cloud
* AWS will setup and manage “Outposts Racks” within your on-premises infrastructure and you can start leveraging AWS services on-premises
* You are responsible for the Outposts Rack physical security
* Benefits:
  * Low-latency access to on-premises systems
  * Local data processing
  * Data residency
  * Easier migration from on-premises to the cloud
  * Fully managed service

### AWS WaveLength

> WaveLength Zones are infrastructure deployments embedded within the telecommunications providers’ datacenters at the edge of the 5G networks

* Brings AWS services to the edge of the 5G networks (Example:EC2,EBS,VPC...)
* Ultra-low latency applications through 5G networks
* Traffic doesn’t leave the Communication Service Provider’s (CSP) network
* High-bandwidth and secure connection to the parent AWS Region
* No additional charges or service agreements
* Use cases:
  * Smart Cities
  * ML-assisted diagnostics
  * Connected Vehicles
  * Interactive Live Video Streams
  * AR/VR
  * Real-time Gaming
  * ...

### AWS Local Zones

* Places AWS compute, storage, database, and other selected AWS services closer to end users to run latency-sensitive applications
* Extend your VPC to more locations – “Extension of an AWS Region”
* Compatible with EC2, RDS, ECS, EBS, ElastiCache, Direct Connect ...

## Cloud Integration

### Amazon SQS – Standard Queue

* Oldest AWS offering (over 10 years old)
* Fully managed service (~serverless), use to decouple applications
* Scales from 1 message per second to 10,000s per second
* Default retention of messages: 4 days, maximum of 14 days
* No limit to how many messages can be in the queue
* Messages are deleted after they’re read by consumers
* Low latency (<10 ms on publish and receive)
* Consumers share the work to read messages & scale horizontally

### Amazon Kinesis

> Kinesis = real-time big data streaming

* Managed service to collect, process, and analyze real-time streaming data at any scale
* `Kinesis Data Streams`: low latency streaming to ingest data at scale from hundreds of thousands of sources
* `Kinesis Data Firehose`: load streams into S3, Redshift, ElasticSearch, etc...
* `Kinesis Data Analytics`: perform real-time analytics on streams using SQL
* `Kinesis Video Streams`: monitor real-time video streams for analytics or ML

### Amazon SNS

* The “event publishers” only sends message to one SNS topic
* As many “event subscribers” as we want to listen to the SNS topic notifications
* Each subscriber to the topic will get all the messages
* Up to 12,500,000 subscriptions per topic, 100,000 topics limit

### Amazon MQ

> Amazon MQ: managed Apache ActiveMQ

* SQS, SNS are “cloud-native” services, and they’re using proprietary protocols from AWS.
* Traditional applications running from on-premise may use open protocols such as:MQTT,AMQP,STOMP,Openwire,WSS
* When migrating to the cloud, instead of re-engineering the application to use SQS and SNS, we can use Amazon MQ
* Amazon MQ doesn’t “scale” as much as SQS / SNS
* Amazon MQ runs on a dedicated machine (not serverless)
* Amazon MQ has both queue feature (~SQS) and topic features (~SNS)

## Cloud Monitoring

### Amazon CloudWatch Metrics

* CloudWatch provides metrics for every services in AWS
* Metric is a variable to monitor (CPUUtilization, NetworkIn...)
* Metrics have timestamps
* Can create CloudWatch dashboards of metrics

### Amazon CloudWatch Alarms

* Alarms are used to trigger notifications for any metric
* Alarms actions:
  * Auto Scaling: increase or decrease EC2 instances “desired” count
  * EC2 Actions: stop, terminate, reboot or recover an EC2 instance
  * SNS notifications: send a notification into an SNS topic
* Various options (sampling, %, max, min, etc...)
* Can choose the period on which to evaluate an alarm
* Example: create a billing alarm on the CloudWatch Billing metric
* Alarm States: OK. INSUFFICIENT_DATA, ALARM

### Amazon CloudWatch Events

* Schedule: Cron jobs (scheduled scripts)
* Event Pattern: Event rules to react to a service doing something
* Trigger Lambda functions, send SQS/SNS messages...

### Amazon EventBridge

* EventBridge is the next evolution of CloudWatch Events
* Default event bus: generated by AWS services (CloudWatch Events)
* Partner event bus: receive events from SaaS service or applications (Zendesk, DataDog, Segment, Auth0...)
* Custom Event buses: for your own applications
* Schema Registry: model event schema
* EventBridge has a different name to mark the new capabilities
* The CloudWatch Events name will be replaced with EventBridge

### AWS CloudTrail

* Provides governance, compliance and audit for your AWS Account
* CloudTrail is enabled by default
* Get an history of events / API calls made within your AWS Account by:
  * Console
  * SDK
  * CLI
  * AWS Services
* Can put logs from CloudTrail into CloudWatch Logs or S3
* A trail can be applied to All Regions (default) or a single Region.
* If a resource is deleted in AWS, investigate CloudTrail first!

#### CloudTrail Events

* Management Events:
  * Operations that are performed on resources in your AWS account
  * Examples:
    * Configuring security (IAM AttachRolePolicy)
    * Configuring rules for routing data (Amazon EC2 CreateSubnet)
    * Setting up logging (AWS CloudTrail CreateTrail)
  * By default, trails are configured to log management events.
  * Can separate Read Events (that don’t modify resources) from Write Events (that may modify resources)
* Data Events:
  * By default, data events are not logged (because high volume operations)
  * Amazon S3 object-level activity (ex: GetObject, DeleteObject, PutObject): can separate Read and Write Events
  * AWS Lambda function execution activity (the Invoke API)

#### CloudTrail Insights

* Enable CloudTrail Insights to detect unusual activity in your account:
  * inaccurate resource provisioning
  * hitting service limits
  * Bursts of AWS IAM actions
  * Gaps in periodic maintenance activity
* CloudTrail Insights analyzes normal management events to create a baseline
* And then continuously analyzes write events to detect unusual patterns
  * Anomalies appear in the CloudTrail console
  * Event is sent to Amazon S3
  * An EventBridge event is generated (for automation needs)

#### CloudTrail Events Retention

* Events are stored for 90 days in CloudTrail
* To keep events beyond this period, log them to S3 and use Athena

### AWS X-Ray

* Troubleshooting performance (bottlenecks)
* Understand dependencies in a microservice architecture
* Pinpoint service issues
* Review request behavior
* Find errors and exceptions
* Are we meeting time SLA?
* Where I am throttled?
* Identify users that are impacted

### Amazon CodeGuru

* An ML-powered service for automated code reviews and application performance recommendations
* Provides two functionalities
  * `CodeGuru Reviewer`: automated code reviews for static code analysis (development)
  * `CodeGuru Profiler`: visibility/recommendations about application performance during runtime (production)

### AWS Status - Service Health Dashboard

* Shows all regions, all services health
* Shows historical information for each day
* Has an RSS feed you can subscribe to

### AWS Personal Health Dashboard

* AWS Personal Health Dashboard provides alerts and remediation guidance when AWS is experiencing events that may impact you.
* While the Service Health Dashboard displays the general status of AWS services, Personal Health Dashboard gives you a personalized view into the performance and availability of the AWS services underlying your AWS resources.
* The dashboard displays relevant and timely information to help you manage events in progress and provides proactive notification to help you plan for scheduled activities.

## VPC

### VPC & Subnets Primer

* VPC -Virtual Private Cloud: private network to deploy your resources (regional resource)
* Subnets allow you to partition your network inside your VPC (Availability Zone resource)
* A public subnet is a subnet that is accessible from the internet
* A private subnet is a subnet that is not accessible from the internet
* To define access to the internet and between subnets, we use Route Tables.

### Internet Gateway & NAT Gateways

* Internet Gateways helps our VPC instances connect with the internet
* Public Subnets have a route to the internet gateway.
* NAT Gateways (AWS-managed) & NAT Instances (self-managed) allow your instances in your Private Subnets to access the internet while remaining private

### Network ACL & Security Groups

* NACL (Network ACL)
  * A firewall which controls traffic from and to subnet
  * Can have ALLOW and DENY rules
  * Are attached at the Subnet level
  * Rules only include IP addresses
* Security Groups
  * A firewall that controls traffic to and from an ENI / an EC2 Instance
  * Can have only ALLOW rules
  * Rules include IP addresses and other security groups

### VPC Flow Logs

* Capture information about IP traffic going into your interfaces:
  * VPC Flow Logs
  * Subnet Flow Logs
  * Elastic Network Interface Flow Logs
* Helps to monitor & troubleshoot connectivity issues.
* Example:
  * Subnets to internet
  * Subnets to subnets
  * Internet to subnets
* Captures network information from AWS managed interfaces too: Elastic Load Balancers, ElastiCache, RDS, Aurora, etc...
* VPC Flow logs data can go to S3 / CloudWatch Logs

### VPC Peering

* Connect two VPC, privately using AWS’ network
* Make them behave as if they were in the same network
* Must not have overlapping CIDR (IP address range)
* VPC Peering connection is not transitive (must be established for each VPC that need to communicate with one another)

### VPC Endpoints

* Endpoints allow you to connect to AWS Services using a private network instead of the public www network
* This gives you enhanced security and lower latency to access AWS services
* VPC Endpoint Gateway: S3 & DynamoDB
* VPC Endpoint Interface: the rest

### Site to Site VPN & Direct Connect

* Site to Site VPN
  * Connect an on-premises VPN to AWS
  * The connection is automatically encrypted
  * Goes over the public internet
  * On-premises: must use a Customer Gateway (`CGW`)
  * AWS: must use a Virtual Private Gateway (`VGW`)
* Direct Connect (DX)
  * Establish a physical connection between on-premises and AWS
  * The connection is private, secure and fast
  * Goes over a private network
  * Takes at least a month to establish

### Transit Gateway

* For having transitive peering between thousands of VPC and on-premises, hub-and-spoke (star) connection
* One single Gateway to provide this functionality
* Works with Direct Connect Gateway,VPN connections

## Security & Compliance

### AWS Shared Responsibility Model

* AWS responsibility - Security **of** the Cloud
  * Protecting infrastructure (hardware, software, facilities, and networking) that runs all the AWS services
  * Managed services like S3, DynamoDB, RDS, etc.
* Customer responsibility - Security **in** the Cloud
  * For EC2 instance, customer is responsible for management of the guest OS (including security patches and updates), firewall & network configuration, IAM
  * Encrypting application data
* Shared controls:
  * Patch Management, Configuration Management, Awareness & Training

### DDOS Protection on AWS

* AWS Shield Standard: protects against DDOS attack for your website and applications, for all customers at no additional costs
* AWS Shield Advanced: 24/7 premium DDoS protection
* AWS WAF: Filter specific requests based on rules
* CloudFront and Route 53:
  * Availability protection using global edge network
  * Combined with AWS Shield, provides attack mitigation at the edge

### AWS WAF – Web Application Firewall

* Protects your web applications from common web exploits (Layer 7)
  * Layer 7 is HTTP (vs Layer 4 is TCP)
* Deploy on Application Load Balancer, API Gateway, CloudFront
* Define Web ACL (Web Access Control List):
  * Rules can include IP addresses, HTTP headers, HTTP body, or URI strings
  * Protects from common attack - SQL injection and Cross-Site Scripting (XSS)
  * Size constraints, geo-match (block countries)
  * Rate-based rules (to count occurrences of events) – for DDoS protection

### AWS KMS (Key Management Service)

> KMS = AWS manages the encryption keys for us

* Anytime you hear “encryption” for an AWS service, it’s most likely KMS
* Encryption Opt-in:
  * EBS volumes: encrypt volumes
  * S3 buckets: Server-side encryption of objects
  * Redshift database: encryption of data
  * RDS database: encryption of data
  * EFS drives: encryption of data
* Encryption Automatically enabled:
  * CloudTrail Logs
  * S3 Glacier
  * Storage Gateway

### CloudHSM

> KMS => AWS manages the software for encryption  
> CloudHSM => AWS provisions encryption hardware  

* Dedicated Hardware (HSM = Hardware Security Module)
* You manage your own encryption keys entirely (not AWS)
* HSM device is tamper resistant, FIPS 140-2 Level 3 compliance

### AWS Certificate Manager (ACM)

* easily provision, manage, and deploy SSL/TLS Certificates
* Used to provide in-flight encryption for websites (HTTPS)
* Supports both public and privateTLS certificates
* Free of charge for publicTLS certificates
* AutomaticTLS certificate renewal
* Integrations with (loadTLS certificates on)
  * Elastic Load Balancers
  * CloudFront Distributions
  * APIs on API Gateway

### AWS Secrets Manager

* Newer service, meant for storing secrets
* Capability to force rotation of secrets every X days
* Automate generation of secrets on rotation (uses Lambda)
* Integration with Amazon RDS (MySQL, PostgreSQL, Aurora)
* Secrets are encrypted using KMS

### Amazon Inspector

* Automated Security Assessments
* For EC2 instances
  * Leveraging the AWS System Manager (SSM) agent
  * Analyze against unintended network accessibility
  * Analyze the running OS against known vulnerabilities
* For Containers push to Amazon ECR
  * Assessment of containers as they are pushed
* Reporting & integration with AWS Security Hub
* Send findings to Amazon Event Bridge
* only evaluate for EC2 instances and container infrastructure

### AWS Config

* Helps with auditing and recording compliance of your AWS resources
* Helps record configurations and changes over time
* Possibility of storing the configuration data into S3 (analyzed by Athena)
* Questions that can be solved by AWS Config:
  * Is there unrestricted SSH access to my security groups?
  * Do my buckets have any public access?
  * How has my ALB configuration changed over time?
* You can receive alerts (SNS notifications) for any changes
* AWS Config is a per-region service
* Can be aggregated across regions and accounts

### Amazon Macie

* Amazon Macie is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover and protect your sensitive data in AWS.
* Macie helps identify and alert you to sensitive data, such as personally identifiable information (PII)

### Amazon Detective

* Amazon Detective analyzes, investigates, and quickly identifies the root cause of security issues or suspicious activities (using ML and graphs)
* Automatically collects and processes events from VPC Flow Logs, CloudTrail, GuardDuty and create a unified view
* Produces visualizations with details and context to get to the root cause

### AWS Abuse

* Report suspected AWS resources used for abusive or illegal purposes
* Abusive & prohibited behaviors are:
  * Spam – receving undesired emails from AWS-owned IP address, websites & forums spammed by AWS resources
  * Port scanning – sending packets to your ports to discover the unsecured ones
  * DoS or DDoS attacks – AWS-owned IP addresses attempting to overwhlem or crash your servers/softwares
  * Intrusion attempts – logging in on your resources
  * Hosting objectionable or copyrighted content – distributing illegal or copyrighted content without consent
  * Distributing malware – AWS resources distributing softwares to harm computers or machines

### Root user privileges

> Root user = Account Owner (created when the account is created)

* Has complete access to all AWS services and resources
* Lock away your AWS account root user access keys!
* Do not use the root account for everyday tasks, even administrative tasks
* Actions that can be performed only by the root user:
  * Change account settings(account name, email address, rootuser password, rootuser accesskeys)
  * View certain tax invoices
  * Close your AWS account
  * Restore IAM user permissions
  * Change or cancel your AWS Support plan
  * Register as a seller in the Reserved Instance Marketplace
  * Configure an Amazon S3 bucket to enable MFA
  * Editor delete an Amazon S3 bucket policy that includes an invalid VPC ID or VPC endpoint ID
  * Sign up for GovCloud

## Machine Learning

### Amazon Rekognition

* Find objects, people, text, scenes in images and videos using ML
* Facial analysis and facial search to do user verification, people counting
* Create a database of “familiar faces” or compare against celebrities
* Use cases:
  * Labeling
  * Content Moderation
  * Text Detection
  * Face Detection and Analysis (gender, age range, emotions...)
  * Face Search and Verification
  * Celebrity Recognition
  * Pathing

### Amazon Transcribe

* Automatically convert speech to text
* Uses a deep learning process called automatic speech recognition (ASR) to convert speech to text quickly and accurately
* Use cases:
  * transcribe customer service calls
  * automate closed captioning and subtitling
  * generate metadata for media assets to create a fully searchable archive

### Amazon Polly

* Turn text into lifelike speech using deep learning
* Allowing you to create applications that talk

### Amazon Translate

* Natural and accurate language translation
* Amazon Translate allows you to localize content for international users, and to easily translate large volumes of text efficiently.

### Amazon Lex & Connect

* Amazon Lex: (same technology that powers Alexa)
  * Automatic Speech Recognition (ASR) to convert speech to text
  * Natural Language Understanding to recognize the intent of text, callers
  * Helps build chatbots, call center bots
* Amazon Connect:
  * Receive calls, create contact flows, cloud-based vir tual contact center
  * Can integrate with other CRM systems or AWS
  * No upfront payments, 80% cheaper than traditional contact center solutions

### Amazon Comprehend

* For Natural Language Processing – NLP
* Fully managed and serverless service
* Uses machine learning to find insights and relationships in text
  * Language of the text
  * Extracts key phrases, places, people, brands, or events
  * Understands how positive or negative the text is
  * Analyzes text using tokenization and parts of speech
  * Automatically organizes a collection of text files by topic
* Sample use cases:
  * analyze customer interactions (emails) to find what leads to a positive or negative experience
  * Create and groups articles by topics that Comprehend will uncover

### Amazon SageMaker

* Fully managed service for developers / data scientists to build ML models
* Typically, difficult to do all the processes in one place + provision servers
* Machine learning process (simplified): predicting your exam score

### Amazon Forecast

* Fully managed service that uses ML to deliver highly accurate forecasts
* Example: predict the future sales of a raincoat
* 50% more accurate than looking at the data itself
* Reduce forecasting time from months to hours
* Use cases: Product Demand Planning, Financial Planning, Resource Planning, ...

### Amazon Kendra

* Fully managed document search service powered by Machine Learning
* Extract answers from within a document (text, pdf, HTML, PowerPoint, MS Word, FAQs...)
* Natural language search capabilities
* Learn from user interactions/feedback to promote preferred results (Incremental Learning)
* Ability to manually fine-tune search results (importance of data, freshness, custom, ...)

### Amazon Personalize

* Fully managed ML-service to build apps with real-time personalized recommendations
* Same technology used by Amazon.com
* Integrates into existing websites, applications, SMS, email marketing systems, ...
* Implement in days, not months (you don’t need to build, train, and deploy ML solutions)
* Use cases: retail stores, media and entertainment...

### AmazonTextract

* Automatically extracts text, handwriting, and data from any scanned documents using AI and ML
* Extract data from forms and tables
* Read and process any type of document (PDFs, images, ...)
* Use cases:
  * Financial Services (e.g., invoices, financial reports)
  * Healthcare (e.g., medical records, insurance claims)
  * Public Sector (e.g., tax forms, ID documents, passports)

## Account Management, Billing & Support

### AWS Organizations

* Global service
* Allows to manage multiple AWS accounts
* The main account is the master account
* Cost Benefits:
  * Consolidated Billing across all accounts - single payment method
  * Pricing benefits from aggregated usage (volume discount for EC2, S3...)
  * Pooling of Reserved EC2 instances for optimal savings
* API is available to automate AWS account creation
* Restrict account privileges using Service Control Policies (SCP)

### Service Control Policies (SCP)

* Whitelist or blacklist IAM actions
* Applied at the OU(Organization Unit) or Account level
* Does not apply to the Master Account
* SCP is applied to all the Users and Roles of the Account, including Root user
* The SCP does not affect service-linked roles
* Service-linked roles enable other AWS services to integrate with AWS Organizations and can't be restricted by SCPs.
* SCP must have an explicit Allow (does not allow anything by default)
* Use cases:
  * Restrict access to certain services (for example: can’t use EMR)
  * Enforce PCI compliance by explicitly disabling services

### AWS Control Tower

* Easy way to set up and govern a secure and compliant multi-account AWS environment based on best practices
* Benefits:
  * Automate the set up of your environment in a few clicks
  * Automate ongoing policy management using guardrails
  * Detect policy violations and remediate them
  * Monitor compliance through an interactive dashboard
* AWS Control Tower runs on top of AWS Organizations:
  * It automatically sets up AWS Organizations to organize accounts and implement SCPs (Service Control Policies)

### Pricing Models in AWS

* AWS has 4 pricing models:
  * `Pay as you go`: pay for what you use, remain agile, responsive, meet scale demands
  * `Save when you reserve`: minimize risks, predictably manage budgets, comply with long-terms requirements
    * Reservations are available for EC2 Reserved Instances, DynamoDB Reserved Capacity, ElastiCache Reserved Nodes, RDS Reserved Instance, Redshift Reserved Nodes
  * `Pay less by using more`: volume-based discounts
  * `Pay less as AWS grows`

### Billing and Costing Tools

* Estimating costs in the cloud:
  * Pricing Calculator
* Tracking costs in the cloud:
  * Billing Dashboard
  * Cost Allocation Tags
  * Cost and Usage Reports
  * Cost Explorer
* Monitoring against costs plans:
  * Billing Alarms
  * Budgets

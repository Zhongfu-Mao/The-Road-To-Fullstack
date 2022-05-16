# IBM Cloud Essentials

## Introduction to IBM Cloud

### Locations and Regions

* 6 regions
  * Dallas(us-south)
  * WashingtonDC(us-east)
  * London(eu-gb)
  * Frankfurt(eu-de)
  * Tokyo(jp-tok)
  * Sydney(au-syd)
* 18 availablity zones
* 60 data centers

* Single Zone Cluster
* Multizone regions(>=3)

Locations:

* North America West
* North America South
* North America East
* South America
* Europe
* Asia Pacific

Locations organize: Geograph -> Country -> Metro -> Data Center(Zone)

### Account Types and Support Plans

IBM Cloud has three types of accounts:

* Lite
  * Access to over 40 Lite services
  * No credit card required
  * Never expires
* Pay-as-you-go
  * Access to all IBM Cloud services
  * IBM support
  * Fit for production use cases
* Subscription
  * Discounted pricing
  * Available for enterprises
  * Access to all IBM Cloud services

Three support levels:

* Basic
* Advanced
* Premium

### Billing and Usage

* Monthly overview
* By service
* Export usage as a CSV

### Identity and Access Management(IAM)

#### IAM components

In IBM Cloud IAM has four key components:

* Users
  * Invited to join accounts
  * API key support for authentication
  * IAM roles and access are associated with a user
  * Platform Roles:
    * Viewer
    * Operator
    * Editor
    * Administrator
* Access Groups
  * Collection of users
  * Allows for cleaner separation of control
  * User can be part of multiple access groups
* Resources
  * A service is an entity in the catalog while a resource is a provisioned service.
  * Have an auto-generated service ID when created
  * User can select a region to create the resource
  * Service Roles dictate permissions for the service's APIs
  * Service Roles:
    * Reader
    * Writer
    * Manager
* Resource Groups
  * Collection of resources
  * Specified at service creation time
  * No geographic restrictions

#### Access Policy

> The combination of a subject(Users and Access Groups), role(Service Roles), and target(Resources and Resource Groups)

## Infrastructure

### Virtual Servers

Virtual Server Offerings:

* Virtual Server
  * Regions
  * Types
    * Public
    * Dedicated
    * Transient
    * Reserved
  * Images
    * CentOS
    * Debian
    * Microsoft Windows
    * Red Hat Enterprise Linux
    * Ubuntu
  * Up to 64 vCPUs, 2 GPUs, and 512GB of RAM
  * Up to 1 Gbps network and 5 SAN volumes
* Bare metal
  * Regions
  * Billing
    * Hourly
    * Monthly
    * 1-year contract
    * 3-year contract
  * Images
    * VMware
    * Citrix
    * Cloud Linux
    * No OS
    * Images from Virturl Server
  * VMware and SAP certified
  * 4 to 72 cores
  * UP to 6 TB RAM and 36 drivers
  * GPU support
* Power Systems
  * Regions
    * Europe
    * North America South
    * North America East
  * Machine Types
    * e880
    * s922
  * Images
    * AIX
    * IBM i
    * Bring your own Linux
* Hyper Protect(Z)
  * Regions
    * North America South
    * Europe
    * North America East
    * Asia Pacific
  * Linux One
  * Secure
  * Easy to deploy
  * No Z skills required

### Block and File Storage

Related services:

* Block storage
* File storage
* Cloud backup
  * Customizable(daily/weekly, OS/directory)
  * Management Portal - One click restores
  * Plug-ins for MS-SQL, MS SharePoint, Oracle
  * End-to-end Encryption
  * Geo-redundancy

Block and File storage common points:

* 20GB to 12TB
* Encryption
* Up to 48k IOPs
* Global footprint
* Snapshot and replication

### Object Storage

> A highly scalable cloud storage, designed for durablity, resiliency and security.

* Access Management
* Encryption
* SQL query support
* High-speed transfer
* SDKs and APIs

### Network Services

#### Cloud Internet Services

> IBM Cloud's Cloud Internet Services(CIS) uses Cloudflare for internet facing applications.

* Domain Name Service(DNS)
* Transport Layer Security(TLS)
* Global Load Balancing(GLB)
* Rate Limiting
* DDoS Protection
* Smart Routing
* Web Application Firewall(WAF)
* Caching

#### Networking Infrastructure

* Direct Link: Create a direct, private connection between remote networks and IBM Cloud
  * Secure Connectivity
  * Fully Integrated Hybrid Environment
  * Speed(50Mbps-5Gbps)
* CDN: A highly-distributed platform of servers that helps minimize delays
  * Based on Akamai
  * Smarter Scaling
  * Secure
  * Optimize Dynamic Content
  * Usage-based pricing
* Load Balancer: Distribute traffic between virtual machines
  * Layer-4(TCP) and Layer-7(HTTP, HTTPS)
  * Public and Private
  * Server Health Checks
  * SSL Offload
  * Monitoring Metrics
* Gateway Appliance
* Firewall
* VPN
* Subnets & IPs
* VLAN

### Virtual Private Cloud

> A secure, isolated private cloud hosted within a public cloud.

* Configurable pool of shared computing resources
* Isolation between users
* Authenticates users and controls access to resources

#### Key Components of VPC

* Multizone Region(location)
* Multiple Subnets(IP Addresses)
* Security groups
* Virtual server instances
* Public & VPN Gateway
* Block storage volumes

#### Differences between Gen1 and Gen2 VPC

Gen 1:

* Available in 6 regions
* Up to 16 Gbps networking
* Provider managed security or BYOK

Gen 2:

* Available in 5 regions
* Up to 80 Gbps networking
* Provider managed security only

### VMware Solution

Why use VMware on a cloud platform?

* Cloud economies
* Scalability & elasticity
* Highly available

#### VMware Solution Dedicated

> Bare metal solution with vCenter and vSphere options

* Customer has access to the hypervisor
* vCenter(fully automated, VMware based software defined data center)
* vSphere(manually configure networking, storage, and add-ons)
* Bring your own license(BYOL)
* Add-on services(Veeam, Zerto)

#### VMware Solution Shared

> Managed deployment of vCloud Director

* IBM manages the hypervisor
* Cost-effective
* Perfect for temporary migration, burst
* Disaster Recovery
* Self-service

#### Benefits of VMware on IBM Cloud

* Security(Encryption+Access Control)
* Compliance(Geo-fencing workloads)
* Expertise
* Repid set up

#### VMware on IBM Cloud: Optional Services

* Veeam
* Zerto
* F5 BIG IP

## Deploying Applications

### Containers and Kubernetes

#### Containers

> Packaging up code, runtimes, and dependencies

* Concept around since 80s
* Various runtimes
* OCI specification
* Image registry

#### Kubernetes

> Open-source, container-based, distributed, and scalable container-orchestration system

* Open source
* Automated rollouts
* Automatic scaling of services
* Service health monitoring
* Deploy anywhere

#### IBM Cloud Kubernetes Service(IKS)

> Production-grade container-orchestration system

* Fully managed environment with upgrades
* Secure clusters(PCI, HIPAA-ready, SOC1 and more)
* Single and multi-zone configurations
* Supported add-ons
* Logging and monitoring

Regions and Configurations:

* Regions
* Types
  * Virtual Shared
  * Virtual Dedicated
  * Bare metal
* Profiles
  * 2vCPU, 4GB RAM - 64vCPU, 512GB RAM
  * 2vCPU, 4GB RAM - 56vCPU, 242GB RAM
  * 4 Cores, 32GB RAM - 28 Cores, 512GB RAM
* Billing
  * Hourly
  * Monthly
  * Free

Container Related Services on IBM Cloud:

* Container Registry
  * Highly available
  * Public & private
  * Vulnerability advisor
* Helm Catalog
  * Access IBM products
  * Open source projects
  * Multi-arch support

#### Kubernetes on IBM Cloud

```shell
ibmcloud login

ibmcloud target -r <name>

ibmcloud target -g <rg-name>

ibmcloud cr images

ibmcloud ks

kubectl
```

### OpenShift

#### Red Hat OpenShift

* Open source(OKD)
* Extend Kubernetes
* Deployable on-premises or in a cloud
* Enhanced security from RHEL

#### OpenShift vs Kubernetes

* Kubernetes:
  * quarterly minor releases
  * core framework
  * platform is responsible to integrate beyond core
* OpenShift:
  * quarterly releases
  * k8s core plus abstractions
  * opinions and integration of common features

#### How does OpenShift extend Kubernetes

* Integrated container registry
* Powerful integrated console
* Access control and projects
* Easier developer flows with Source to Image and Routes

#### Red Hat OpenShift on IBM Cloud(ROKS)

* Automated upgrades and patching
* Secure clusters(PCI, HIPAA-ready, SOC1 and more)
* Single and multi-zone configurations
* Integrated with LogDNA and SysDig

#### ROKS Regions and Configurations

* Regions
* Types
  * Virtual Shared
  * Virtual Dedicated
  * Bare metal
* Profiles
  * 2vCPU, 4GB RAM - 64vCPU, 512GB RAM
  * 2vCPU, 4GB RAM - 56vCPU, 242GB RAM
  * 4 Cores, 32GB RAM - 28 Cores, 512GB RAM
* Billing
  * Hourly
  * Monthly

!!! tip

    no free tier!

#### What's new in OpenShift 4

* Operator Framework
* OpenShift Service Mesh
* OpenShift serverless computing
* OpenShift pipelines
* CodeReady Workspaces

#### Ways to try OpenShift

* IBM Cloud
* IBM Z
* IBM Power
* Amazon Web Services
* Microsoft Azure
* Google Cloud Platform
* Red Hat OpenStack
* Red Hat Virtualization
* OpenShift Playground
* CodeReady Containers
* VMware vSphere
* Bare metal

### Cloud Foundry

> Cloud Foundry is a PaaS that allows developers to build, deploy, and manage applications on the cloud.

* Open source
* Deployment automation
* Flexible infrastructure
* Commercial options
* Community support

#### Deploy with Cloud Foundry on IBM Cloud

* Continuous delivery service
* Application level console
* Bind IBM Cloud Services

#### Benefits of Cloud Foundry on IBM Cloud

* Access control
* Health management
* Automatic Routing
* Lite tier

#### Cloud Foundry runtimes on IBM Cloud

* Java
* Node.js
* Python
* Go
* Swift
* PHP
* ASP.NET Core
* Tomcat
* Ruby

### Cloud Functions

#### What is Serverless

* No server or resource management
* Focus on microservices
* Pay only for code execution

#### Comparing Compute Options

`Bare Metal(Best performance and control)` - `Virtual Server(Leverae existing languages & tools)` - `Containers(Maximux protability)` - `PaaS(Mix of developer speed and control)` - `Serverless(Maximum developer speed)`

<- control                                                                                          development speed->

#### IBM Cloud Functions

> IBM Cloud + Apache OpenWhisk

* Integrated API Gateway
* OpenAPI support(Swagger)
* Integrate with Watson APIs
* 5M free executions per month
* Logging and monitoring

#### Actions, Triggers, and Sequences

* Actions contain code performing the work
* Triggers receive events and invoke actions
* Sequences invoke actions in a linear order

#### Use cases

* Serverless APIs
* Extract-Transform-Load(ETL)
* Alarm driven

#### Cloud Functions runtimes

* Java
* Node.js
* Python
* Go
* Swift
* PHP
* ASP.NET Core
* Ruby
* Containers

## Services on IBM Cloud

### Databases

#### DBaaS

> Database as a Service

* Cost-effective management
* Secure, available, and scalable
* Faster time to market

#### Relational databases on IBM Cloud

* Db2
  * Fully managed Db2
  * Scalable and elastic
* Db2 Hosted
  * Managed Db2, with admin access
  * Mirror on-prem Db2
* Postgres
  * Robust open source database
  * Integrates with IBM services

#### Document databases on IBM Cloud

* MongoDB
  * Flexible data model
  * Compliance support
* Cloudant
  * 99.99% SLA
  * Based on Apache CouchDB
* Elasticsearch
  * full-text search capabilities
  * Data encrypted at rest

#### Key-value databases on IBM Cloud

* Redis
  * Open source in-memory data store
  * Used as database, cache, message broker
* etcd
  * Open source obect-relational database
  * Emphasis on flexibility

### Integration

#### What is Integration

Provides:

* Connectivity
* Routing
* Transformation

Enables:

* Sharing data
* Connecting applications
* Security

#### Integration on IBM Cloud

* API Connect
  * Generate Swagger APIs
  * Graphically assemble API
  * Share APIs with self-service portal
  * API analytics
* App Connect
  * Automate your workflow
  * Integrate with 75+ connectors
  * Use templates to get started
  * Expose flows as REST APIs
* Event Stream
  * Fully managed Kafka Service
  * Highly Available
  * Intuitive User Experience
  * Event-driven architecture
* MQ
  * Fully managed Message service
  * Extend messaging to the cloud
  * IBM cloud and AWS compatibility
  * Use MQ Explorer or Console

### Artifical Intelligence

#### Data Science

> A method for creating insights from data using anlytics and machine learning

* Many use cases from all industries
* 80% of a data scientists' time finding, cleaning and organizing data
* Build models that can predict and forecast

#### What is Artificial Intelligence

* Machine learning
* Natural language processing
* Speech recognition
* Vision
* Robotics
* Planning & Optimization

#### AI Frameworks

* TensorFlow
* scikit-learn
* PyTorch

#### AI service on IBM Cloud

* Watson Studio: Build run and manage AI models
* Machine Learning: Run and deploy models
* Watson OpenScale: Monitor AI models
* Knowledge Catalog: Categorize and share data and models
* Natural Language Understanding
* Tone Analyzer
* Discovery
* Knowledge Studio
* Speech to Text
* Text to Speech
* Language Translator
* Watson Assistant

### Analytics

#### What is Data Analytics

> The science of analyzing raw data in order to make conclusions about that information

* Planning
* Descriptive
* Diagnostic
* Predictive
* Prescriptive

#### Analytics service on IBM Cloud

* Analytics Engine
  * Spark and Hadoop
  * Scalability
  * HIPAA-ready
  * Customizable Environment
* Streaming Analytics
  * Support for text, video, audio...
  * Real-time analysis
  * Integrates with Spark and Hadoop
  * Built-in domain analytics
* Db2 Warehouse
  * Train ML models
  * Highly scalable
  * Secure
  * Oracle compatible
* Cognos Dashboard
  * Create visualizations
  * Live connection to data
  * Embed visualizations
  * Explore data
* Information Server
  * Extract, Transform, and Load with DataStage
  * Data lineage with Information Gov. Catalog
  * Data profiling with Information Analyzer

### DevOps

#### What is DevOps

> A set of practice that combine software development and IT operations to shorten the development lifecycle and provide high quality software

#### Integration vs delivery vs deployment

`git push` -> Continuous Integration(`Code Repo -> Build -> Test`) -> Continus Delivery(``Staging`) -> Continuous Deployment(`Production`)

#### IBM Cloud DevOps services

> A set of tools that support development, deployment, delivery, and operations tasks

* Toolchain
  * Code
    * GitLab CE
    * GitHub
    * Bitbucket
  * Deliver
    * Helm
    * Razee
    * Tekton
  * Run
    * Cloud Foundry
    * Kubernetes
    * Virtual Server
  * Learn
    * New Relic
    * Google Analytics
    * Sauce Labs
  * Culture
    * Slack
    * PagerDuty
    * Jira
* Continuous Delivery
* Delivery Pipeline

### Blockchain

#### What is Blockchain

> A permanent, growing list of records, called blocks, linked using cryptography

#### Elements of a blockchain

> Blockchains are distributed, permanent, and record transaction between two parties

* Distributed
* Immutable
* Smart Contracts

#### What is Hyperledger Fabric

* Framework to build blockchain apps
* Contracts, consensus, confidentiality, resiliency, scalability
* Supported by AWS, Azure, GCP, IBM, Oracle
* Open source, hosted by Linux Foundation

#### Consensus

> How nodes agree on order of transaction

* Proof of work, proof of stake, Raft
* Fix any nodes in error, and malicious nodes
* Assumes majority of the nodes are trustworthy

#### Value of blockchain

* Shared source of truth
* Automated transactions with smart contracts
* Visibility into history of an asset

#### IBM Blockchain Platform

* Advanced tooling
* Open technology
* Deploy anywhere

### Internet of Things

#### What is IoT

> Internet of things(IoT) is a system of interrelated computing devices, that transfers data over a network without requiring human interaction

#### IoT Use Cases

* Predictive Maintenance
* Asset Tracking
* Connected Vehicles

#### IBM Cloud Internet of Things Platform

* Connect and register devices
* information management
* Real-time analysis
* Risk and security management

### Cloud Paks

#### What are Cloud Paks

> Containerized software solutions built to run anywhere

* Modular Architecture
* Put AI To work
* Built on OpenShift

#### Cloud Pak for Applications

> Tools to modernize existing applications and build new cloud native applications

* Cloud-native accelerators
* Modernization and transformation
* Java EE platform
* Mobile app development tools

#### Cloud Pak for Data

* Unified platform
* Databases
* Data Virtualization
* Data Governance
* AI services
* Model lifecycle

#### Cloud Pak for Multicloud Management

* Dashboard
* Compliance
* SRE Tooling
* Partner integrations

#### Cloud Pak for Integration

> Integration tools to connect your applications and data

* API Connect
* App Connect
* MQ and Event Streams
* High-speed data transfer

#### Cloud Pak for Security

* Security capabilities
* Core platform services
* Integration with existing tools and data

#### Cloud Pak for Automation

* Low code tools to consume content
* Business automation workflow
* Automate business policies

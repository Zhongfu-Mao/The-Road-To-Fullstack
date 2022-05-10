# Introduction to Cloud

## Overview of Cloud Computing

### Definition

> A model for enabling convenient, on-demand network access to a shared pool of configurable computing resources that can be repidly provisioned and released with minimal management effort or service prodiver interaction.

### Examples of Cloud Computing Resources

* networks
* servers
* storage
* applications
* services

### Essential Characteristics

* On-demand Self-service
* Broad Network Access
* Resource Pooling
* Repid Elasticity
* Measured Service

### Deployment Models

* Public Cloud
* Private Cloud
* Hybrid Cloud

!!! note

    Deployment models indicates:

    * where the infrastructure resides
    * who owns and manages it
    * how cloud resources and services are made available to users

### Service Models

* Infrastructure
* Platform
* Application

### Benefits of Cloud Adoption

* Flexibility
* Efficiency
* Strategic Value

### Challenges of Cloud Adoption

* Data security, associated with loss or unavailablity of data causing business disruption
* Governance and sovereignty issues
* Legal, regulatory and compliance issues
* Lack of standardization in how the constantly evolving technologies integrate and interoperate
* Choosing the right deployment and service models to serve specific needs
* Partnering with the right cloud service providers
* Concerns related to business continuity and disaster recovery

### Key Cloud Service Providers and Their Services

* Alibaba Cloud
* Amazon Web Services
* Google Cloud Platform
* IBM Cloud
* Microsoft Azure
* Oracle Cloud
* Salesforce
* SAP Cloud Platform

## Cloud Adoption and Emerging Technologies

!!! note

    * Three-way symbiotic relationship between IoT, AI and Cloud:
      * IoT delivers the data
      * AI powers the insights
      * Both emerging technologies leverage cloud's scalablity and processing power
    * Three-way relationship between blockchain, AI and Cloud:
      * Blockchain provides the trusted, decentralized source of truth
      * AI powers the analytics and decisions made from the collected data
      * Cloud provides the globally distributed, scalable, and cost-effective computing resources to support both technologies

## Cloud Computing Service and Deployment Models

### IaaS: Infrastructure as a Service

#### IaaS Definition

> Infrastructure-as-a-Service(IaaS) is a form of cloud computing that delivers fundamental `compute`, `network`, and `storage` services to consume **on-demand, over the internet, on a pay-as-you-go** basis.  
> The cloud provider hosts the infrastructure components traditionally present in an on-premises data center as well as the **virtualization** or **hypervisor layer**.

#### IaaS Stucture

* Physical data centers: physical machines
* Compute: compute memory storage
* Network: virtualizations, or APIs
* Storage: object, file, block

#### IaaS Usage

* Test and Development
* Business Continuity and Disaster Recovery
* Faster Deployment and Scaling
* High Performance Computing
* Big Data Analysis

#### IaaS Concerns

* Lack of transparency
* Dependency on a third-party

### PaaS: Platform as a Service

#### PaaS Definition

> Platform-as-a-Service(PaaS) is a cloud computing model that provides a complete application platform to `Develop`, `Deploy`, `Run`, and `Manage` applications.

#### PaaS Providers Host & Manage

* Servers
* Networks
* Storage
* Operating Systems
* Application Runtime
* APIs
* Middleware
* Databases

#### Essential Charasteristics of PaaS

* High level of Abstraction: Eliminate complexity of deploying applications
* Support Services and APIs: Simplify the job of developers and IT professionals
* Run-time environments: Execute code according to application owner and cloud provider policies
* Rapid deployment mechanisms: Deploy, run, and scale applications efficiently
* Middleware capabilities: Support a range of application infrastructure capabilities

#### PaaS Use Cases

* API development and management
* Internet of Things (IoT)
* Business analytics/intelligence
* Business Process Management(BPM)
* Master data management(MDM)

#### Advantages of PaaS

* Scalability
* Faster time to market
* Greater agility and innovation

#### PaaS available offerings

* AWS Elastic Beanstalk
* CLOUDFOUNDRY
* IBM Cloud Paks
* Azure
* OPENSHIFT
* Magento
* force.com
* apache Stratos

#### Risks of PaaS

* Information security threats
* Dependency on service provider's infrastructure
* Customers lack control over changes in strategy, service offerings, or tools

### SaaS: Software as a Service

#### SaaS Definition

> Software-as-a-Service(SaaS) is a cloud offering that provides access to a service provider's cloud-based software and services.  
> Providers maintains Servers, Databases, Application Code, Security  
> Providers managers Application Security, Availability, and Performance

#### SaaS Supports

* Email and Collaboration
* Customer Relationship Management
* Human Resource Management
* Financial Management

#### Key Characteristics of SaaS

* Multitenant Architecture
* Manage Privileges and Monitor Data
* Security, Compliance, Maintenance
* Customize Applications
* Subscription Model
* Scalable Resources

#### Key Benefits of SaaS

* Greatly reduces the time from decision to value
* Increase workforce productivity and efficiency
  * Users can access the application from anywhere, anytime
  * Buy and deploy applications in minutes
* Spread out software costs over time

#### SaaS Use Cases

* Reduce on-premises IT infrastructure and capital expenditure
* Avoid ongoing upgrades, maintenance, and patching
* Run applications with minimal input
* Manage websites, marketing, sales, and operations
* Gain resilience and business continuity of the cloud provider

#### SaaS Concerns

* Data ownership and data safety
* Third-party maintains business-critical data
* Needs good internet connection

### Public Cloud

#### Public Cloud Characteristics

* Virtualized multi-tenant architecture enabling tenants or users to share computing resources
* The cloud providers pool of resources, including infrastructure, platforms, and software, and NOT dedicated for use by a single tenant or organization
* Resources are distributed on an as-needed basis offered through a variety of subscription and pay-as-you-go models

#### Public Cloud Benefits

* On-demand resources
* Economies of scale
* Highly reliable

#### Public Cloud Concerns

* Security: Data breaches, data loss, account hijacking, insufficient due diligence, and system and application vulnerabilities
* Data sovereignty compliance: It's increasingly critical for companies to be compliant with data sovereignty regulations governing the storage, transfer, and security of data

#### Public Cloud Use Cases

* Building and testing applications, and reducing time-to-market for their products and services
* Business with fluctuating capacity and resourcing needs
* Build secondary infrastructure for disaster recovery, data protection, and business continuity
* Cloud storage and data management services for greater accessibility, easy distribution, and backing up their data
* IT departments are outsourcing the management of less critical and standardized business platforms and applications to public cloud providers

### Private Cloud

#### Private Cloud Definition

> Cloud infrastructure provisioned for exclusive use by a **single organization** comprising multiple consumers, such as the business units within the organization.  
> It may be owned, managed, and operated by the organization, a third-party, or some combination of them, and it may exist on or off-premises.

#### Internal or External

* Internal Infrastructure: On-premises; owned and managed by the organization
* External infrastructure: Owned, managed, and operated by service provider

#### Virtual Private Cloud(VPC)

> An external cloud that offers a private, secure, computing environment in a shared public cloud

#### Benefits of Private Cloud

* Controlled by internal IT
* Reduce costs
* Better scalability
* Controlled access & security
* Greater agility and innovation

#### Private Cloud Use Cases

* Modernize and unify in-house & legacy applications
* Integrate data & application services from existing applications
* Build applications anywhere & move them without compromising security or compliance
* Full control over critical security & compliance issues within dedicated cloud

### Hybrid Cloud

#### Hybrid Cloud Definition

> Connects an organization's on-premise private cloud and third-party public cloud.  
> Which gives the organization the ability to use its own private cloud infrastructure, while also benefiting from the third-party cloud infrastructure.

#### The Three Tenets

* Interoperable: Public & private clouds understand each other's APIs, configuration, data formats, authentication and authorization
* Scalable: Private clouds can leverage public cloud capacity
* Portable: Move applications and data between on-premise, cloud systems, and cloud services providers

#### Types of Hybrid Cloud

* Hybrid Monocloud: One cloud provider
* Hybrid Multicloud: Can be deployed on any public cloud infrastructure
* Composite Cloud: Greater flexibility and scalability

#### Hybrid Cloud Benefits

* Security and compliance
* Scalability and resilience
* Resource optimization
* Cost savings

#### Hybrid Cloud Use Cases

* Software as a Service (SaaS) integration
* Data and AI integration
* Enhancing legacy applications
* VMware migration

## Components of Cloud Computing

### Computing Resources

* Virtual Servers(VMs): Software based
  * Rapidly provisioned
  * Provide an elastic and scalable computing environment
  * Low cost to use
* Bare Metal Servers(BMs): Physical servers
  * Work best for CPU and I/O intensive workloads
  * Excel with highest performance and security
  * Satisfy strict compliance requirements
  * Offer complete flexibility, control and transparency
  * Come with added management and operational overhead
* "Serverless": Abstraction

### Storage

* Block Storage
* File Storage
* Object Storage: The most-common mode of storage

### Networking

* Public Interfaces: connect the servers to the public internet
* Private Interfaces: provide connectivity to your other cloud resources and help keep them secure

Network interfaces in the cloud need:

* IP address
* subnets

It is even more important to configure which network traffic and users can access your resources:

* Security Groups
* ACLs
* VLANs
* VPCs
* VPNs

Some of the traditional hardware appliances can also be used in the cloud:

* firewalls
* load balancers
* gateways
* traffic analyzers

Another networking capability provided by the Cloud Providers is CDNs.

## Cloud Computing Storage and Content Delivery Network

### File Storage

* Like Direct Attached: Attached to a computer node to store data
* Unlike Direct Attached:
  * Less Expensive
  * More resilient
  * Less disk management and maintenance for users
  * Provision much larger amounts storage

File storage is mounted from remote storage appliances: Physical disks -> Storage appliances -> Computer nodes -> File storage

File storage is mounted on compute nodes via ethernet networks:

* Network dedicated for storage
* Network Attached Storage or Network File Storage(NFS)
* Speeds vary based on network traffic
* For workloads where consistent speed is not required

File storage can be mounted onto more than one compute node

Common workloads:

* Department file share
* Landing zone for incoming files
* Repository for data files
* Low cost database storage

### Block Storage

#### What is Block Storage?

* Block storage breaks files into chunks(or blocks) of data
* Stores each block separetly under a unique address
* Must be attached to a compute node before it can be utilized
* Mounted from remote storage appliances
* Extremely resilient to failures
* Data is more secure

Block storage is mounted as a volume to compute nodes using a dedicated network of optical fibres:

* Signals move at the speed of light
* Higher price-point
* Perfect for workloads that need low-latency
* Consistent high speed
* Databases and mail servers
* Not suitable for shared storage between multiple servers

#### Common Attributes of File & Block Storage

* Block and File Storage is taken from appliances which are maintained by the service provider
* Both are highly available and resilient
* Often include data encryption at rest and in transit

#### Differences: File Storage vs Block Storage

File Storage:

* Attached via ethernet network
* Speeds vary, based on load
* Can attach to multiple compute nodes at once
* Good for file shares where:
  * Fast connectivity isn't required
  * Cost is a factor

Block Storage:

* Attached via high-speed fibre network
* Only attach to one node at a time
* Good for applications that need consistent fast access to disk

### Object Storage

* Object storage can be used without connecting to particular compute node to use it -> Access via API to download or upload
* Object storage is less expensive than file storage or block storage
* Object storage is effectively infinite

Good for large amounts of unstructured data

Object Storage -> Bucket -> Metadata

#### Object Storage Use Cases

* Text files
* Audio files
* Video files
* IoT data
* VM images
* Backup files
* Data Archives

Any Data which is static and where fast read and write speed are not necessary  
Not suitable for operating systems, databases, changing content

#### Tiers and APIs

The tiers are based on how frequently the data is accessed:

* Standard Tier: Frequently accessed data
* Vault/Archive Tier: Seldom accessed data like once or twice a month
* Cold Vault Tier: Rarely accessed data like once or twice a year

## Emergent Trend, Cloud Native, DevOps and Application Modernization

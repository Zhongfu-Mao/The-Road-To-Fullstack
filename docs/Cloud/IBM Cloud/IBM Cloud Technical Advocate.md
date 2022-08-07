# IBM Cloud Technical Advocate

## An Introduction to Cloud

### The history of Cloud Computing

* Amazon Web Services (AWS) launched in 2006.
* Google Cloud Platform(GCP) launched in 2008.
* Microsoft Azure launched in 2010.
* IBM launched SmartCloud Enterprise in early 2011.

### Hypevistor

Type 1 Hypervisors

* Can support multiple virtual machines
* Also known as a “bare metal” hypervisors
* Most frequently used and seen in the market, most secure, lower latency
* Examples include VMware ESXi, Microsoft Hyper-V, open source Kernel-based Virtual Machine (KVM)

Type 2 Hypervisors

* Run as an application in a host operating system, rather than in place of an operating system
* Create a virtual machine and install a guest operating system on it
* Assign physical resources to a virtual machine and set the amount of processor cores and memory it can use
* Known as “hosted”
* Mostly used for end-user virtualization, less frequently used, higher latency
* Some examples are Oracle VirtualBox and VMware Workstation

### HybridCloud vs MultiCloud

#### Hybrid Cloud

Features:

A hybrid cloud is formed when an organization’s on-premises private cloud and a third-party public cloud are connected, forming a single flexible infrastructure that runs applications and workloads.

Benefits:

* Developer productivity increases as Agile (an approach to software development)  and DevOps (set of practices that combines software development with IT operations (Ops) methodologies are adopted, enabling teams to develop once then deploy to all clouds.
* There is greater control over resources as development teams optimize usage across public cloud services, private clouds, and cloud vendors.
* Security and compliance across all environments are implemented in a consistent way.
* Overall business operations are accelerated, such as shorter development times, faster response to customers, and faster delivery of new products and services.

#### MultiCloud

Features:

A multicloud uses cloud services from more than one cloud vendor. Applications are run on PaaS or IaaS from multiple cloud service vendors.

Benefits:

* Organizations have the flexibility to choose cloud services from different cloud providers.
* Technologies can be adopted from any vendor as needed or as they emerge.
* There is reduced vulnerability to outages and unplanned downtime.
* Exposure to licensing, security, compatibility, and other issues is reduced.

## IBM Cloud Fundamentals

### IBM Cloud Catalog Services

* You can find additional information about each service in the `IBM Cloud Catalog` using the "About" tab.
* `Code Engine` can be used to build container images.
* `IBM Cloud Object Storage` is a way to store data in units called buckets for easy access.
* `Db2` is a relational database with enterprise-grade performance.
* `Cloudant` is a NoSQL database that uses JSON files to store and index documents.
* `Watson Assistant` can be used to add chat functionality to an application.
* `Watson Discovery` is used to gain a deeper understanding of data and implement natural language document search capabilities.
* `Watson Studio` allows you to customize machine learning models.
* `Certificate Manager` provides a centralized location to store and manage your security certificates.
* `Hyper Protect Crypto Service` provides hardware solutions to manage your crypto keys.

### DevSecOps

!!! abstract

    * Sec: Throughout the entire process, security is continually integrated.
    * Plan: In this stage, teams create a scope for new functionality based on end-user feedback.
    * Code: The development team writes the code for the new features.
    * Build: All of the code that has been written is stored in a central repository. Once developers request that their code be merged with existing code, a series of automated tests are run.
    * Test: The new code is tested in a temporary staging environment for deeper testing.
    * Release: At this phase, the new functionality is considered to be out of development and ready to be released to a production environment.
    * Deploy: This is the stage where the new functionality is officially released.
    * Operate: At this point, the new functionality is in full operation in the production in the production environment.
    * Monitor: The new functionality is monitored and issues and identified.

* DevOps was designed to create an integrated working environment between developers and IT operations.
* DevSecOps added security into the development cycle.
* DevOps was intended to decrease development time by adding automation to the process.
* Instead of releasing a couple updates per year, DevOps is designed to continually release smaller updates as needed.
* `Toolchains` are sets of tools that are used to automate the process of developing and deploying code.
* `Pipelines` are used to build, test, and deploy code with minimal human intervention.
* An integrated web-based environment allows developers to work from anywhere.

### Database, Integration and Analytic Service

#### Databases on IBM Cloud

* `IBM Cloud Databases for PostgreSQL` are customizable, open-source object-relational databases.
* `IBM Cloud Databases for EnterpriseDB` optimize the built-in features of PostgreSQL while adding compatibility with Oracle.
* `IBM Db2 on Cloud` is based on the enterprise-class IBM Db2 database engine and provides a fully managed solution.
* `IBM Cloudant` is a document database that uses JSON.
* `IBM Cloud Databases for MongoDB` is a JSON-based document store which includes rich query functionality.
* `IBM Cloud Databases for DataStax` is a NoSQL database built on Apache Cassandra which is best for high-availability and workload flexibility.
* `IBM Cloud Databases for Elastisearch` are based on JSON document databases and allow full-text search.
* `IBM Cloud Databases for Redis` are designed for in-memory functionality making them very fast.
* `IBM Cloud HyperProtect` can be used with PostgreSQL and MongoDB for fully managed, highly secure applications.

#### Analytics of IBM Cloud

* There are three types of analytics: descriptive, diagnostic, and prescriptive.
* `IBM Cloud Analytics` use two open-source technologies: Apache Hadoop and Apache Spark.
* `IBM Analytics Engine` builds on Apache Hadoop and Apache Spark but separates compute and storage functionality.
* `IBM Information Server on Cloud` can analyze a wide variety of data and is easily scalable.
* `IBM Streaming Analytics` allows you to analyze fast moving, real-time data.

#### Integration on IBM Cloud

* `API Connect` is used to create and manage APIs to your applications.
* `App Connect` is used to connect various applications to each other.
* `Event Streams` are built on Apache Kafka and are used as high throughput message buses.
* `MQ` provides enterprise-grade messaging capabilities between applications.

### IBM Cloud Security Strategy Overview

* There are three types of encryption: data at rest, data in motion, and data in use.
* IBM Cloud Identity and Access Management (IAM) is used to identify users and grant them access to specific parts of an application or network.
* There are two common types of IAM used in IBM Cloud: `Attribute-Based Access Control` (ABAC) and `Role-Based Access Control` (RBAC).
* There are three network encryption options: Secure Socket Layer (SSL), Transport Layer Security (TLS), and Hypertext Transfer Protocol Secure (HTTPS).
* IBM Certificate Manager is used to manage SSL and TLS certificates.
* Data in IBM Object Storage is divided up and distributed across multiple data centers.
* Once data in IBM Object Storage is deleted, it is impossible to retrieve it.

## Compute Options

### Bare Metal Servers

> Bare Metal servers are physical, single-tenant, dedicated servers that provide ultimate performance and control with low-level access to the hardware resources

Options:

* Fast Provisioning Servers: preconfigured servers that meet the needs of use cases for most clients
* Custom-Based Servers: been customized to meet particular CPU / Memory requirements

### Virtual Server for Classic

* Classic Virtual Servers are easily deployed and can be created on shared or dedicated infrastructure.
* Classic Virtual Servers are customizable, can be provisioned quickly, are scalable, and integrated seamlessly.
* Some of the deployment options are public virtual servers, transient virtual servers, and dedicated virtual servers.
* Some of the key differences between bare metal servers and virtual servers are that bare metal servers can offer better performance and security for certain workloads and are more ideal for heavy workloads. However, virtual servers provision more quickly and offer a more flexible and scalable environment than bare metal.

### Virtual Private Cloud

* Virtual Private Cloud (VPC) allows the creation of a private cloud computing environment on a shared public cloud infrastructure. VPC saves on cost and focuses on convenience for clients.
* VPC offers virtual server instances (VSIs) with a wide range of vCPU and memory options.
* Under VPC, block storage can be provisioned and attached to virtual server instances. Block storage either has defined IOPS tiers or you can provision storage with custom IOPS

### VMware Solutions Offerings

Deployment Offerings:

* VMware Solutions Shared
* VMware Solutions Dedicated
* VMware Solutions Regulated Workloads
* WMware Solutions Dedicated Security and Compliance Readiness Bundle

### Power Systems Virtual Server

* Power Systems Virtual Servers can be quickly created and deployed through the IBM Cloud console but are colocated with IBM Cloud resources.
* Power Systems Virtual Servers can run AIX, IBM i, or Linux operating systems.
* Some key features are monthly billing rates, customized infrastructure, and images from AIX and IBM i.
* Backup strategies for AIX are Veeam AIX and IBM Spectrum Project and IBM i uses IBM Backup, Recovery, and Media Services.

### Code Engine

> Code engine is a serverless platform

benefits:

* Building apps with your code using IBM's infrastructure
* Being able to run HTTP-driven apps and run-to-completion batch jobs
* Having private workloads
* Allowing clients to determine who gets access to the resources

### IBM Cloud Satellite

* IBM Cloud Satellite enables organizations to run IBM Cloud Services in the location of their choice
  * on-premises
  * a competitor's cloud
  * at the edge
* IBM Cloud Satellite enables users to run select IBM Cloud Services on-premises, behind their corporate firewall, allowing them to meet more demanding security rules or simply process data closer to its source
* There are four main Satellite components: **hosts, link, location, and endpoints**.
  * A host is a customer-provided computer running Red Hat Enterprise Linux 7.x. A minimum of three hosts are required for a Satellite location.
  * A Satellite location is a customer data center, competitors' cloud, or edge location, at which the Satellite Hosts are deployed and run.
  * A Satellite Link is an encrypted TLS tunnel that allows you to securely connect the Satellite installation to other services running in IBM Cloud and to manage and monitor the Satellite instance from the IBM Cloud Console.
  * Satellite Link has two types of Endpoint: a Cloud Endpoint and a Location Endpoint. The Cloud Endpoint destination is outside of the Satellite location, while the Location Endpoint provides access to a server, service, or app that runs in your Satellite location from a client that is connected to the IBM Cloud private network.

## Storage

### Block Storage

> Block storage is a technology that is used to store data files on SANs or cloud-based storage environments by breaking them into blocks and then storing those blocks as separate pieces.

* Block storage stores data by breaking it into evenly sized blocks, which is written to disk. The data stored is highly available because each block is stored multiple times across different disks.
* Block storage is used for computing situations where users require fast, efficient, and reliable data storage.
* Block storage decouples data from user environments. This allows that data to be spread across multiple environments enabling the user to retrieve it quickly.
* Block storage can be deployed on a Virtual Private Cloud (VPC) or classic environments.
* There are two available tiers: the IOPS tier, and the Custom IOPS profile tier.

### File Storage

* File storage uses a hierarchical structure to organize files, folders, and subfolders.
* There are strategic benefits to choosing file storage: reducing costs, and scaling up capacity.
* It is available in the endurance and performance tier.

### Object Storage

> Object storage is a storage option that manages unstructured data into self-contained units called Objects.

* Object storage is referred to as unstructured as it does not use a conventional 'folder/subfolder' structure to store objects. Instead, it uses a flat structure known as a "bucket."
* IBM Cloud Object Storage stores encrypted and dispersed data across multiple geographic locations.
* There are some advantages to using object storage. It enables customers to handle large amounts of unstructured data, is scalable and cost-effective, uses metadata allowing users to maximize the search feature, and quickly access the object they need.
* IBM Cloud Object Storage service offers different levels of resiliency: cross region, regional, and single data center.
* There are four tiers, including Smart, Standard, Vault, and Cold Vault tier.

#### Software Defined Storage (SDS) Offerings

* Software-defined storage (SDS) is a storage architecture that separates storage software from its hardware.
* It enables organizations to increase their storage capacity quickly making it flexible and scalable.
* SDS allows the organization to use existing hardware that they currently have, which can be a tremendous cost savings.
* Portworx is a highly available SDS that can be used as persistent storage management for containerized applications.

### Backup and Recovery

#### IBM Cloud Backup Capabilities

* `IBM Cloud Backup Portal` is a browser-based management utility that enables customers to back up data between servers or data centers on the IBM Cloud network.
* Backup and restore make periodic copies of data and applications to a secondary device.
* **RTO**(recovery time objective) is the maximum amount of time the organization can afford to be without access to the data or application. In other words, how quickly the customer needs to recover the data and application.
* **RPO**(recovery point objective) is the amount of data an organization can afford to lose and effectively dictates how frequently they need to back up their data to avoid losing more.
* There are four types of backup devices or services a customer can use: *tape drive*, *HDD or SDD*, *backup server*, or *cloud backup*.  
* Commonly used back and restore methods include *full image only*, *incremental*, *differential*, *CDP*, *bare metal backup*, and *instant recovery*.
* Disaster recovery is much different than backup and restore. Disaster recovery is a plan that is created to deal with an outage that impacts applications, data, and IT resources.  
* Data replication allows the use of real-time information that captures data that is constantly changing to allow for efficient data growth management.  

#### Zerto, Veeam, and IBM Spectrum Protect Plus within VMware Solutions in IBM Cloud

* There are a wide variety of services used for disaster recovery and protection. Zerto, Veeam, and IBM Spectrum Protect Plus are the most commonly used for these services.
* `Zerto` is a service that provides replication and disaster recovery capabilities using continuous data replication with journaling versus snapshots.
* `Veeam` is a service that integrates directly with VMware hypervisors to help an organization achieve high availability to control backup and restore for all the virtual machines attached to their infrastructure from one console.
* `IBM Spectrum Protect Plus` creates an efficient and scalable solution for clients who need data protection, reuse, and recovery in virtual environments.

#### Disaster Recovery options in IBM Power Systems Virtual Server

* In the event of a hardware failure, the `IBM Power Systems Virtual Server` service will restart the virtual servers on a different host system to provide uninterrupted service.
* There are four strategies used for data recovery, including *image capture*, *AIX backup*, *IBM i backups*, and *cloud object storage*.

## Networking

### Basic Networking Options

* Automatic VLANs are provisioned and removed automatically based on whether there are cloud services which need them.
* VLANs remain on an account until they are canceled.
* VRF allows multiple instances of a routing table to exist in a router and to work simultaneously.
* The cloud automatically assigns and manages primary subnets.

### Load Balancer Options

* Distributing connections using load balancers prevents server overload and enhances uptime.
* Cloud Internet Services provide global load balancer services.

### Direct Link Offerings

* Direct Link offerings provide connectivity from external sources into a private cloud network.
* Direct Link Connect on Classic provides private access to the cloud infrastructure.
* Global routing can be added to all Direct Link products.
* Direct Link creates private connections between on-premises environment and cloud resources.
* Private connects are created without using the public internet.
* Workloads with large and frequent data transfers are supported.
* A Direct Link Connect on Classic connection is best for a customer who wants to reduce their cloud connection costs and use a carrier who owns and operates a network.

### Virtual Private Cloud Networking

* A VPC provides cloud security to workloads.
* By default, resources in a VPC are isolated from other services.
* A VPC can contain multiple subnets within each zone.
* A public gateway can be attached to a VPC subnet to allow the subnet to route traffic to and from the internet.

### VPCs

* A virtual private cloud provides a private cloud environment on a shared public cloud infrastructure.
* VPC infrastructure is deployed across three zones.
* VPC cloud resources have their own isolated virtual network.

### Transit Gateways

* Transit gateways connect VPC resources across multiple regions.
* Routing options stay in the private cloud infrastructure.
* Connecting transit gateways to Direct Link enables connection to an on-premises network and other networks connected to the transit gateway.

## Services

### Cloud Integration Use Cases

* `IBM API Connect` lets users create, secure, expose, manage, socialize, and analyze its APIs across clouds.
* `IBM APP Connect` integrates data and applications from existing systems, and ties together technologies across environments, including legacy and SaaS systems.
* Apache Kafka-based `IBM Event Streams` enable organizations to create smart applications that react to events as soon as they happen.
* `IBM MQ` is a scalable messaging platform that uses Java Message Service (JMS) and other technologies to integrate applications and put information such as product availability on the cloud, where consumers can easily retrieve it.

### Edge Solution

* Edge computing is a distributed computing method that aims to use bandwidth more efficiently, by bringing applications close to where data is created and actions are performed.
* By eliminating the need to send data over a network, edge computing reduces latency and enables real-time processing.
* When implementing an `IBM Cloud Internet Service (CIS)` Edge function, developers consider the actions they want it to perform. For each action, they define a uniform resource identifier (URIs) called a trigger. IBM CIS Edge intercepts user requests, compares them against the list of triggers, and performs the associated action if it finds a match, called a trigger event.
* Because edge functions run code on trusted CIS Edge servers, users don't need to use a modern browser.
* If processing needs to occur on client-provided servers physically located at the edge, IBM Cloud Satellite may be a more appropriate solution.

### AI and Analytics

IBM's AI Ladder views the process of gathering, preparing, and using data in terms of a ladder comprised of four steps:

* collecting data
* organizing data
* analyzing data to scale business insight
* infusing data to implement AI with trust and transparency

### Hyper Protect Crypto Services

* IBM Cloud `Hyper Protect Crypto Services (HPCS)` is a dedicated key management service that uses a dedicated cryptographic processing Hardware Security Module (HSM) to generate, encrypt, store, and decrypt keys.
* The HSM is built on FIPS 140-2 Level 4 certified hardware: the highest level available for cryptographic security.
* Customers retain exclusive control of their keys with a feature called Keep Your Own Key (KYOK).
* Users can integrate HPCS with selected managed database services to bring and manage their own encryption in the cloud.
* Integration involves associating user-managed HPCS root keys to control the randomly generated ones from the database service, and then adding another layer of protection, envelope encryption, to the data.
* By default, cloud providers control system keys. But for even greater protection, users should control their own keys.
* In order to keep all of their keys, users must set up the HSM themselves, which requires a dedicated solution like HPCS.
* Customers benefit from HPCS cryptographic capabilities in many ways: image protection, app development, database encryption, and enterprise environments.

## Security

### Network Security Options

* ACLs and security groups are two types of network access controls that make up the layers of VPC security.
* Network security provides security to information in a network and also controls who can access the network, but there are vulnerable entry points that warrant defense mechanisms for enhanced security.
* Juniper vSRX is a router, firewall, and security device that exists as a virtual appliance and provides a firewall, VPN gateway, and NAT as an encryption feature.
* There are multiple ways to secure data in transit or data at rest.

### Storage Security Options

* IBM Cloud File Storage and IBM Cloud Block Storage are provisioned with Endurance or Performance options.
* IBM Cloud Object Storage provides the ability to store large volumes of unstructured data.
* IAM, OpenShift & Containers, and VMware provide varying levels of access policies in order to secure solutions built on IBM Cloud.
* Block Storage for VPC gives users the ability to provide hypervisor-mounted, high-performance data storage for any VSIs that can be provisioned within a VPC.
* IBM Cloud Object Storage provides storage for large volumes of unstructured data that provides security, availability, and reliability.
* When utilizing VMware Solutions Dedicated, data can be stored locally, or using IBM Cloud File Storage or Cloud Object Storage.
* When using VMware Solutions Shared, the workload data is in an IBM-managed cloud infrastructure account.
* VSIs and customer-managed encryption are other options to secure data.

### PaaS Security Options

#### Network Security

* `Data Shield` is an IBM Cloud service that helps protect data in containerized workloads that run on Kubernetes Service and OpenShift clusters while the data is in use.
* Service endpoints are a connectivity option for securely accessing cloud service endpoints.
* Application exposure services enable users to securely expose applications to external traffic.

#### Authenticating Users

* SSO provides authentication between multiple web apps.
* App ID is a service provided by IBM Cloud that allows users to create and use SSO for their own applications.
* vCenter Single Sign-On (SSO) is an authentication broker and security token exchange infrastructure. This allows vSphere to communicate with each other via a secure token mechanism.

#### Encryption, Secrets, and Certificates

* Secrets Manager creates dynamic secrets and manages the lifecycle of the secrets.  
* IBM Key Protect securely stores and applies secrets for apps. It provides encryption solutions and allows data to be secured and stored in IBM Cloud through envelope encryption.
* Hyper Protect Crypto Services is a key management system that provides keep your own key (KYOK) capabilities for cloud data encryption. It provides lifecycle management for keys, encryption for IBM Cloud services, access management, auditing, and security certification.
* VMware integrates on-premises vSphere vCenter networks to the IBM Cloud for VMware solutions deployment.

#### IBM Cloud Code Engine and Security

IBM Code Engine provides a security solution by isolating customers and their workloads.

#### Delivery Pipeline Private and Public Workers

Delivery Pipeline Private Workers and the IBM Cloud Continuous Delivery Development teams work together to use the private worker in their toolchain.

#### Other Security Topics

* Terraform is a third-party service used by IBM Cloud, and it enables predictable provisioning of the IBM Cloud platform, classic infrastructure, and VPC infrastructure.
* Data Shield is an IBM Cloud service that helps protect data in containerized workloads that run on Kubernetes and OpenShift clusters while the data is in use.  

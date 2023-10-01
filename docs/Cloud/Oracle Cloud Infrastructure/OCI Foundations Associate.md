# OCI Foundations Associate

## Introduction

### Architecture

* Regions
* Availability Domains
* Fault Domains

### Distributed Cloud

* Public Cloud
* Hybrid Cloud
    * Dedicated Region Cloud@Customer
    * Oracle Cloud VMware Solution
    * Autonomous DB on Exadata Cloud@Customer
    * Roving Edge Infrastructure
* Dedicated Cloud
* Multi-Cloud: OCI-Azure Interconnect
    * 12 Azure Interconnect Regions
    * <2 milliseconds latency private interconnection
    * No egress or ingress charges for data transfer

## IAM

* Oracle Cloud ID (OCID): unique identifier for every resource in OCI, `ocid1.<Resource Type>.<Realm>.<Region>.[<Future use>].<Unique ID>`
* Compartment: logical container for organizing and isolating resources, max 6 levels
* Principles: users, groups, dynamic groups, compartments
* Policies: document that specifies who has what type of access to which resources
* Federation: allows to use external identity provider (IdP) to authenticate users
* AuthZ: allow `<group_name>` to `<verb>` `<resource_type>` in `<location>` where `<condition>`

!!! note

    verb: 

    * manage
    * use
    * read
    * inspect

## Networking

* VCN: virtual private network, logically isolated network
* Internet Gateway: Two-way communication between VCN and Internet
* Service Gateway: Access from a VCN to public Oracle services
* NAT Gateway: One-way communication from VCN to Internet
* Dynamic Routing Gateway: Access from a VCN to destination other than the Internet

!!! tip

    Route tables are only referenced for traffic destined outside of the VCN;  
    traffic between two points inside of the VCN is handled automatically.

* Security List: A set of firewall rules that apply to all resources in a subnet
* Network Security Group: A set of firewall rules that apply to any set of resources in a VCN that you specify

## Compute

!!! tip

    The OCI Compute service offers instances powered by various processor types, including ==AMD==, ==Intel==, and ==Ampere==.

> Autoscaling in an instance pool within the OCI Compute service automatically provisions and removes instances based on specific conditions or schedules.  
> It does not change the shape of the compute instance, nor is it limited to only metric-based or schedule-based autoscaling.  
> Instead, autoscaling can be driven by both metric-based and schedule-based policies, offering a more dynamic and flexible scaling solution.

## Storage

### Object Storage

!!! note

    An existing standard Object Storage bucket cannot be downgraded to the Archive Storage tier and an Archive Storage bucket cannot be upgraded to the standard Object Storage tier. 

* The minimum duration to store objects in the Archive tier is 90 days.
* Objects in the Archive Storage tier cannot be accessed directly. Instead, you need to restore the object to the Standard tier before reading it.
* From the time a restore request is made, it takes at most an hour to read the data.
* You can specify a duration time from 1 to 240 hours that the restored data is accessible for download on the Object Storage tier.
* If you do not explicitly set a duration time, data is available for download for 24 hours by default.

## DataBase

* Oracle Autonomous Database
    * Autonomous Data Warehouse(ADW) for high-performance analytics
    * Autonomous Transaction Processing(ATP) for high-performance transactional workloads
    * APEX Service for low-code application development
    * Autonomous JSON Database(AJD) for JSON document storage and querying

!!! note

    Automated: 

    * Provisioning
    * Scale-up and Scale-out
    * Tuning
    * Security and Patching
    * Fault Tolerance

> The self-driving feature of Oracle Autonomous Database enables automatic database optimizations without manual intervention.  
> It uses machine learning and automation to perform tasks such as provisioning, patching, tuning, and backup, which helps reduce the need for manual database administration and maintenance.

### MySQL Heatwave

> MySQL HeatWave is an integrated query accelerator for the MySQL Database service in Oracle Cloud Infrastructure.  
> It significantly boosts the performance of MySQL, enabling it to efficiently run OLAP (Online Analytical Processing) queries, which are complex queries that analyze large amounts of data to uncover business insights.

* MySQL HeatWave uses an in-memory data storage mechanism to provide high-performance query execution.
* It achieves this by storing the data in a columnar format in-memory, which allows for faster access and processing of data during query execution, especially for OLAP workloads.

## Security

* OCI Cloud Guard: continuous monitoring and response system that helps to detect security threats across all Oracle Cloud Infrastructure resources.
    * `Detectors` continuously monitor your infrastructure, looking for potential issues.
    * `Problems` are the security risks and issues that detectors identify.
    * `Responders` are the automatic or manual actions taken to address the identified problems.
* Security Zone: Refers to a cloud compartment in which you cannot disable security features such as encryption, logging, and auditing.
* Security Advisor: Refers to a cloud service that unifies security zone, cloud guard, and other cloud capabilities to provide a single pane of glass for security monitoring and response.
* OCI Vault is composed of various components including master encryption keys, secrets, and vaults.
    * A vault in OCI is a logical entity where you can centrally manage and store your encryption keys and secrets.
    * A secret is a resource that helps manage credentials needed to access OCI resources.
    * A master encryption key is a key that OCI uses to encrypt the encryption keys that you create in the vault (these are customer managed).

## Governance and Administration

### Pricing

> [Comparison of cloud pricing lists](https://www.oracle.com/cloud/economics/)

* Pay-as-you-go: pay only for the resources you use
* Annual Universal Credits: commit to a certain amount of cloud resources for a year
* Bring Your Own License: use your existing on-premises licenses to run Oracle Database on Oracle Cloud Infrastructure

!!! tip

    OCI maintains the same pricing across all regions, so the choice of OCI region does not directly influence pricing. 

### Cost Management

* OCI Budgets: monitor and manage your spending by setting up budgets that alert you when your spending exceeds a certain amount.
* Cost Analysis: analyze your spending by viewing your cost data in a variety of ways, including by service, compartment, and tag.
* Usage Reports: view your usage data in a variety of ways, including by service, compartment, and tag.
* Service Limits: view and manage your service limits.
* Compartment Quotas: view and manage your compartment quotas.

!!! note

    Service limits are the upper bounds placed by Oracle on the number of resources you can create in a region or tenancy, while compartment quotas are the upper bounds defined by the users for resource usage within specific compartments.  
    The distinction is that service limits are set by Oracle and apply to a tenancy in a region, while compartment quotas are set by the users and apply to specific compartments.

### Tagging

* Tag Namespace is a container for a set of tag keys with tag key definitions.
* Tag key definition specifies its key and what types of values are allowed.
* Tag key definition or a tag namespace cannot be deleted, but retired.

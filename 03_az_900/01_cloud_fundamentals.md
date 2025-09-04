# Cloud Fundamentals

## Table of contents
1. [Cloud Computing](#question1)
2. [Cloud benefits](#question2)
3. [Cloud Service Types](#question3)
4. [Shared responsibility model](#question4)
5. [Consumption-based model](#question5)

## 1. Cloud Computing <a name="question1"></a>

**Cloud Computing** is the delivery of computing services over the internet, enabling faster innovation, flexible resources, and economies of scale.  
- Compute Power (8GB RAM, 1TB Storage, etc)
  
**Private cloud:**  
- Organisations create a cloud environment in their datacenter
- Organization is responsible for operating the services they provide
- Does not provide access to users outside the organisation

**Public cloud:**  
- Owned by cloud services or hosting providers
- Provides resources and services to multiple organizations and users
- Accessed via secure network connection (typically over the internet)

**Hybrid cloud:**  
Combines Public and Private clouds to allow applications to run in the most appropriate location

**Cloud model comparison:**
1. Public Cloud:
    - No capital expenditures to scale up
    - Applications can be quickly provisioned and deprovisioned
    - Organizations pay only for what they use
2. Private Cloud:
    - Hardware must be purchased for start-up and maintenance
    - Organizations have complete control over resources and security
    - Organizations are responsible for hardware maintenance and updates
3. Hybrid Cloud:
    - Provides the most flexibility
    - Organizations determine where to run their applications
    - Organizations control security, compliance, or legal requirements

## 2. Cloud benefits <a name="question2"></a>

1. **High availability:** aka uptime. Azure is a highly available cloud environment with uptime guarantees depending on the service. These guarantees are part of the service-level agreements (SLAs).
    - SLA 99%: downtime is 1.68h per week, 7.2h per month
    - SLA 99.9%: downtime is 10 min per week, 43.2 min per month
2. **Scalability:** refers to the ability to adjust resources to meet demand (vertically - processing power and horizontally - replicas)
    - You can add more resources to better handle the increased demand
    - You aren't overpaying for services
3. **Elasticity:** the ability to scale automatically
4. **Reliability:** is the ability of a system to recover from failures and continue to function (use global scale for your resources. If one is down, all others are up)
5. **Predictability:**  
    - Performance predictability focuses on predicting the resources needed to deliver a positive experience for your customers
    - Cost predictability is focused on predicting or forecasting the cost of the cloud spend
6. **Security:** Cloud providers offer improved data security, and compliance-oriented frameworks adhere to major regulations. If you want maximum control of security, infrastructure as a service provides you with physical resources but lets you manage the operating systems and installed software, including patches and maintenance
7. **Governance:** all your deployed resources meet corporate standards and government regulatory requirements. Depending on your operating model, software patches and updates may also automatically be applied, which helps with both governance and security
8. **Manageability**:
    - Management of the cloud:
        - Automatically scale resource deployment based on need.
        - Deploy resources based on a preconfigured template, removing the need for manual configuration.
        - Monitor the health of resources and automatically replace failing resources.
        - Receive automatic alerts based on configured metrics, so you’re aware of performance in real time.
    - Management in the cloud:
        - Through a web portal.
        - Using a command line interface.
        - Using APIs.
        - Using PowerShell.

## 3. Cloud Service Types <a name="question3"></a>

1. Infrastructure as a Service (IaaS): build pay-as-you-go IT infrastructure by renting servers, virtual machines, storage, networks, and operating systems from a cloud provider (servers and storages, Networking Firewalls/Security, Datacenter, Physical Plant/building).
2. Platfrom as a Service (PaaS): provides environment for building, testing, and deploying software applications; without focusing on managing underlying infrastructure (includes IaaS + Operating systems, Development Tools, database Management, Business Analytics).
3. Software as a Services (SaaS): users connect to and use cloud-based apps over the internet: for example, MS Office 365, email, and calendars (includes IaaS, PaaS + Hosted applications)

**Cloud service comparison:**  
1. IaaS: the most flexible cloud service, as it provides you the maximum amount of control for your cloud resources (renting the hardware in a cloud datacenter).
    - cloud provider is responsible for maintaining the hardware, network connectivity (to the internet), and physical security
    - You’re responsible for everything else: operating system installation, configuration, and maintenance; network configuration; database and storage configuration  
    **Examples:**  
    - Lift-and-shift migration: You’re setting up cloud resources similar to your on-prem datacenter, and then simply moving the things running on-prem to running on the IaaS infrastructure.
    - Testing and development: You have established configurations for development and test environments that you need to rapidly replicate. You can start up or shut down the different environments rapidly with an IaaS structure, while maintaining complete control.
2. PaaS: well suited to provide a complete development environment without the headache of maintaining all the development infrastructure
    - cloud provider maintains the physical infrastructure, physical security, and connection to the internet, operating systems, middleware, development tools, and business intelligence services that make up a cloud solution
    - Depending on the configuration, you or the cloud provider may be responsible for networking settings and connectivity within your cloud environment, network and application security, and the directory infrastructure.  
    **Examples:**  
    - Development framework: PaaS provides a framework that developers can build upon to develop or customize cloud-based applications. Similar to the way you create an Excel macro, PaaS lets developers create applications using built-in software components. Cloud features such as scalability, high-availability, and multi-tenant capability are included, reducing the amount of coding that developers must do.
    - Analytics or business intelligence: Tools provided as a service with PaaS allow organizations to analyze and mine their data, finding insights and patterns and predicting outcomes to improve forecasting, product design decisions, investment returns, and other business decisions.
3. SaaS: renting or using a fully developed application
    - Pay-as-you-go pricing model
    - Users pay for the software they use on a subscription model

## 4. Shared responsibility model <a name="question4"></a>

Start with a traditional corporate datacenter. The company is responsible for maintaining the physical space, ensuring security, and maintaining or replacing the servers if anything happens. The IT department is responsible for maintaining all the infrastructure and software needed to keep the datacenter up and running. They’re also likely to be responsible for keeping all systems patched and on the correct version.  
  
With the shared responsibility model, these responsibilities get shared between the cloud provider and the consumer. Physical security, power, cooling, and network connectivity are the responsibility of the cloud provider. The consumer isn’t collocated with the datacenter, so it wouldn’t make sense for the consumer to have any of those responsibilities.  
  
At the same time, the consumer is responsible for the data and information stored in the cloud. (You wouldn’t want the cloud provider to be able to read your information.) The consumer is also responsible for access security, meaning you only give access to those who need it.  

When using a cloud provider, you’ll always be responsible for:
- The information and data stored in the cloud
- Devices that are allowed to connect to your cloud (cell phones, computers, and so on)
- The accounts and identities of the people, services, and devices within your organization

The cloud provider is always responsible for:
- The physical datacenter
- The physical network
- The physical hosts

Your service model will determine responsibility for things like:
- Operating systems
- Network controls
- Applications
- Identity and infrastructure

## 5. Consumption-based model <a name="question5"></a>

**CapEx vs OpEx**  
1. Capital Expenditure:
    - one-time, the up-front spending of money on physical infrastructure
    - Costs from CapEx have a value that reduces over time
2. Operational Expenditure (OpEx)
    - Spend on products and services as needed, pay-as-you-go
    - Get billed immediately

**Benefits:**  
- No upfront costs.
- No need to purchase and manage costly infrastructure that users might not use to its fullest potential.
- The ability to pay for more resources when they're needed.
- The ability to stop paying for resources that are no longer needed.

# Basics

## Table of contents
1. [AWS CodeCommit, CodeBuild, CodeDeploy, and CodePipeline](#question1)
2. [Differentiate between EC2, Lambda, and ECS/EKS](#question2)
3. [Discuss AWS CloudWatch, CloudTrail](#question3)
4. [Explain VPCs, subnets, security groups, and network ACLs](#question4)
5. [Discuss S3, EBS, and EFS](#question5)
6. [Explain services like RDS, DynamoDB, and Aurora](#question6)
7. [Configuration Management: Discuss tools like AWS Systems Manager or third-party tools like Ansible](#question7)
8. [Some](#question8)
9. [Some](#question9)
10. [NoSQL DB](#question10)

## 1. AWS CodeCommit, CodeBuild, CodeDeploy, and CodePipeline <a name="question1"></a>

AWS CodeCommit, CodeBuild, CodeDeploy, and CodePipeline are core services within the AWS developer tools suite, designed to facilitate Continuous Integration and Continuous Delivery (CI/CD) workflows.  
  
1. AWS CodeCommit:  
    This is a fully managed source control service that hosts secure, highly scalable private Git repositories. It allows teams to collaborate on code in a centralized and version-controlled environment, eliminating the need to manage their own version control infrastructure.
2. AWS CodeBuild:  
    This is a fully managed continuous integration service that compiles source code, runs tests, and produces deployable software packages. CodeBuild scales automatically to meet demand, removing the operational burden of provisioning and managing build servers.
3. AWS CodeDeploy:  
    This service automates application deployments to various compute services, including Amazon EC2 instances, AWS Lambda functions, and on-premises servers. CodeDeploy simplifies the deployment process, helps minimize downtime during updates, and supports various deployment strategies like in-place, blue/green, and canary deployments.
4. AWS CodePipeline:  
    This is a fully managed continuous delivery service that automates the release pipelines for fast and reliable application and infrastructure updates. CodePipeline orchestrates the entire CI/CD process, integrating services like CodeCommit, CodeBuild, and CodeDeploy to automate the build, test, and deploy phases based on a defined release model. It can also integrate with third-party tools and services. 

## 2. Differentiate between EC2, Lambda, and ECS/EKS <a name="question2"></a>

1. Amazon EC2 (Elastic Compute Cloud):
    EC2 provides virtual servers (instances) in the cloud, offering the most control over the underlying operating system and software.  
    **Use it when:**  
    - When you require full control over the server environment, including the operating system, specific software installations, and persistent storage.
    - For applications with consistent, predictable workloads or those requiring specialized hardware configurations not available with other services.
    - When migrating existing on-premises applications to the cloud with minimal architectural changes.
2. AWS Lambda:
    Lambda is a serverless compute service that runs code in response to events without provisioning or managing servers. You only pay for the compute time consumed.  
    **Use it when:**  
    - For event-driven applications, such as processing data from S3, responding to API Gateway requests, or handling messages from SQS.
    - For short-lived, stateless functions or microservices where cold starts are acceptable.
    - When cost-efficiency is a primary concern for intermittent or highly variable workloads.
3. Amazon ECS (Elastic Container Service) / EKS (Elastic Kubernetes Service): 
    Both ECS and EKS are container orchestration services for deploying, managing, and scaling containerized applications.  
    - **ECS:** A fully managed container orchestration service that simplifies running Docker containers.
    - **EKS:** A managed Kubernetes service that allows you to run Kubernetes on AWS without managing the Kubernetes control plane.  
    **Use it when:**  
    - **ECS:** When you need a managed solution for running Docker containers and prefer a simpler, AWS-native approach to container orchestration. Suitable for microservices architectures and applications that benefit from containerization without the complexity of managing Kubernetes.
    - **EKS:** When you require the full power and flexibility of Kubernetes, including its extensive ecosystem, portability across environments, and fine-grained control over container deployments. Ideal for complex, large-scale containerized applications or when already using Kubernetes on-premises.

## 3. Discuss AWS CloudWatch, CloudTrail, and setting up effective monitoring and alerting <a name="question3"></a>

AWS CloudWatch and CloudTrail are fundamental services for monitoring, auditing, and ensuring the operational health and security of your AWS environment.  

1. AWS CloudWatch:  
    CloudWatch is a monitoring and observability service that collects and tracks metrics, monitors log files, and sets alarms. It provides a unified view of operational health, enabling you to: 
    - Collect Metrics:  
        Gather performance data from AWS resources (EC2 instances, EBS volumes, RDS databases, etc.) and custom applications.  
    - Monitor Logs:  
        Ingest and analyze log data from various sources, such as EC2 instances, Lambda functions, and CloudTrail.  
    - Create Alarms:  
        Set up automated actions or notifications based on metric thresholds or log patterns, triggering alerts when issues arise.  
    - Build Dashboards:  
        Visualize metrics and logs to gain insights into system performance and resource utilization.  
2. AWS CloudTrail:  
    CloudTrail is an auditing and governance service that records API calls and events within your AWS account. It provides a detailed history of actions taken, including:  
    - API Call Logging:  
        Records every API call made to AWS services, whether initiated by users, roles, or AWS services.
    - Event Logging:  
        Captures events like resource changes, security configuration modifications, and user activity.
    - Auditing and Compliance:  
        Provides a comprehensive audit trail for security analysis, compliance requirements, and troubleshooting operational issues.
    - Security Monitoring:  
        Detects unauthorized or suspicious activity by tracking changes to critical resources and configurations.  
  
**Setting Up Effective Monitoring and Alerting:**  
1. Define Key Metrics and Logs:  
    Identify the critical performance indicators (e.g., CPU utilization, network I/O, error rates) and log sources relevant to your applications and infrastructure.
2. Configure CloudWatch Alarms:  
    - Metric Alarms:  
        Create alarms based on thresholds for key metrics (e.g., high CPU utilization on an EC2 instance, low free storage space on an RDS instance).  
    - Log Alarms:  
        Set up alarms based on patterns in CloudWatch Logs, such as error messages or specific events.  
    - Actions:  
        Configure actions for alarms, including sending notifications (SNS), triggering Auto Scaling actions, or invoking Lambda functions for automated remediation.  
3. Enable CloudTrail:  
    - Create a Trail:  
        Configure a CloudTrail trail to log API calls and events, specifying where to store the logs (typically an S3 bucket).  
    - Integrate with CloudWatch Logs:  
        Send CloudTrail logs to CloudWatch Logs for centralized log management and analysis.  
    - Create CloudWatch Alarms for CloudTrail Events:  
        Set up alarms to detect suspicious or unauthorized activities recorded by CloudTrail, such as changes to security groups or IAM roles.  
4. Build CloudWatch Dashboards:  
    Create custom dashboards to visualize key metrics, logs, and alarm states, providing a consolidated view of your operational health.  
5. Establish Notification Channels:  
    Configure SNS topics or other notification mechanisms to receive alerts from CloudWatch Alarms, ensuring timely awareness of issues.  
6. Regularly Review and Refine:  
    Periodically review your monitoring and alerting configurations, adjusting thresholds, adding new metrics, and refining alarms as your environment evolves.  

## 4. Explain VPCs, subnets, security groups, and network ACLs <a name="question4"></a>

A Virtual Private Cloud (VPC) provides an isolated section of the public cloud for your resources, like a private network. Subnets are logical divisions within a VPC, creating smaller, manageable segments like public or private areas for your resources. Security Groups act as stateful virtual firewalls at the resource level, controlling traffic for individual resources like EC2 instances, while Network Access Control Lists (NACLs) are stateless virtual firewalls that control traffic at the subnet level, offering a separate layer of security.  

1. VPC (Virtual Private Cloud)  
    - Definition:  
        A VPC is a logically isolated, private network within a public cloud environment.  
    - Purpose:   
        It allows you to launch AWS resources in a virtual network that you define, including your own IP address range, routing tables, and network gateways.  
    - Function:  
        Think of it as your own customizable private data center in the cloud.  
2. Subnets  
    - Definition:  
        A subnet is a logical subdivision of a VPC, breaking down the larger network into smaller, distinct network segments.  
    - Purpose:  
        Subnets help organize resources and control network traffic flow. You can create public subnets (with access to the internet) and private subnets (isolated from the internet).  
    - Association:  
        Each subnet in your VPC must be associated with a Network ACL.  
3. Security Groups  
    - Definition:  
        A Security Group is a stateful virtual firewall that controls traffic to and from individual resources, such as EC2 instances.  
    - Function:  
        It acts as a firewall for your instance. You define rules for the traffic allowed in and out.  
    - Stateful nature:  
        Security Groups are stateful, meaning if you allow inbound traffic, the return traffic is automatically allowed, and vice versa.  
4. Network ACLs (NACLs)  
    - Definition:  
        A Network ACL is a stateless virtual firewall that controls traffic at the subnet level.  
    - Function:  
        It allows or denies inbound and outbound traffic for the entire subnet based on explicit rules.  
    - Stateless nature:  
        NACLs are stateless, meaning they evaluate each packet individually. If you allow an inbound request, you must also create an explicit outbound rule for the response to be allowed.  
    - Rule Processing:  
        Rules are processed in order based on their number (e.g., lower numbers are evaluated first).  
    - Role:  
        NACLs provide an additional layer of security to your VPC, working alongside Security Groups.  

## 5. Discuss S3, EBS, and EFS, and their respective use cases <a name="question5"></a>

Amazon S3 is for object storage of large, unstructured data like backups, images, and website content, offering high durability and scalability. Amazon EBS is block storage for single EC2 instances, like a virtual hard drive, ideal for operating systems, databases, and high-performance applications. Amazon EFS is shared file storage, similar to network-attached storage (NAS), that multiple EC2 instances can mount simultaneously, perfect for shared workloads and content management systems.  
  
1. Amazon S3 (Simple Storage Service)
    An object storage service that stores data as objects within buckets, providing seemingly unlimited, highly durable, and scalable storage for unstructured data.  
    **Use Cases:**  
    - Backups and Archives: Storing large volumes of data, including backups, disaster recovery, and archival purposes with low-cost archival options.  
    - Website Hosting: Hosting static website content and other web assets.  
    - Data Lakes and Analytics: Building data lakes for big data analytics, storing raw data for various machine learning tools.  
    - Content Management: Storing and serving content for content management systems.  
2. Amazon EBS (Elastic Block Store)
    Block storage volumes that are attached to a single EC2 instance, functioning as a persistent, low-latency virtual hard drive.  
    **Use Cases:**  
    - Operating Systems & Databases: Providing storage for EC2 instances, including hosting the operating system and running databases.  
    - High-Performance Applications: Delivering high-performance, low-latency block storage for demanding applications that require fast data access.  
    - Single-Instance Storage: Used for workloads that need storage for a single, dedicated EC2 instance.  
3. Amazon EFS (Elastic File System)
    A managed, scalable file system that multiple EC2 instances or other AWS services can access concurrently. It functions as a shared drive.  
    **Use Cases:**  
    - Shared File Access: Providing a shared file system for multiple EC2 instances or containers to access concurrently.  
    - Content Management & Web Servers: Supporting content management systems and web servers that require shared storage.  
    - Big Data and Analytics: Facilitating big data analytics and other workloads that require concurrent file system access.  
    - Lift-and-Shift Applications: Ideal for lifting and shifting existing applications that rely on shared file systems.  

## 6. Explain services like RDS, DynamoDB, and Aurora <a name="question6"></a>

Amazon Web Services (AWS) offers various managed database services designed to simplify database management and scalability. Among these, Amazon RDS, Amazon DynamoDB, and Amazon Aurora are prominent, each serving distinct use cases.  
  
1. Amazon RDS (Relational Database Service)  
    Amazon RDS is a managed relational database service that supports several popular database engines, including MySQL, PostgreSQL, Oracle, SQL Server, and MariaDB. RDS simplifies the setup, operation, and scaling of relational databases in the cloud by automating administrative tasks such as hardware provisioning, database setup, patching, and backups. It provides a cost-efficient and scalable solution for traditional relational database workloads.

2. mazon DynamoDB  
    Amazon DynamoDB is a fully managed, serverless NoSQL database service that supports key-value and document data models. It is designed for applications requiring high performance at any scale, offering single-digit millisecond latency at any throughput. DynamoDB automatically scales to handle varying loads and provides built-in security, backup and restore capabilities, and in-memory caching with DynamoDB Accelerator (DAX). It is well-suited for use cases like mobile applications, gaming, ad tech, and IoT, where flexible schema and extreme scalability are crucial.

3. Amazon Aurora  
    Amazon Aurora is a fully managed, MySQL and PostgreSQL-compatible relational database engine built for the cloud. It combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open-source databases. Aurora's innovative architecture separates storage and compute, allowing for independent scaling and enhanced performance. It offers high availability, automated backup and recovery, and advanced features like Aurora Serverless for on-demand, auto-scaling capacity. Aurora is ideal for demanding relational database workloads requiring high performance, scalability, and availability, often serving as an upgrade path for existing MySQL or PostgreSQL applications.

## 7. Configuration Management: Discuss tools like AWS Systems Manager or third-party tools like Ansible <a name="question7"></a>

Configuration management tools automate the process of maintaining consistency in the configuration of systems, servers, and applications across an IT infrastructure. This ensures that systems are configured correctly, securely, and uniformly, reducing manual errors and improving efficiency.
  
1. AWS Systems Manager  
    AWS Systems Manager is a collection of capabilities within AWS that helps manage and automate operational tasks across AWS resources and on-premises instances. For configuration management, key components include:  
    - State Manager:  
        Maintains a defined state for instances by applying configurations and ensuring compliance.
    - Parameter Store:  
        Securely stores and manages configuration data and secrets.
    - Run Command:  
        Remotely executes commands on instances for tasks like software installation or updates.
    - Patch Manager:  
        Automates the patching process for operating systems and applications.  

    **Advantages:** Deep integration with the AWS ecosystem, serverless capabilities for many features, and centralized management within the AWS console.
  
    **Considerations:** Primarily focused on AWS environments, though it can manage hybrid environments with on-premises instances.

2. Third-Party Tools: Ansible  
    Ansible is an open-source automation engine developed by Red Hat, widely used for configuration management, application deployment, and orchestration.  
    - Agentless:  
        Operates over SSH (or WinRM for Windows), eliminating the need for agents on target machines.
    - YAML-based Playbooks:  
        Uses human-readable YAML files (playbooks) to define automation tasks and desired states.
    - Idempotent:  
        Ensures that applying a configuration multiple times yields the same result, preventing unintended changes.
    - Extensible:  
        Supports a vast library of modules for various tasks and platforms, including cloud providers like AWS.
  
    **Advantages:** Simplicity and readability of playbooks, agentless architecture, strong community support, and versatility across diverse environments (cloud, on-premises, network devices).
  
    **Considerations:** Requires Python on managed nodes for some modules, and larger-scale deployments might benefit from Ansible Tower (or AWX, the open-source upstream project) for centralized management and reporting.

3. Other Notable Third-Party Tools
    - Puppet and Chef:  
        Agent-based tools that use a master-agent architecture and declarative languages (Ruby-based DSLs) for defining infrastructure as code. Known for their robust features and enterprise-grade capabilities.
    - SaltStack:  
        Agent-based tool known for its high-speed execution and scalability, using Python-based "states" and "formulas."
    - Terraform:  
        While primarily an Infrastructure as Code (IaC) tool for provisioning infrastructure, it can be used in conjunction with configuration management tools to provision and then configure resources.

## 8.  <a name="question8"></a>

## 9.  <a name="question9"></a>

## 10. NoSQL DB <a name="question10"></a>

A NoSQL database, also known as a non-relational or "not only SQL" database, is a type of database system that differs from traditional relational databases by offering a flexible schema and storing data in a non-tabular format. NoSQL databases are designed to handle large volumes of diverse and rapidly changing data, particularly unstructured or semi-structured data, and are known for their scalability and high performance. 
  
**Key Characteristics of NoSQL Databases:**  
1. Non-Relational:  
    Unlike relational databases that store data in tables with predefined schemas, NoSQL databases use various data models like document, key-value, graph, or wide-column stores. 
2. Flexible Schema:  
    NoSQL databases offer a flexible schema, meaning the structure of the data can change easily without requiring major schema updates, making them adaptable to evolving data requirements. 
3. Scalability:  
    NoSQL databases are designed for horizontal scalability, allowing them to easily distribute data across multiple servers or clusters to handle large datasets and high traffic loads. 
4. Performance:  
    NoSQL databases are optimized for specific data models and workloads, often providing faster read and write operations compared to traditional relational databases, especially in scenarios with large datasets and high user traffic. 
5. Various Data Models:  
    NoSQL databases support different data models, including: 
    - Document databases:  
        Store data as documents (e.g., JSON, XML) with flexible schemas. 
    - Key-value stores:  
        Store data as key-value pairs, where each value is associated with a unique key. 
    - Graph databases:  
        Store data as nodes and edges, representing relationships between entities. 
    - Wide-column stores:  
        Store data in columns, allowing for flexible schemas and efficient storage of large datasets.  
6. Distributed Systems:  
    NoSQL databases are often designed as distributed systems, with data replicated across multiple machines to ensure high availability and fault tolerance. 
  
**When to Use NoSQL Databases:**  
- Big Data Applications:  
    Handling massive amounts of data with diverse formats and structures. 
- Real-Time Applications:  
    Providing fast data access and low latency for real-time analytics and user interactions. 
- Web Applications:  
    Managing user data, session information, and content in dynamic web environments. 
- Mobile Applications:  
    Storing and retrieving data for mobile apps with varying data structures and user loads. 
- Internet of Things (IoT) Applications:  
    Managing data from connected devices with diverse data streams and formats. 
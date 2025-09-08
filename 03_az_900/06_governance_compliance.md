# Azure Tools for Governance and Compliance

## Table of contents
1. [Microsoft Purview](#question1)
2. [Azure Policy](#question2)
3. [Resource locks](#question3)
4. [Service Trust portal](#question4)

## 1. Microsoft Purview <a name="question1"></a>

Microsoft Purview is a family of data governance, risk, and compliance solutions that helps you get a single, unified view into your data. Microsoft Purview brings insights about your on-premises, multicloud, and software-as-a-service data together.  

- Automated data discovery
- Sensitive data classification
- End-to-end data lineage

1. Microsoft Purview risk and compliance solutions:  
    Microsoft Teams, OneDrive, and Exchange are just some of the Microsoft 365 services that Microsoft Purview uses to help manage and monitor your data.  
    - Protect sensitive data across clouds, apps, and devices.
    - Identify data risks and manage regulatory compliance requirements.
    - Get started with regulatory compliance.
2. Unified data governance:  
    Microsoft Purview has robust, unified data governance solutions that help manage your on-premises, multicloud, and software as a service data. Microsoft Purview’s robust data governance capabilities enable you to manage your data stored in Azure, SQL and Hive databases, locally, and even in other clouds like Amazon S3.  
    - Create an up-to-date map of your entire data estate that includes data classification and end-to-end lineage.
    - Identify where sensitive data is stored in your estate.
    - Create a secure environment for data consumers to find valuable data.
    - Generate insights about how your data is stored and used.
    - Manage access to the data in your estate securely and at scale.

## 2. Azure Policy <a name="question2"></a>

Azure Policy is a service in Azure that enables you to create, assign, and manage policies that control or audit your resources. These policies enforce different rules across your resource configurations so that those configurations stay compliant with corporate standards.  

Azure Policy enables you to define both individual policies and groups of related policies, known as initiatives. Azure Policy evaluates your resources and highlights resources that aren't compliant with the policies you've created. Azure Policy can also prevent noncompliant resources from being created.  

Azure Policies are inherited  
Azure Policy also integrates with Azure DevOps by applying any continuous integration and delivery pipeline policies that pertain to the pre-deployment and post-deployment phases of your applications.  

An Azure Policy **initiative** is a way of grouping related policies together. The initiative definition contains all of the policy definitions to help track your compliance state for a larger goal.  

Under this initiative, the following policy definitions are included:
- **Monitor unencrypted SQL Database in Security Center:** This policy monitors for unencrypted SQL databases and servers.
- **Monitor OS vulnerabilities in Security Center:** This policy monitors servers that don't satisfy the configured OS vulnerability baseline.
- **Monitor missing Endpoint Protection in Security Center:** This policy monitors for servers that don't have an installed endpoint protection agent.

## 3. Resource locks <a name="question3"></a>

A resource lock prevents resources from being accidentally deleted or changed.  
Resource locks prevent resources from being deleted or updated, depending on the type of lock. Resource locks can be applied to individual resources, resource groups, or even an entire subscription. Resource locks are inherited, meaning that if you place a resource lock on a resource group, all of the resources within the resource group will also have the resource lock applied.  

- **Delete** means authorized users can still read and modify a resource, but they can't delete the resource.
- **ReadOnly** means authorized users can read a resource, but they can't delete or update the resource. Applying this lock is similar to restricting all authorized users to the permissions granted by the Reader role.

## 4. Service Trust portal <a name="question4"></a>

The Microsoft Service Trust Portal is a portal that provides access to various content, tools, and other resources about Microsoft security, privacy, and compliance practices.  

The Service Trust Portal contains details about Microsoft's implementation of controls and processes that protect our cloud services and the customer data therein.  
https://servicetrust.microsoft.com/

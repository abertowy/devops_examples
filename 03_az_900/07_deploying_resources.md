# Managing and Deploying Azure resources

## Table of contents
1. [Azure Resource Manager](#question1)
2. [Monitoring: Azure Advisor](#question2)
3. [Azure Service Health](#question3)
4. [Azure Monitor](#question4)
5. [Some](#question5)
6. [Some](#question6)
7. [Some](#question7)
8. [Some](#question8)
9. [Some](#question9)
10. [Some](#question10)

## 1. Azure Resource Manager <a name="question1"></a>

Azure Resource Manager (ARM) is the deployment and management service for Azure. It provides a management layer that enables you to create, update, and delete resources in your Azure account. Anytime you do anything with your Azure resources, ARM is involved.  

Manage your infrastructure through declarative templates rather than scripts. A Resource Manager template is a JSON file that defines what you want to deploy to Azure.  

**ARM templates (JSON):**  
- Declarative syntax:  
    ARM templates allow you to create and deploy an entire Azure infrastructure declaratively. Declarative syntax means you declare what you want to deploy but don’t need to write the actual programming commands and sequence to deploy the resources.
- Repeatable results:  
    Repeatedly deploy your infrastructure throughout the development lifecycle and have confidence your resources are deployed in a consistent manner. You can use the same ARM template to deploy multiple dev/test environments, knowing that all the environments are the same.
- Orchestration:  
    You don't have to worry about the complexities of ordering operations. Azure Resource Manager orchestrates the deployment of interdependent resources, so they're created in the correct order. When possible, Azure Resource Manager deploys resources in parallel, so your deployments finish faster than serial deployments. You deploy the template through one command, rather than through multiple imperative commands.
- Modular files:  
    You can break your templates into smaller, reusable components and link them together at deployment time. You can also nest one template inside another template. For example, you could create a template for a VM stack, and then nest that template inside of templates that deploy entire environments, and that VM stack will consistently be deployed in each of the environment templates.
- Extensibility:  
    With deployment scripts, you can add PowerShell or Bash scripts to your templates. The deployment scripts extend your ability to set up resources during deployment. A script can be included in the template or stored in an external source and referenced in the template. Deployment scripts give you the ability to complete your end-to-end environment setup in a single ARM template.

**Bicep** is a language that uses declarative syntax to deploy Azure resources. A Bicep file defines the infrastructure and configuration. Then, ARM deploys that environment based on your Bicep file. While similar to an ARM template, which is written in JSON, Bicep files tend to use a simpler, more concise style.  
**Bicep:**  
- Support for all resource types and API versions:  
    Bicep immediately supports all preview and GA versions for Azure services. As soon as a resource provider introduces new resource types and API versions, you can use them in your Bicep file. You don't have to wait for tools to be updated before using the new services.
- Simple syntax:  
    When compared to the equivalent JSON template, Bicep files are more concise and easier to read. Bicep requires no previous knowledge of programming languages. Bicep syntax is declarative and specifies which resources and resource properties you want to deploy.
- Repeatable results:  
    Repeatedly deploy your infrastructure throughout the development lifecycle and have confidence your resources are deployed in a consistent manner. Bicep files are idempotent, which means you can deploy the same file many times and get the same resource types in the same state. You can develop one file that represents the desired state, rather than developing lots of separate files to represent updates.
- Orchestration:  
    You don't have to worry about the complexities of ordering operations. Resource Manager orchestrates the deployment of interdependent resources so they're created in the correct order. When possible, Resource Manager deploys resources in parallel so your deployments finish faster than serial deployments. You deploy the file through one command, rather than through multiple imperative commands.
- Modularity:  
    You can break your Bicep code into manageable parts by using modules. The module deploys a set of related resources. Modules enable you to reuse code and simplify development. Add the module to a Bicep file anytime you need to deploy those resources.

## 2. Monitoring: Azure Advisor <a name="question2"></a>

Azure Advisor evaluates your Azure resources and makes recommendations to help improve reliability, security, and performance, achieve operational excellence, and reduce costs. Azure Advisor is designed to help you save time on cloud optimization. The recommendation service includes suggested actions you can take right away, postpone, or dismiss.  

## 3. Azure Service Health <a name="question3"></a>

Azure Service Health helps you keep track of Azure resource, both your specifically deployed resources and the overall status of Azure. Azure service health does this by combining three different Azure services:  
- **Azure Status** is a broad picture of the status of Azure globally. Azure status informs you of **service outages** in Azure on the Azure Status page. The page is a **global view** of the health of all Azure services across all Azure regions. It’s a good reference for incidents with widespread impact.
- **Service Health** provides a narrower view of Azure services and regions. It focuses on the **Azure services and regions you're using**. This is the best place to look for service impacting communications about outages, planned maintenance activities, and other health advisories because the authenticated Service Health experience knows which services and resources you currently use. You can even set up Service Health alerts to notify you when service issues, planned maintenance, or other changes may affect the Azure services and regions you use.
- **Resource Health** is a tailored view of your **actual Azure resources**. It provides information about the health of your individual cloud resources, such as a specific virtual machine instance. Using `Azure Monitor`, you can also configure alerts to notify you of availability changes to your cloud resources.

## 4. Azure Monitor <a name="question4"></a>

Azure Monitor is a platform for collecting data on your resources, analyzing that data, visualizing the information, and even acting on the results. Azure Monitor can monitor Azure resources, your on-premises resources, and even multi-cloud resources like virtual machines hosted with a different cloud provider.  

1. Azure Log Analytics:  
    Azure Log Analytics is the tool in the Azure portal where you’ll write and run log queries on the data gathered by Azure Monitor.
2. Azure Monitor Alerts:  
    Azure Monitor Alerts are an automated way to stay informed when Azure Monitor detects a threshold being crossed. You set the alert conditions, the notification actions, and then Azure Monitor Alerts notifies when an alert is triggered. Depending on your configuration, Azure Monitor Alerts can also attempt corrective action.
3. Application Insights:  
    Application Insights, an Azure Monitor feature, monitors your web applications. Application Insights is capable of monitoring applications that are running in Azure, on-premises, or in a different cloud environment.  
    SDK or Application Insights agent.  
    Monitors:  
    - Request rates, response times, and failure rates
    - Dependency rates, response times, and failure rates, to show whether external services are slowing down performance
    - Page views and load performance reported by users' browsers
    - AJAX calls from web pages, including rates, response times, and failure rates
    - User and session counts
    - Performance counters from Windows or Linux server machines, such as CPU, memory, and network usage

## 5.  <a name="question5"></a>

## 6.  <a name="question6"></a>

## 7.  <a name="question7"></a>

## 8.  <a name="question8"></a>

## 9.  <a name="question9"></a>

## 10.  <a name="question10"></a>
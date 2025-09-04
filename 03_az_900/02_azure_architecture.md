# Basics

## Table of contents
1. [What is Microsoft Azure](#question1)
2. [Azure physical infrastructure](#question2)
3. [Azure management infrastructure](#question3)
4. [Azure virtual machines](#question4)
5. [Azure virtual desktop](#question5)
6. [Azure containers](#question6)
7. [Azure functions](#question7)
8. [Azure App Service](#question8)
9. [Azure virtual networking](#question9)
10. [Azure virtual private networks](#question10)
11. [Azure ExpressRoute](#question11)
12. [Azure DNS](#question12)

## 1. What is Microsoft Azure <a name="question1"></a>

Azure is a continually expanding set of cloud services that help you meet current and future business challenges. Azure gives you the freedom to build, manage, and deploy applications on a massive global network using your favorite tools and frameworks.  
  
- **Bring ideas to life:** Build on a trusted platform to advance your organization with industry-leading AI and cloud services.
- **Seamlessly unify:** Efficiently manage all your infrastructure, data, analytics, and AI solutions across an integrated platform.
- **Innovate on trust:** Rely on trusted technology from a partner who's dedicated to security and responsibility.

## 2. Azure physical infrastructure <a name="question2"></a>

1. Regions:
    A region is a geographical area on the planet that contains at least one, but potentially multiple datacenters that are nearby and networked together with a low-latency network. Azure intelligently assigns and controls the resources within each region to ensure workloads are appropriately balanced.
2. Availability Zones:
    Availability zones are physically separate datacenters within an Azure region. Each availability zone is made up of one or more datacenters equipped with independent power, cooling, and networking. An availability zone is set up to be an isolation boundary. If one zone goes down, the other continues working. Availability zones are connected through high-speed, private fiber-optic networks.  
    You can use availability zones to run mission-critical applications and build high-availability into your application architecture by co-locating your compute, storage, networking, and data resources within an availability zone and replicating in other availability zones. Keep in mind that there could be a cost to duplicating your services and transferring data between availability zones.  
    - **Zonal services:** You pin the resource to a specific zone (for example, VMs, managed disks, IP addresses).
    - **Zone-redundant services:** The platform replicates automatically across zones (for example, zone-redundant storage, SQL Database).
    - **Non-regional services:** Services are always available from Azure geographies and are resilient to zone-wide outages as well as region-wide outages.
3. Region pairs:
    Most Azure regions are paired with another region within the same geography (such as US, Europe, or Asia) at least 300 miles away. This approach allows for the replication of resources across a geography that helps reduce the likelihood of interruptions because of events such as natural disasters, civil unrest, power outages, or physical network outages that affect an entire region. For example, if a region in a pair was affected by a natural disaster, services would automatically fail over to the other region in its region pair.  
    Advantages:  
    - If an extensive Azure outage occurs, one region out of every pair is prioritized to make sure at least one is restored as quickly as possible for applications hosted in that region pair.
    - Planned Azure updates are rolled out to paired regions one region at a time to minimize downtime and risk of application outage.
    - Data continues to reside within the same geography as its pair (except for Brazil South) for tax- and law-enforcement jurisdiction purposes.
4. Sovereign Regions:
    Sovereign regions are instances of Azure that are isolated from the main instance of Azure. You may need to use a sovereign region for compliance or legal purposes.
    - US DoD Central, US Gov Virginia, US Gov Iowa and more: These regions are physical and logical network-isolated instances of Azure for U.S. government agencies and partners. These datacenters are operated by screened U.S. personnel and include additional compliance certifications.
    - China East, China North, and more: These regions are available through a unique partnership between Microsoft and 21Vianet, whereby Microsoft doesn't directly maintain the datacenters.

## 3. Azure management infrastructure <a name="question3"></a>

1. Azure resources and resource groups:
    A resource is the basic building block of Azure. Anything you create, provision, deploy, etc. is a resource. Virtual Machines (VMs), virtual networks, databases, cognitive services, etc. are all considered resources within Azure.  
    Resource groups are simply groupings of resources. When you create a resource, you’re required to place it into a resource group. While a resource group can contain many resources, a single resource can only be in one resource group at a time.  
    Resource groups can't be nested, meaning you can’t put resource group B inside of resource group A.  
    When you apply an action to a resource group, that action will apply to all the resources within the resource group.  
    It may be best to group resources based on the access schema, and then assign access at the resource group level.  
2. Azure subscriptions:
    In Azure, subscriptions are a unit of management, billing, and scale. Similar to how resource groups are a way to logically organize resources, subscriptions allow you to logically organize your resource groups and facilitate billing.  
    A subscription provides you with authenticated and authorized access to Azure products and services.  
    Subscription boundaries:  
    - Billing boundary: This subscription type determines how an Azure account is billed for using Azure. You can create multiple subscriptions for different types of billing requirements. Azure generates separate billing reports and invoices for each subscription so that you can organize and manage costs.
    - Access control boundary: Azure applies access-management policies at the subscription level, and you can create separate subscriptions to reflect different organizational structures. An example is that within a business, you have different departments to which you apply distinct Azure subscription policies. This billing model allows you to manage and control access to the resources that users provision with specific subscriptions.
3. Azure management groups:
    Azure management groups provide a level of scope above subscriptions. You organize subscriptions into containers called management groups and apply governance conditions to the management groups. All subscriptions within a management group automatically inherit the conditions applied to the management group, the same way that resource groups inherit settings from subscriptions and resources inherit from resource groups. Management groups give you enterprise-grade management at a large scale, no matter what type of subscriptions you might have. Management groups can be nested.  
    Examples:  
    - Create a hierarchy that applies a policy
    - Provide user access to multiple subscriptions.

    Important facts about management groups:  
    - 10,000 management groups can be supported in a single directory.
    - A management group tree can support up to six levels of depth. This limit doesn't include the root level or the subscription level.
    - Each management group and subscription can support only one parent.

## 4. Azure virtual machines <a name="question4"></a>

VMs provide infrastructure as a service (IaaS) in the form of a virtualized server and can be used in many ways.  
VMs are an ideal choice when you need:
- Total control over the operating system (OS).
- The ability to run custom software.
- To use custom hosting configurations.

1. Virtual machine scale sets:  
    Virtual machine scale sets let you create and manage a group of identical, load-balanced VMs. If you simply created multiple VMs with the same purpose, you’d need to ensure they were all configured identically and then set up network routing parameters to ensure efficiency. You’d also have to monitor the utilization to determine if you need to increase or decrease the number of VMs.  

    Instead, with virtual machine scale sets, Azure automates most of that work. Scale sets allow you to centrally manage, configure, and update a large number of VMs in minutes. The number of VM instances can automatically increase or decrease in response to demand, or you can set it to scale based on a defined schedule. Virtual machine scale sets also automatically deploy a load balancer to make sure that your resources are being used efficiently. With virtual machine scale sets, you can build large-scale services for areas such as compute, big data, and container workloads.  

2. Virtual machine availability sets:  
    Availability sets are designed to ensure that VMs stagger updates and have varied power and network connectivity, preventing you from losing all your VMs with a single network or power failure.
    - Update domain: The update domain groups VMs that can be rebooted at the same time. This setup allows you to apply updates while knowing that only one update domain grouping is offline at a time. All of the machines in one update domain update. An update group going through the update process is given a 30-minute time to recover before maintenance on the next update domain starts.
    - Fault domain: The fault domain groups your VMs by common power source and network switch. By default, an availability set splits your VMs across up to three fault domains. This helps protect against a physical power or networking failure by having VMs in different fault domains (thus being connected to different power and networking resources).

**When to use VMs:**
- During testing and development.
- When running applications in the cloud.
- When extending your datacenter to the cloud
- During disaster recovery.

VMs are also an excellent choice when you move from a physical server to the cloud (also known as lift and shift). You can create an image of the physical server and host it within a VM with little or no changes.

```bash
az vm create \
--resource-group "azure_devops_dft" \
--name my-vm \
--public-ip-sku Standard \
--image Ubuntu2204 \
--admin-username azureuser \
--generate-ssh-keys
```
Returns:
```JSON
{
  "fqdns": "",
  "id": "/subscriptions/279c0dbc-da5c-440d-a7ff-c83c6f05bcfb/resourceGroups/azure_devops_dft/providers/Microsoft.Compute/virtualMachines/my-vm",
  "location": "austriaeast",
  "macAddress": "7C-1E-52-8E-27-59",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "68.210.38.232",
  "resourceGroup": "azure_devops_dft"
}
```
  
-------
  
```bash
az vm extension set \
--resource-group "azure_devops_dft" \
--vm-name my-vm \
--name customScript \
--publisher Microsoft.Azure.Extensions \
--version 2.1 \
--settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' \
--protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```
Returns:
```JSON
{
  "autoUpgradeMinorVersion": true,
  "id": "/subscriptions/279c0dbc-da5c-440d-a7ff-c83c6f05bcfb/resourceGroups/azure_devops_dft/providers/Microsoft.Compute/virtualMachines/my-vm/extensions/customScript",
  "location": "austriaeast",
  "name": "customScript",
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.Extensions",
  "resourceGroup": "azure_devops_dft",
  "settings": {
    "fileUris": [
      "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"
    ]
  },
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "2.1",
  "typePropertiesType": "customScript"
}
```

## 5. Azure virtual desktop <a name="question5"></a>

Azure Virtual Desktop is a desktop and application virtualization service that runs on the cloud. It enables you to use a cloud-hosted version of Windows from any location.
  
Azure Virtual Desktop provides centralized security management for users' desktops with Microsoft Entra ID. You can enable multifactor authentication to secure user sign-ins. You can also secure access to data by assigning granular role-based access controls (RBACs) to users.
  
With Azure Virtual Desktop, the data and apps are separated from the local hardware. The actual desktop and apps are running in the cloud, meaning the risk of confidential data being left on a personal device is reduced. Additionally, user sessions are isolated in both single and multi-session environments.
  
Azure Virtual Desktop lets you use Windows 10 or Windows 11 Enterprise multi-session, the only Windows client-based operating system that enables multiple concurrent users on a single VM.

## 6. Azure containers <a name="question6"></a>

Containers are a virtualization environment. Much like running multiple virtual machines on a single physical host, you can run multiple containers on a single physical or virtual host. Unlike virtual machines, you don't manage the operating system for a container. Virtual machines appear to be an instance of an operating system that you can connect to and manage. Containers are lightweight and designed to be created, scaled out, and stopped dynamically. It's possible to create and deploy virtual machines as application demand increases, but containers are a lighter weight, more agile method. Containers are designed to allow you to respond to changes on demand. With containers, you can quickly restart if there's a crash or hardware interruption.
  
**Azure Container Instances** offer the fastest and simplest way to run a container in Azure; without having to manage any virtual machines or adopt any additional services. Azure Container Instances are a platform as a service (PaaS) offering. Azure Container Instances allow you to upload your containers and then the service runs the containers for you.
  
**Azure Kubernetes Service (AKS)** is a container orchestration service. An orchestration service manages the lifecycle of containers. When you're deploying a fleet of containers, AKS can make fleet management simpler and more efficient.
  
Containers are often used to create solutions by using a microservice architecture. This architecture is where you break solutions into smaller, independent pieces. For example, you might split a website into a container hosting your front end, another hosting your back end, and a third for storage. This split allows you to separate portions of your app into logical sections that can be maintained, scaled, or updated independently.
  
Imagine your website back-end reaches capacity, but the front end and storage aren't stressed. With containers, you could scale the back-end separately to improve performance. If something necessitated such a change, you could also choose to change the storage service or modify the front end without impacting any of the other components.

## 7. Azure functions <a name="question7"></a>

Azure Functions is an event-driven, serverless compute option that doesn’t require maintaining virtual machines or containers. If you build an app using VMs or containers, those resources have to be “running” in order for your app to function. With Azure Functions, an event wakes the function, alleviating the need to keep resources provisioned when there are no events.

Functions are a key component of serverless computing. They're also a general compute platform for running any type of code. If the needs of the developer's app change, you can deploy the project in an environment that isn't serverless. This flexibility allows you to manage scaling, run on virtual networks, and even completely isolate the functions.

**Benefits:**
- you're only concerned about the code running your service and not about the underlying platform or infrastructure.
- Functions are commonly used when you need to perform work in response to an event (often via a REST request), timer, or message from another Azure service, and when that work can be completed quickly, within seconds or less.
- Functions scale automatically based on demand, so they may be a good choice when demand is variable
- Azure Functions runs your code when it triggers and automatically deallocates resources when the function is finished. In this model, Azure only charges you for the CPU time used while your function runs.
- Functions can be either stateless or stateful
    - **Stateless** (the default): behave as if they restart every time they respond to an event.
    - **Stateful** (called Durable Functions): a context is passed through the function to track prior activity.

## 8. Azure App Service <a name="question8"></a>

App Service enables you to build and host web apps, background jobs, mobile back-ends, and RESTful APIs in the programming language of your choice without managing infrastructure. It offers automatic scaling and high availability. App Service supports Windows and Linux. It enables automated deployments from GitHub, Azure DevOps, or any Git repo to support a continuous deployment model.  

Azure App Service is a robust hosting option that you can use to host your apps in Azure. Azure App Service lets you focus on building and maintaining your app, and Azure focuses on keeping the environment up and running.  

App Service handles most of the infrastructure decisions you deal with in hosting web-accessible apps:
- Deployment and management are integrated into the platform.
- Endpoints can be secured.
- Sites can be scaled quickly to handle high traffic loads.
- The built-in load balancing and traffic manager provide high availability.

Types of app services:
1. **Web apps:**  
    App Service includes full support for hosting web apps by using ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP, or Python. You can choose either Windows or Linux as the host operating system.
2. **API apps:**  
    Much like hosting a website, you can build REST-based web APIs by using your choice of language and framework. You get full Swagger support and the ability to package and publish your API in Azure Marketplace. The produced apps can be consumed from any HTTP- or HTTPS-based client.
3. **WebJobs:**  
    You can use the WebJobs feature to run a program (.exe, Java, PHP, Python, or Node.js) or script (.cmd, .bat, PowerShell, or Bash) in the same context as a web app, API app, or mobile app. They can be scheduled or run by a trigger. WebJobs are often used to run background tasks as part of your application logic.
4. **Mobile apps:**  
    Use the Mobile Apps feature of App Service to quickly build a back end for iOS and Android apps. With just a few actions in the Azure portal, you can:
    - Store mobile app data in a cloud-based SQL database.
    - Authenticate customers against common social providers, such as MSA, Google, X, and Facebook.
    - Send push notifications.
    - Execute custom back-end logic in C# or Node.js.

## 9. Azure virtual networking <a name="question9"></a>

Azure virtual networks provide the following key networking capabilities:
- Isolation and segmentation
- Internet communications
- Communicate between Azure resources
- Communicate with on-premises resources
- Route network traffic
- Filter network traffic
- Connect virtual networks

Azure virtual networking supports both public and private endpoints to enable communication between external or internal resources with other internal resources.
- Public endpoints have a public IP address and can be accessed from anywhere in the world.
- Private endpoints exist within a virtual network and have a private IP address from within the address space of that virtual network.

```bash
IPADDRESS="$(az vm list-ip-addresses \
  --resource-group "azure_devops_dft" \
  --name my-vm \
  --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
  --output tsv)"

echo $IPADDRESS
68.210.38.232

curl --connect-timeout 5 http://$IPADDRESS
curl: (28) Connection timeout after 5001 ms

az network nsg list \
  --resource-group "azure_devops_dft" \
  --query '[].name' \
  --output tsv

# returns: my-vmNSG
```
```bash
az network nsg rule list \
  --resource-group "azure_devops_dft" \
  --nsg-name my-vmNSG
```
Returns:
```JSON
[
  {
    "access": "Allow",
    "destinationAddressPrefix": "*",
    "destinationAddressPrefixes": [],
    "destinationPortRange": "22",
    "destinationPortRanges": [],
    "direction": "Inbound",
    "etag": "W/\"47d32a13-0760-44aa-9676-4080daa7becf\"",
    "id": "/subscriptions/279c0dbc-da5c-440d-a7ff-c83c6f05bcfb/resourceGroups/azure_devops_dft/providers/Microsoft.Network/networkSecurityGroups/my-vmNSG/securityRules/default-allow-ssh",
    "name": "default-allow-ssh",
    "priority": 1000,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "azure_devops_dft",
    "sourceAddressPrefix": "*",
    "sourceAddressPrefixes": [],
    "sourcePortRange": "*",
    "sourcePortRanges": [],
    "type": "Microsoft.Network/networkSecurityGroups/securityRules"
  }
]
```
  
------
  
```bash
az network nsg rule list \
  --resource-group "azure_devops_dft" \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table
```
Returns:
```bash
Name               Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow
```
  
-----
  
```bash
az network nsg rule create \
  --resource-group "azure_devops_dft" \
  --nsg-name my-vmNSG \
  --name allow-http \
  --protocol tcp \
  --priority 100 \
  --destination-port-range 80 \
  --access Allow
```
Returns:
```JSON
{
  "access": "Allow",
  "destinationAddressPrefix": "*",
  "destinationAddressPrefixes": [],
  "destinationPortRange": "80",
  "destinationPortRanges": [],
  "direction": "Inbound",
  "etag": "W/\"97b226d6-22e1-42a8-84a4-a3411fa55cb4\"",
  "id": "/subscriptions/279c0dbc-da5c-440d-a7ff-c83c6f05bcfb/resourceGroups/azure_devops_dft/providers/Microsoft.Network/networkSecurityGroups/my-vmNSG/securityRules/allow-http",
  "name": "allow-http",
  "priority": 100,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "azure_devops_dft",
  "sourceAddressPrefix": "*",
  "sourceAddressPrefixes": [],
  "sourcePortRange": "*",
  "sourcePortRanges": [],
  "type": "Microsoft.Network/networkSecurityGroups/securityRules"
}
```
  
-----
  
```bash
az network nsg rule list \
  --resource-group "azure_devops_dft" \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table
```
Returns:
```bash
Name               Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow
allow-http         100         80      Allow
```
```bash
curl --connect-timeout 5 http://$IPADDRESS
# <html><body><h2>Welcome to Azure! My name is my-vm.</h2></body></html>
```
```bash
az group delete --name azure_devops_dft
```

## 10. Azure virtual private networks <a name="question10"></a>

A virtual private network (VPN) uses an encrypted tunnel within another network. VPNs are typically deployed to connect two or more trusted private networks to one another over an untrusted network (typically the public internet). Traffic is encrypted while traveling over the untrusted network to prevent eavesdropping or other attacks. VPNs can enable networks to safely and securely share sensitive information.  

1. **VPN gateways:**  
    A VPN gateway is a type of virtual network gateway. Azure VPN Gateway instances are deployed in a dedicated subnet of the virtual network and enable the following connectivity:
    - Connect on-premises datacenters to virtual networks through a site-to-site connection.
    - Connect individual devices to virtual networks through a point-to-site connection.
    - Connect virtual networks to other virtual networks through a network-to-network connection.

    All data transfer is encrypted inside a private tunnel as it crosses the internet. You can deploy only one VPN gateway in each virtual network. However, you can use one gateway to connect to multiple locations, which includes other virtual networks or on-premises datacenters.

    - Policy-based VPN gateways specify statically the IP address of packets that should be encrypted through each tunnel. This type of device evaluates every data packet against those sets of IP addresses to choose the tunnel where that packet is going to be sent through.
    - In Route-based gateways, IPSec tunnels are modeled as a network interface or virtual tunnel interface. IP routing (either static routes or dynamic routing protocols) decides which one of these tunnel interfaces to use when sending each packet. Route-based VPNs are the preferred connection method for on-premises devices. They're more resilient to topology changes such as the creation of new subnets.

    Use a route-based VPN gateway if you need any of the following types of connectivity:
    - Connections between virtual networks
    - Point-to-site connections
    - Multisite connections
    - Coexistence with an Azure ExpressRoute gateway

2. **High-availability scenarios:**  
    If you’re configuring a VPN to keep your information safe, you also want to be sure that it’s a highly available and fault tolerant VPN configuration. There are a few ways to maximize the resiliency of your VPN gateway.

    - **Active/standby:**  
        By default, VPN gateways are deployed as two instances in an active/standby configuration, even if you only see one VPN gateway resource in Azure. When planned maintenance or unplanned disruption affects the active instance, the standby instance automatically assumes responsibility for connections without any user intervention. Connections are interrupted during this failover, but they typically restore within a few seconds for planned maintenance and within 90 seconds for unplanned disruptions.
    - **Active/active:**  
        With the introduction of support for the BGP routing protocol, you can also deploy VPN gateways in an active/active configuration. In this configuration, you assign a unique public IP address to each instance. You then create separate tunnels from the on-premises device to each IP address. You can extend the high availability by deploying an additional VPN device on-premises.
    - **ExpressRoute failover:**  
        ExpressRoute circuits have resiliency built in. However, they aren't immune to physical problems that affect the cables delivering connectivity or outages that affect the complete ExpressRoute location. In high-availability scenarios, where there's risk associated with an outage of an ExpressRoute circuit, you can also provision a VPN gateway that uses the internet as an alternative method of connectivity.
    - **Zone-redundant gateways:**  
        In regions that support availability zones, VPN gateways and ExpressRoute gateways can be deployed in a zone-redundant configuration. This configuration brings resiliency, scalability, and higher availability to virtual network gateways. Deploying gateways in Azure availability zones physically and logically separates gateways within a region while protecting your on-premises network connectivity to Azure from zone-level failures. These gateways require different gateway stock keeping units (SKUs) and use Standard public IP addresses instead of Basic public IP addresses.

## 11. Azure ExpressRoute <a name="question11"></a>

Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a private connection, with the help of a connectivity provider. This connection is called an ExpressRoute Circuit. With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure and Microsoft 365. This feature allows you to connect offices, datacenters, or other facilities to the Microsoft cloud. Each location would have its own ExpressRoute circuit.

Connectivity can be from an any-to-any (IP VPN) network, a point-to-point Ethernet network, or a virtual cross-connection through a connectivity provider at a colocation facility. ExpressRoute connections don't go over the public Internet. This setup allows ExpressRoute connections to offer more reliability, faster speeds, consistent latencies, and higher security than typical connections over the Internet.

**Benefits:**  
- Connectivity to Microsoft cloud services across all regions in the geopolitical region.
- Global connectivity to Microsoft services across all regions with the ExpressRoute Global Reach.
- Dynamic routing between your network and Microsoft via Border Gateway Protocol (BGP).
- Built-in redundancy in every peering location for higher reliability.

**Global connectivity**  
You can enable ExpressRoute Global Reach to exchange data across your on-premises sites by connecting your ExpressRoute circuits. For example, say you had an office in Asia and a datacenter in Europe, both with ExpressRoute circuits connecting them to the Microsoft network. You could use ExpressRoute Global Reach to connect those two facilities, allowing them to communicate without transferring data over the public internet.  
  
**Dynamic routing**  
ExpressRoute uses the BGP. BGP is used to exchange routes between on-premises networks and resources running in Azure. This protocol enables dynamic routing between your on-premises network and services running in the Microsoft cloud.  

**ExpressRoute connectivity models:**  
- **CloudExchange colocation:** refers to your datacenter, office, or other facility being physically colocated at a cloud exchange, such as an ISP. If your facility is colocated at a cloud exchange, you can request a virtual cross-connect to the Microsoft cloud
- **Point-to-point Ethernet connection:** refers to using a point-to-point connection to connect your facility to the Microsoft cloud.
- **Any-to-any connection:** integrate your wide area network (WAN) with Azure by providing connections to your offices and datacenters. Azure integrates with your WAN connection to provide a connection like you would have between your datacenter and any branch offices.
- **Directly from ExpressRoute sites:** You can connect directly into the Microsoft's global network at a peering location strategically distributed across the world. ExpressRoute Direct provides dual 100 Gbps or 10-Gbps connectivity, which supports Active/Active connectivity at scale.

**Security considerations:**  
With ExpressRoute, your data doesn't travel over the public internet, reducing the risks associated with internet communications. ExpressRoute is a private connection from your on-premises infrastructure to your Azure infrastructure. Even if you have an ExpressRoute connection, DNS queries, certificate revocation list checking, and Azure Content Delivery Network requests are still sent over the public internet.

## 12. Azure DNS <a name="question12"></a>

Azure DNS is a hosting service for DNS domains that provides name resolution by using Microsoft Azure infrastructure. By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.  

**Benefits:**
- **Reliability and performance:**  
    DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers, providing resiliency and high availability. Azure DNS uses anycast networking, so the closest available DNS server answers each DNS query, providing fast performance and high availability for your domain.
- **Security:**  
    - Azure role-based access control (Azure RBAC) to control who has access to specific actions for your organization.
    - Activity logs to monitor how a user in your organization modified a resource or to find an error when troubleshooting.
    - Resource locking to lock a subscription, resource group, or resource. Locking prevents other users in your organization from accidentally deleting or modifying critical resources.
- **Ease of Use:**  
    Azure DNS is integrated in the Azure portal and uses the same credentials, support contract, and billing as your other Azure services.
- **Customizable virtual networks:**  
    Azure DNS also supports private DNS domains. This feature allows you to use your own custom domain names in your private virtual networks, rather than being stuck with the Azure-provided names.
- **Alias records:**  
    You can use an alias record set to refer to an Azure resource, such as an Azure public IP address, an Azure Traffic Manager profile, or an Azure Content Delivery Network (CDN) endpoint. If the IP address of the underlying resource changes, the alias record set seamlessly updates itself during DNS resolution. The alias record set points to the service instance, and the service instance is associated with an IP address.

**You can't use Azure DNS to buy a domain name.** For an annual fee, you can buy a domain name by using App Service domains or a third-party domain name registrar. Once purchased, your domains can be hosted in Azure DNS for record management.

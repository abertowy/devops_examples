# AZ-104: Configure and manage virtual networks for Azure administrators

## Table of contents
1. [Azure virtual networks](#question1)
2. [Subnets](#question2)
3. [Create virtual networks](#question3)
4. [Some](#question4)
5. [Some](#question5)
6. [Some](#question6)
7. [Some](#question7)
8. [Some](#question8)
9. [Some](#question9)
10. [Some](#question10)

## 1. Azure virtual networks <a name="question1"></a>

An **Azure Virtual Network (VNet)** is the fundamental building block for your private network in the cloud, providing a secure and isolated environment for your Azure resources like Virtual Machines to communicate with each other, the internet, and your on-premises networks. **VNets** allow you to define your own private IP address space, segment it into subnets, and control traffic with security groups.  
You can implement Azure Virtual Network to create a virtual representation of your network in the cloud.  

- An **Azure virtual network** is a logical isolation of the Azure cloud resources.
- You can use virtual networks to provision and manage virtual private networks (VPNs) in Azure.
- Each virtual network has its own **Classless Inter-Domain Routing** (`CIDR`) block and can be linked to other virtual networks and on-premises networks.
- You can link virtual networks with an on-premises IT infrastructure to create hybrid or cross-premises solutions, when the `CIDR` blocks of the connecting networks don't overlap.
- You control the DNS server settings for virtual networks, and segmentation of the virtual network into subnets.

### Scenarios

1. **Create a dedicated private cloud-only virtual network**:  
    Sometimes you don't require a cross-premises configuration for your solution. When you create a virtual network, your services and virtual machines within your virtual network can communicate directly and securely with each other in the cloud. You can still configure endpoint connections for the virtual machines and services that require internet communication, as part of your solution.  
2. **Securely extend your data center with virtual networks**:  
    You can build traditional site-to-site VPNs to securely scale your datacenter capacity. Site-to-site VPNs use IPSEC to provide a secure connection between your corporate VPN gateway and Azure.  
3. **Enable hybrid cloud scenarios**:  
    Virtual networks give you the flexibility to support a range of hybrid cloud scenarios. You can securely connect cloud-based applications to any type of on-premises system, such as mainframes and Unix systems.  

## 2. Subnets <a name="question2"></a>

There are certain conditions for the IP addresses in a virtual network when you apply segmentation with subnets.

- Each subnet contains a **range of IP addresses** that fall **within** the virtual network **address space**.
- The **address range** for a subnet must be **unique** within the address space for the virtual network.
- The **range** for one subnet **can't overlap** with other subnet IP address ranges in the same virtual network.
- The **IP address space** for a subnet must be specified by using **CIDR notation**.
- You can segment a virtual network into one or more subnets in the Azure portal.

### Reserved addresses

1. `192.168.1.0`: This value identifies the virtual network address
2. `192.168.1.1``: Azure configures this address as the default gateway
3. `192.168.1.2` and `192.168.1.3`: Azure maps these Azure DNS IP addresses to the virtual network space.
4. `192.168.1.255`: This value supplies the virtual network broadcast address.

### Considerations

1. **Consider service requirements**  
    Each service directly deployed into a virtual network has specific requirements for routing and the types of traffic that must be allowed into and out of associated subnets. A service might require or create their own subnet. There must be enough unallocated space to meet the service requirements. Suppose you connect a virtual network to an on-premises network by using Azure VPN Gateway. The virtual network must have a dedicated subnet for the gateway.  
2. **Consider network virtual appliances**  
    Azure routes network traffic between all subnets in a virtual network, by default. You can override Azure's default routing to prevent Azure routing between subnets. You can also override the default to route traffic between subnets through a network virtual appliance. If you require traffic between resources in the same virtual network to flow through a network virtual appliance, deploy the resources to different subnets.  
3. **Consider network security groups**  
    You can associate zero or one network security group to each subnet in a virtual network. You can associate the same or a different network security group to each subnet. Each network security group contains rules that allow or deny traffic to and from sources and destinations.  
4. **Consider private links**  
    Azure Private Link provides private connectivity from a virtual network to Azure platform as a service (PaaS), customer-owned, or Microsoft partner services. Private Link simplifies the network architecture and secures the connection between endpoints in Azure. The service eliminates data exposure to the public internet.  

## 3. Create virtual networks <a name="question3"></a>

### Requirements

1. When you create a virtual network, you need to **define the IP address space** for the network.
2. Plan to use an IP address space that's not already in use in your organization.
    - The address space for the network can be either on-premises or in the cloud, but not both.
    - Once you create the IP address space, it can't be changed. If you plan your address space for cloud-only virtual networks, you might later decide to connect an on-premises site.
3. To create a virtual network, you need to define at least one subnet.
    - Each subnet contains a range of IP addresses that fall within the virtual network address space.
    - The address range for each subnet must be unique within the address space for the virtual network.
    - The range for one subnet can't overlap with other subnet IP address ranges in the same virtual network.
3. You can create a virtual network in the Azure portal. Provide the Azure subscription, resource group, virtual network name, and service region for the network.

## 4.  <a name="question4"></a>

## 5.  <a name="question5"></a>

## 6.  <a name="question6"></a>

## 7.  <a name="question7"></a>

## 8.  <a name="question8"></a>

## 9.  <a name="question9"></a>

## 10.  <a name="question10"></a>
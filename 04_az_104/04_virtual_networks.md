# AZ-104: Configure and manage virtual networks for Azure administrators

## Table of contents
1. [Azure virtual networks](#question1)
2. [Subnets](#question2)
3. [Create virtual networks](#question3)
4. [Plan IP addressing](#question4)
5. [Public IP address](#question5)
6. [Private IP address](#question6)
7. [Network security groups](#question7)
8. [Network security group rules](#question8)
9. [Azure DNS](#question9)
10. [Configure Azure DNS to host your domain](#question10)
11. [Azure Virtual Network peering](#question11)
12. [Gateway transit and connectivity](#question12)
13. [Extend peering with user-defined routes and service chaining](#question13)

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
4. You can create a virtual network in the Azure portal. Provide the Azure subscription, resource group, virtual network name, and service region for the network.

## 4. Plan IP addressing <a name="question4"></a>

**Private IP addresses** enable communication within an **Azure virtual network** and your **on-premises network**. You create a private IP address for your resource when you use a **VPN gateway** or **Azure ExpressRoute** circuit to extend your network to Azure.  
  
**Public IP addresses** allow your resource to communicate with the **internet**. You can create a public IP address to connect with Azure public-facing services.  
  
### Characteristics

1. IP addresses can be **statically** assigned or **dynamically** assigned.
2. You can **separate** dynamically and statically assigned IP resources into **different subnets**.
3. **Static IP addresses** don't change and are **best** for certain situations, such as:
    - DNS name resolution, where a change in the IP address requires updating host records.
    - IP address-based security models that require apps or services to have a static IP address.
    - TLS/SSL certificates linked to an IP address.
    - Firewall rules that allow or deny traffic by using IP address ranges.
    - Role-based virtual machines such as Domain Controllers and DNS servers.

## 5. Public IP address <a name="question5"></a>

### Considerations: public IP address

- **IP Version**: Select to create an IPv4 or IPv6 address, or Both addresses.
- **SKU**: Select the SKU for the public IP address, including **Basic** or **Standard**. The value must match the SKU of the Azure load balancer with which the address is used.
- **Name**: Enter a name to identify the IP address. The name must be **unique** within the resource group you select.
- **IP address assignment**: Identify the type of IP address assignment to use.  
    - **Dynamic addresses** are assigned after a public IP address is associated to an Azure resource and is started for the first time. Dynamic addresses can change if a resource such as a virtual machine is stopped (deallocated) and then restarted through Azure. The address remains the same if a virtual machine is rebooted or stopped from within the guest OS. When a public IP address resource is removed from a resource, the dynamic address is released.
    - **Static addresses** are assigned when a public IP address is created. Static addresses aren't released until a public IP address resource is deleted. If the address isn't associated to a resource, you can change the assignment method after the address is created. If the address is associated to a resource, you might not be able to change the assignment method.

> If you select IPv6 for the IP version, the assignment method must be Dynamic for the Basic SKU. Standard SKU addresses are Static for both IPv4 and IPv6 addresses.

A public IP address resource can be associated with virtual machine network interfaces, internet-facing load balancers, VPN gateways, and application gateways. You can associate your resource with both dynamic and static public IP addresses.  

### Public IP associating

| Resource | Public IP address association | Dynamic IP address | Static IP address |
|----------|-------------------------------|--------------------|-------------------|
| Virtual machine | NIC | Yes | Yes |
| Load balancer | Front-end configuration | Yes | Yes |
| VPN gateway | VPN gateway IP configuration | Yes | Yes * |
| Application gateway | Front-end configuration | Yes | Yes * |

> Static IP addresses are available on certain SKUs only.

### Public IP address SKUs

| Feature | Basic SKU | Standard SKU |
|---------|-----------|--------------|
| IP assignment | Static or Dynamic | Static |
| Security | Open by default | Secure by default, closed to inbound traffic |
| Resources | Network interfaces, VPN gateways, Application gateways, and internet-facing load balancers | Network interfaces or public standard load balancers |
| Redundancy | Not zone redundant | Zone redundant by default |

## 6. Private IP address <a name="question6"></a>

A **private IP address** resource can be associated with virtual machine network interfaces, internal load balancers, and application gateways. Azure can provide an IP address (dynamic assignment) or you can assign the IP address (static assignment).  

### Private IP address association

| Resource | Private IP address | Dynamic IP address | Static IP address |
|----------|--------------------|--------------------|-------------------|
| Virtual machine | NIC | Yes | Yes |
| Internal load balancer | Front-end configuration | Yes | Yes |
| Application gateway | Front-end configuration | Yes | Yes |

A private IP address is allocated from the address range of the virtual network subnet that a resource is deployed in. There are two options: dynamic and static.  

- **Dynamic:**  
    Azure assigns the next available unassigned or unreserved IP address in the subnet's address range. Dynamic assignment is the **default allocation method**.  
    > Suppose addresses `10.0.0.4` through `10.0.0.9` are already assigned to other resources. In this case, Azure assigns the address `10.0.0.10` to a new resource.  
- **Static:**  
    You select and assign any unassigned or unreserved IP address in the subnet's address range.  
    > Suppose a subnet's address range is `10.0.0.0/16`, and addresses `10.0.0.4` through `10.0.0.9` are already assigned to other resources. In this scenario, you can assign any address between `10.0.0.10` and `10.0.255.254`.  

## 7. Network security groups <a name="question7"></a>

**Network security groups** are a way to **limit network traffic** to resources in your virtual network.  

### NSG Characteristics

- **Network security group** contains a **list of security rules** that allow or deny inbound or outbound network traffic.
- **Network security group** can be associated to a **subnet** or a **network interface**.
- **Network security group** can be associated **multiple** times.
- The **Overview page** for a virtual machine provides information about the associated network security groups. You can see details such as the assigned subnets, assigned network interfaces, and the defined security rules.

> Each subnet can have a maximum of one associated network security group.

> Each network interface that exists in a subnet can have zero, or one, associated network security groups.

## 8. Network security group rules <a name="question8"></a>

- Azure creates several **default** security rules within each network security group, including inbound traffic and outbound traffic. Examples of default rules include `DenyAllInbound` traffic and `AllowInternetOutbound` traffic.
- Azure creates the **default** security rules in **each network security group** that you create.
- You can add more security rules to a network security group by specifying conditions. Here's a list of the most common conditions:  
    - **Source**: Identifies how the security rule controls inbound traffic. Values: `Any`, `IP Addresses`, `IP address range`, `My IP address`, `Service Tag`, or `Application security group`.
    - **Source port ranges** and **Destination port ranges**: Specify the ports on which the rule allows or denies traffic
    - **Destination**: Identifies how the security rule controls outbound traffic. Values: `Any`, `IP Addresses`, `IP address range`, `My IP address`, `Service Tag`, or `Application security group`.
    - **Protocol**: Restrict the rule to the Transmission Control Protocol (`TCP`), User Datagram Protocol (`UDP`), or Internet Control Message Protocol (`ICMP`). The **default** is for the rule to **apply to all** protocols (`Any`)
    - **Service**: Specifies the destination **protocol** and port range for the security rule. You can choose a predefined service like RDP or SSH or provide a custom port range.
    - **Action**: Allow or Deny
    - **Priority**: A value between 100 and 4,096 that's unique for all security rules within the NSG. **The lower the priority value, the higher priority for the rule**.
- Each security rule is assigned a **Priority value**. All security rules for a network security group are processed in priority order. When a rule has a low Priority value, the rule has a higher priority or precedence in terms of order processing.
- You **can't remove** the default security rules.
- You can **override** a default security rule by creating another security rule that has a **higher Priority** setting for your network security group.

Azure defines three **default inbound security rules** for your network security group. These rules deny all inbound traffic (`DenyAllInBound`) except traffic from your virtual network(`AllowVnetInBound`) and Azure load balancers (`AllowAzureLoadBalancerInBound`).  
Azure defines three **default outbound security rules** for your network security group (`AllowVnetOutBound`, `AllowInternetOutBound`, `DenyAllOutBound`). These rules only allow outbound traffic to the internet and your virtual network.

- For **inbound traffic**, Azure **first** processes network security group security rules for any associated **subnets** and then any associated network interfaces.
- For **outbound traffic**, the process is reversed. Azure **first** evaluates network security group security rules for any associated **network interfaces** followed by any associated subnets.
- For both the **inbound and outbound** evaluation process, Azure also checks how to apply the rules for **intra-subnet traffic**. Intra-subnet traffic refers to virtual machines in the same subnet.
- When you apply **network security groups** to **both** a subnet and a network interface, each **network security group** is **evaluated independently**. Both inbound and outbound rules are considered based on the **priority and processing order**.

### NSG considerations

- **Consider allowing all traffic**. If you place your virtual machine within a subnet or utilize a network interface, you don't have to associate the subnet or NIC with a network security group. This approach allows all network traffic through the subnet or NIC according to the default Azure security rules. If you're **not concerned about controlling traffic** to your resource at a specific level, then **don't associate your resource** at that level **to a network security group**.
- **Consider importance of allow rules**. When you **create a network security group**, you **must define an allow rule** for both the **subnet and network interface** in the group to ensure traffic can get through. If you have a subnet or NIC in your network security group, you must define an allow rule at each level. Otherwise, the traffic is denied for any level that doesn't provide an allow rule definition.
- **Consider intra-subnet traffic**. The security rules for a network security group associated to a subnet can affect traffic between all virtual machines in the subnet. You can prohibit intra-subnet traffic by defining a rule in the network security group to deny all inbound and outbound traffic. This rule prevents all virtual machines in your subnet from communicating with each other.
- **Consider rule priority**. The security rules for a network security group are processed in priority order. To ensure a particular security rule is **always processed**, **assign the lowest possible priority value** to the rule. It's a good practice to **leave gaps in your priority numbering**, such as 100, 200, 300, and so. The gaps in the numbering allow you to add new rules without having to edit existing rules.

> Use the Effective security rules link in the Azure portal to verify which security rules are applied to your machines, subnets, and network interfaces.

### Application Security Group Considerations

- **Consider IP address maintenance**. When you control network traffic by using **application security groups**, you **don't need** to **configure** inbound and outbound traffic for **specific IP addresses**. If you have many virtual machines in your configuration, it can be difficult to specify all of the affected IP addresses. As you maintain your configuration, the number of your servers can change. These changes can require you to modify how you support different IP addresses in your security rules.
- **Consider no subnets**. By organizing your virtual machines into **application security groups**, you **don't need** to also **distribute** your **servers across specific subnets**. You can arrange your **servers by application** and purpose to achieve logical groupings.
- **Consider simplified rules**. Application security groups help to eliminate the need for multiple rule sets. You don't need to create a separate rule for each virtual machine. You can dynamically apply new rules to designated application security groups. New security rules are **automatically applied** to all the virtual machines in the specified application security group.
- **Consider workload support**. A configuration that implements application security groups is **easy to maintain** and understand because the organization is based on workload usage. Application security groups provide logical arrangements for your applications, services, data storage, and workloads.
- **Consider service tags**. **Service Tags** represent a group of **IP address prefixes** from a specific Azure service. They help minimize the complexity of frequent updates on network security rules. While service tags are used to simplify the management of IP addresses for Azure services, ASGs are used to group VMs and manage network security policies based on those groups.

## 9. Azure DNS <a name="question9"></a>

**Azure DNS** is a hosting service for **Domain Name System** (`DNS`) domains that provides **name resolution** by using Microsoft Azure infrastructure.  
`DNS`, or the **Domain Name System**, is a **protocol** within the TCP/IP standard. **DNS** serves an essential role of **translating** the human-readable domain names (`www.wideworldimports.com`) into a **known IP address**.  

**DNS primary functions:**  
- Maintains a **local cache** of recently accessed or used domain names and their IP addresses. This cache provides a **faster response** to a local domain lookup request. If the DNS server can't find the requested domain, it passes the request to another DNS server. This process repeats at each DNS server until either a match is made or the search times out.
- Maintains the **key-value pair database of IP addresses** and any host or subdomain over which the DNS server has authority. This function is often **associated with mail, web, and other internet domain services**.

**Domain lookup requests**  
- If the domain name is **stored** in the short-term **cache**, the **DNS server resolves** the domain request.
- If the domain isn't in the cache, it **contacts one or more DNS servers** on the web to see if they have a **match**. When a match is found, the DNS server **updates the local cache** and resolves the request.
- If the domain isn't found after a **reasonable number of DNS checks**, the DNS server responds with a **domain cannot be found** error.

Every computer, server, or network-enabled device on your network has an **IP address**. An IP address is **unique** within your **domain**. There are two standards of IP address: IPv4 and IPv6.
- **IPv4** is composed of **four sets of numbers, in the range 0 to 255**, each separated by a dot; for example: `127.0.0.1`. Today, **IPv4** is the most commonly used standard. Yet, with the increase in IoT devices, the IP**v4 standard will eventually be **unable to keep up**.
- **IPv6** is a relatively new standard and is intended to eventually **replace IPv4**. It consists of **eight groups of hexadecimal numbers**, each separated by a colon; for example: `fe80:11a1:ac15:e9gf:e884:edb0:ddee:fea3`.

**Configuration** information for your DNS server is stored as a **file** within a **zone** on your **DNS server**. Each file is called a **record**. The following record types are the most commonly created and used:  
- `A` is the **host record**, and is the most common type of DNS record. It **maps the domain or host name to the IP address**.
- `CNAME` is a **Canonical Name record** that's used to create an **alias** from one domain name to another domain name. If you had different domain names that all accessed the same website, you'd use `CNAME`.
- `MX` is the **mail exchange record**. It **maps mail requests** to your mail server, whether hosted on-premises or in the cloud.
- `TXT` is the **text record**. It's used to **associate text strings with a domain name**. **Azure** and Microsoft 365 use TXT records to **verify domain ownership**.
- `AAAA' (Quad-A record, host IPV6)
- `Wildcards`
- `CAA` (certificate authority)
- `NS` (name server)
- `SOA` (start of authority)
- `SPF` (sender policy framework)
- `SRV` (server locations)

The `SOA` and `NS` records are created **automatically** when you create a DNS zone by using Azure DNS.  
  
Some record types support the concept of **record sets**, or resource record sets. A record set allows for multiple resources to be defined in a single record. `SOA` and C`NAME records **can't contain record sets**.  
  
**Azure DNS** allows you to host and manage your domains by using a globally distributed name-server infrastructure. It allows you to manage all of your domains by using your **existing Azure credentials**.  
**Azure DNS** acts as the `SOA` for the domain.  
You **can't** use **Azure DNS** to **register a domain name**; you need to register it by using a third-party domain registrar.  
At this time, **Azure DNS doesn't support Domain Name System Security Extensions**.  

**Azure DNS security features**:  
- **Role-based access control**, which gives you fine-grained control over users' access to Azure resources. You can monitor their usage and control the resources and services to which they have access.
- **Activity logs**, which let you track changes to a resource and pinpoint where faults occurred.
- **Resource locking**, which gives you a greater level of control to restrict or remove access to resource groups, subscriptions, or any Azure resources.

### Private domains

**Azure DNS** lets you create **private zones**. These zones provide name resolution for virtual machines (VMs) within a virtual network and between virtual networks without having to create a custom DNS solution. **Private zones** allow you to use your **own custom domain names** rather than the Azure-provided names.  
To publish a **private DNS zone** to your virtual network, you specify the **list of virtual networks that are allowed** to resolve records within the zone.  
  
**Benefits:**  
- **DNS zones** are supported as **part of the Azure infrastructure**, so there's no need to invest in a DNS solution.
- **All** DNS record **types** are supported: `A`, `CNAME`, `TXT`, `MX`, `SOA`, `AAAA`, `PTR`, and `SRV`.
- **Host names** for VMs in your virtual network are **automatically** maintained.
- Split-horizon DNS support allows the same **domain name** to exist in both **private and public** zones. It resolves to the correct one based on the originating request location.

Alias records sets ('A', `AAAA`, `CNAME`) can point to an Azure resource. For example, you can set up an alias record to direct traffic to an Azure public IP address, an Azure Traffic Manager profile, or an Azure Content Delivery Network endpoint.  

## 10. Configure Azure DNS to host your domain <a name="question10"></a>

> You used a third-party domain-name registrar to register the wideworldimports.com domain. The domain doesn't point to your organization's website yet.

### Public DNS

1. Create a DNS zone in Azure
2. Get your Azure DNS name servers from the name servers (`NS`) record (to update your domain registrar's information and point to the Azure DNS zone)
3. Update the domain registrar setting  
    As the domain owner, you need to sign in to the domain-management application provided by your domain registrar. In the management application, edit the NS record and change the NS details to match your Azure DNS name server details  
    > Changing the `NS details` is called **domain delegation**. When you delegate the domain, you must use **all four name servers** provided by Azure DNS.  
4. Verify delegation of domain name services (10 minutes, but might take longer)  
    Query the start of authority (SOA) record. The SOA record is automatically created when the Azure DNS zone is set up. You can verify the SOA record using a tool like nslookup.  
    `nslookup -type=SOA wideworldimports.com`  
5. Configure your custom DNS settings  
    Web servers or load balancers need to have their own custom settings in the DNS zone, either as an `A` record or a `CNAME`.  
    - `A` record:  
        - **Name**: The name of the custom domain, for example webserver1.
        - **Type**: In this instance, it's `A`.
        - **TTL**: Represents the "time-to-live" as a whole unit, where 1 is one second. This value indicates how long the `A` record lives in a DNS cache before it expires.
        - **IP address**: The IP address of the server to which this A record should resolve.
    - `CNAME` record:
        - **NAME**: www
        - **TTL**: 600 seconds
        - **Record type**: `CNAME`  

        You might need a `CNAME` in the `wideworldimports` zone if you want both `www.wideworldimports.com` and `wideworldimports.com` to resolve to the **same IP address**.  
        If you exposed a **web function**, you'd create a `CNAME` record that resolves to the **Azure function**.  

### Private DNS

1. Create a private DNS zone
2. Identify virtual networks
3. Link your virtual network to a private DNS zone  
    To link the private DNS zone to a virtual network, you **create a virtual network link**. In the Azure portal, go to the `private zone`, and select `Virtual network links`.  

### Aliases

**Apex domain** is your domain's highest level. In our case, that's `wideworldimports.com`. The apex domain is also sometimes referred to as the **zone apex** or **root apex**. The `@` symbol often represents the **apex domain** in your DNS zone records.  
The `NS` and `SOA` records are automatically created for apex domain when you created the DNS zone.  
`CNAME` records that you might need for an Azure Traffic Manager profile or Azure Content Delivery Network endpoints **aren't supported** at the **zone apex level**. However, other alias records are supported at the zone apex level.  
**Azure alias records** enable a zone apex domain to **reference other Azure resources** from the DNS zone. You can also use an Azure alias to route all traffic through Traffic Manager.  

**Azure alias record** can point to the following Azure resources:  

- A Traffic Manager profile
- Azure Content Delivery Network endpoints
- A public IP resource
- A front-door profile

### Advantages of using alias records:

- **Prevents dangling DNS records**: A dangling DNS record occurs when the DNS zone records aren't up to date with changes to IP addresses. Alias records prevent dangling references by tightly coupling the lifecycle of a DNS record with an Azure resource.
- **Updates DNS record set automatically when IP addresses change**: When the underlying IP address of a resource, service, or application is changed, the alias record ensures that any associated DNS records are automatically refreshed.
- **Hosts load-balanced applications at the zone apex**: Alias records allow for zone apex resource routing to Traffic Manager.
- **Points zone apex to Azure Content Delivery Network endpoints**: With alias records, you can now directly reference your Azure Content Delivery Network instance.

## 11. Azure Virtual Network peering <a name="question11"></a>

**Virtual Network peering** enables you to seamlessly **connect two Azure virtual networks**. After the networks are peered, the two virtual networks operate **as a single network**, for connectivity purposes.  
After you create a peering between virtual networks, the **individual virtual networks** are still managed as **separate** resources.  
**Virtual networks** can be peered across **subscriptions** and **tenants**.  

### Regional

**Regional** virtual network peering connects Azure virtual networks that **exist in the same region**.  
You can create a regional peering of virtual networks in the same **Azure public cloud region**, or in the same **China cloud region**, or in the same **Microsoft Azure Government cloud region**.  

### Global

**Global** virtual network peering connects Azure virtual networks that **exist in different regions**.  
You can create a global peering of virtual networks in **any Azure public cloud region**, or in **any China cloud region**.  
**Global** peering of virtual networks in different Azure Government cloud regions isn't permitted.

### Benefits

- **Private network connections**:  
    Network **traffic** between **peered virtual** networks is **private**.  
    Traffic between the virtual networks is kept on the **Microsoft Azure backbone network**.  
    **No public internet, gateways, or encryption** is required in the communication between the virtual networks.  
- **Strong performance**:  
    Because Azure Virtual Network peering utilizes the **Azure infrastructure**, you gain a **low-latency**, **high-bandwidth connection** between resources in different virtual networks.  
- **Simplified communication**:
    **Azure Virtual Network peering** lets resources in one virtual network **communicate with resources in a different virtual network**, after the virtual networks are peered.  
- **Seamless data transfer**:  
    You can create an **Azure Virtual Network peering** configuration to transfer data **across Azure subscriptions**, **deployment models**, and across **Azure regions**.
- **No resource disruptions**:  
    **Azure Virtual Network peering** **doesn't require downtime** for resources in either virtual network when creating the peering, or after the peering is created.

> To implement virtual network peering, your Azure account must be assigned to the Network Contributor role. Alternatively, your Azure account can be assigned to a custom role that can complete the necessary peering actions. For details, see Permissions.
  
> The second virtual network in the peering is referred to as the remote network

### Peering status

- For deployment with the **Azure Resource Manager**, the two primary status conditions are `Initiated` and `Connected`. For the classic deployment model, the `Updating` status condition is also used.
- When you create the **initial peering to the second (remote) virtual network** from the first virtual network, the peering status for the **first virtual network** is `Initiated`.
- When you create the **subsequent peering from the second virtual network** to the first virtual network, the **peering status for both** the first and remote virtual networks is `Connected`. In the Azure portal, you can see the status for the first virtual network change from `Initiated` to `Connected`.

## 12. Gateway transit and connectivity <a name="question12"></a>

When **virtual networks are peered**, you can configure **Azure VPN Gateway** in the peered virtual network as a **transit point**. In this scenario, a **peered virtual network uses the remote VPN gateway to gain access to other resources**.  
  
### Example

Three virtual networks in the same region are connected by virtual network peering. Virtual network A and virtual network B are each peered with a hub virtual network. The hub virtual network contains several resources, including a gateway subnet and an Azure VPN gateway. The VPN gateway is configured to allow VPN gateway transit. Virtual network B accesses resources in the hub, including the gateway subnet, by using a remote VPN gateway.  

![V-net peering: VPN transit](../images/04_az_104_04_virtual_networks_with_vpn.png)

The Azure portal doesn't specifically mention gateway transit and connectivity. Instead, you have choices for allowing and forwarding network traffic.  
- Allow `vnet-hub-australiaeast` to access the peered virtual network
- Allow `vnet-hub-australiaeast` to receive forwarded traffic from the peered virtual network
- Allow gateaway in `vnet-hub-australiaeast` to forward traffic to the peered virtual network
- Enable `vnet-hub-australiaeast` to use the peered virtual networks' remote gateaway

### Azure VPN Gateway Details

- A virtual network can have **only one VPN gateway**
- **Gateway** transit is supported for both **regional and global virtual network peering**
- When you allow **VPN gateway transit**, the virtual network can communicate to **resources outside the peering**. In example, the gateway subnet gateway within the hub virtual network can complete tasks such as:  
    - Use a **site-to-site VPN** to connect to an **on-premises network**
    - Use a **vnet-to-vnet** connection to **another virtual network**
    - Use a **point-to-site VPN** to connect to a **client**
- **Gateway transit** allows peered virtual networks to **share the gateway** and get access to **external resources**. With this implementation, you **don't need to deploy a VPN gateway in the peered virtual network**
- You can apply **network security groups** in a virtual network to **block or allow access** to other virtual networks or subnets. When you configure virtual network peering, you can choose to open or close the network security group rules between the virtual networks  

## 13. Extend peering with user-defined routes and service chaining <a name="question13"></a>

**Virtual network peering is nontransitive**. The **communication** capabilities in a peering are **available to only the virtual networks and resources in the peering**. Other mechanisms have to be used to enable traffic to and from resources and networks outside the private peering network.  
Suppose you have three virtual networks: **A**, **B**, and **C**. You establish **virtual network peering** between networks **A** and **B**, and **also** between networks **B** and **C**. You don't set up peering between networks A and C. The virtual network peering capabilities that you set up between networks B and C **don't automatically enable** peering communication capabilities between networks **A** and **C**.  

### Extending peering

1. **Hub and spoke network**  
    When you deploy a **hub-and-spoke** network, the **hub virtual network** can h**ost infrastructure components** like a network virtual appliance (NVA) or Azure VPN gateway. **All** the spoke **virtual networks can then peer with the hub virtual network**. Traffic can flow through NVAs or VPN gateways in the hub virtual network.  
2. **User-defined route (UDR)**  
    Virtual network peering **enables the next hop in a user-defined route** to be the IP address of a virtual machine in the **peered virtual network**, or a **VPN gateway**.
3. **Service chaining**  
    S**ervice chaining** is used to **direct traffic from one virtual network to a virtual appliance or gateway**. To enable **service chaining**, configure **UDRs** that **point to virtual machines** in peered virtual networks **as the next hop IP address**. UDRs could also point to virtual network gateways to enable service chaining.  

![Hub-n-spoke virtual network](../images/04_az_104_04_extend_peering.png)

# Azure Routing

## Table of contents
1. [Azure routing](#question1)
2. [Create custom routes](#question2)
3. [Network virtual appliance (NVA)](#question3)
4. [Create an NVA and virtual machines](#question4)
5. [Route traffic through the NVA](#question5)
6. [Azure Load Balancer](#question6)
7. [How Azure Load Balancer works](#question7)
8. [Azure Load Balancer: Use Cases](#question8)
9. [Azure Application Gateway](#question9)
10. [Some](#question10)

## 1. Azure routing <a name="question1"></a>

**Network traffic** in Azure is **automatically routed** across Azure subnets, virtual networks, and on-premises networks. **System routes** control this routing. They're assigned by **default** to each subnet in a virtual network. With these **system routes**, any Azure virtual machine that is deployed into a virtual network can **communicate** with any other **in the network**. These virtual machines are also potentially accessible from on-premises through a hybrid network or the internet.  
You **can't create or delete** system routes, but you can **override the system routes** by adding custom routes to control traffic flow to the next hop.  
**Next hop type** shows the network path taken by traffic sent to each address prefix.  

| Address prefix | Next hop type | Comment |
|----------------|---------------|---------|
| Unique to the virtual network | Virtual network | A route is created in the address prefix.<br>The prefix represents each address range created at the virtual-network level.<br>If multiple address ranges are specified, multiple routes are created for each address range |
| `0.0.0.0/0' | Internet | Default system route 0.0.0.0/0 routes any address range to the internet,<br>unless you override Azure's default route with a custom route |
| `10.0.0.0/8` | None | Any traffic routed to this hop type is dropped and doesn't get routed outside the subnet<br>IPv4 private-address |
| `172.16.0.0/12` | None | Any traffic routed to this hop type is dropped and doesn't get routed outside the subnet<br>IPv4 private-address |
| `192.168.0.0/16` | None | Any traffic routed to this hop type is dropped and doesn't get routed outside the subnet<br>IPv4 private-address |
| `100.64.0.0/10` | None | Any traffic routed to this hop type is dropped and doesn't get routed outside the subnet<br>Shared address space |

### Virtual network peering and service chaining

**Virtual network peering** and **service chaining** let **virtual networks** within Azure **connect to one another**. This communication in turn creates more routes within the default route table. **Service chaining** lets you override these routes by creating **user-defined routes** between peered networks.  

### Virtual network gateway

Use a **virtual network gateway** to send **encrypted traffic** between Azure and on-premises **over the internet** and to send encrypted traffic **between Azure networks**. A virtual network gateway **contains routing tables and gateway services**.

### Virtual network service endpoint

**Virtual network endpoints** **extend** your **private address space** in Azure by providing a **direct connection to your Azure resources**. This connection restricts the flow of traffic: your Azure **virtual machines can access** your storage account **directly from the private address space** and **deny access from a public virtual machine**. As you enable service endpoints, **Azure creates routes** in the route table to direct this traffic.

### User-defined routes

You can use a **user-defined route to override the default system routes** so traffic can be routed through firewalls or NVAs.  
  
For example, you might have a network with two subnets and want to add a virtual machine in the perimeter network to be used as a **firewall**. You can create a **user-defined route** so that **traffic passes through the firewall** and **doesn't go directly between the subnets**.  

**Hop types**:

- **Virtual appliance**: a **firewall** device used to **analyze** or **filter traffic** that is entering or leaving your network. You can specify the **private IP address** of a Network Interface Card (NIC) attached to a virtual machine **so that IP forwarding can be enabled**. Or you can provide the private IP address of an **internal load balancer**.
- **Virtual network gateway**: Use to indicate when you want **routes for a specific address to be routed to a virtual network gateway**. The **virtual network gateway** is **specified as a VPN** for the next hop type.
- **Virtual network**: Use to **override the default system route** within a virtual network
- **Internet**: Use to **route traffic to a specified address prefix** that is routed to the **internet**.
- **None**: Use to **drop traffic sent** to a specified address prefix

> With user-defined routes, you can't specify the next hop type VirtualNetworkServiceEndpoint, which indicates virtual network peering.

### Service tags for user-defined routes

You can specify a **service tag** as the **address prefix** for a user-defined route instead of an **explicit IP range**. A **service tag** represents a **group of IP address prefixes from a given Azure service**. Microsoft manages the address prefixes encompassed by the service tag and **automatically updates the service tag as addresses change**, thus minimizing the complexity of frequent updates to user-defined routes and reducing the number of routes you need to create.

### Border gateway protocol

A **network gateway** in your **on-premises** network can **exchange routes** with a virtual network gateway in Azure **by using BGP**. BGP is the **standard routing protocol** that's normally used **to exchange routing information** among two or more networks. BGP is used to transfer data and information between autonomous systems on the internet, such as different host gateways.  

Typically, you use **BGP** to **advertise on-premises routes to Azure** when you're connected to an Azure datacenter through **Azure ExpressRoute**. You can also configure BGP if you **connect to an Azure virtual network by using a VPN site-to-site connection**.  

**BGP offers network stability**, because routers can quickly change connections to send packets if a connection path goes down.  

### Route selection and priority

If **multiple routes are available in a route table**, Azure **uses the route with the longest prefix match**. For example, a message is sent to the IP address `10.0.0.2`, but two routes are available with the `10.0.0.0/16` and `10.0.0.0/24` prefixes. Azure **selects** the route with the `10.0.0.0/24` prefix because it's **more specific**.  
When you use longer prefixes, the routing algorithm can select the intended address more quickly.  
> You can't configure multiple user-defined routes with the same address prefix.

If there are **multiple routes with the same address prefix**, Azure selects the route based on the type in the following order of **priority**:  
1. User-defined routes
2. BGP routes
3. System routes

## 2. Create custom routes <a name="question2"></a>

### Create a route table and custom route

```bash
# create a route table
az network route-table create --name publictable --resource-group "[sandbox resource group name]" --disable-bgp-route-propagation false

# create a custom route
az network route-table route create --route-table-name publictable --resource-group "[sandbox resource group name]" \
--name productionsubnet --address-prefix 10.0.1.0/24 --next-hop-type VirtualAppliance --next-hop-ip-address 10.0.2.4
```

### Create a virtual network and subnets

```bash
# create the vnet virtual network and the publicsubnet subnet
az network vnet create --name vnet --resource-group "[sandbox resource group name]" \
--address-prefixes 10.0.0.0/16 --subnet-name publicsubnet --subnet-prefixes 10.0.0.0/24

# create the privatesubnet subnet
az network vnet subnet create --name privatesubnet --vnet-name vnet --resource-group "[sandbox resource group name]" --address-prefixes 10.0.1.0/24

# create the dmzsubnet subnet
az network vnet subnet create --name dmzsubnet --vnet-name vnet --resource-group "[sandbox resource group name]" --address-prefixes 10.0.2.0/24

# show all of the subnets in the vnet virtual network
az network vnet subnet list --resource-group "[sandbox resource group name]" --vnet-name vnet --output table

# associate the route table with the public subnet
az network vnet subnet update --name publicsubnet --vnet-name vnet --resource-group "[sandbox resource group name]" --route-table publictable
```

## 3. Network virtual appliance (NVA) <a name="question3"></a>

**Network virtual appliance (NVA)** is a **virtual appliance** that consists of various layers like:

- firewall
- WAN optimizer
- application-delivery controllers
- routers
- load balancers
- IDS/IPS
- proxies

You can deploy **NVAs** that you choose from **providers in Azure Marketplace**. Such providers include **Cisco**, **Check Point**, **Barracuda**, **Sophos**, **WatchGuard**, and **SonicWall**. You can use an **NVA** to **filter traffic inbound to a virtual network**, to **block malicious requests**, and to **block requests made from unexpected resources**.  
**Network virtual appliances (NVAs)** are virtual machines that **control the flow of network traffic** by controlling routing. You'll typically use them to **manage traffic flowing** from a perimeter-network environment to other networks or subnets.  

You can **deploy firewall appliances** into a virtual network in different configurations. You can put a firewall appliance in a **perimeter-network subnet** in the virtual network, or if you want more control of security, **implement a microsegmentation approach**.  
With the **microsegmentation approach**, you can create **dedicated subnets for the firewall** and then **deploy web applications** and other services in **other subnets**. All traffic is routed through the firewall and inspected by the NVAs. You'll enable forwarding on the virtual-appliance network interfaces to **pass traffic that is accepted by the appropriate subnet**.  
**Microsegmentation** lets the firewall inspect all packets at **OSI Layer 4** and, for application-aware appliances, **Layer 7**. When you deploy an **NVA** to Azure, it acts as a **router that forwards requests** between subnets on the virtual network.  
Some NVAs require **multiple network interfaces**. One network interface is dedicated to the **management network for the appliance**. Additional network interfaces manage and control the traffic processing. After you’ve deployed the NVA, you can then configure the appliance to route the traffic through the proper interface.  

### User-defined routes use cases

- Access to the internet via on-premises network using forced tunneling
- Using virtual appliances to control traffic flow

You can create **multiple route tables in Azure**. Each route table can be associated with one or more subnets. A **subnet can only be associated with one route table**.  

> If traffic is routed through an NVA, the NVA becomes a critical piece of your infrastructure. Any NVA failures directly affect the ability of your services to communicate. It's important to include a highly available architecture in your NVA deployment.

## 4. Create an NVA and virtual machines <a name="question4"></a>

```bash
# deploy the appliance
az vm create --resource-group "[resource group name]" --name nva --vnet-name vnet --subnet dmzsubnet --image Ubuntu2204 \
    --admin-username azureuser --admin-password <password>

# get the NVA network interface's ID
NICID=$(az vm nic list --resource-group "[resource group name]" --vm-name nva --query "[].{id:id}" --output tsv)
echo $NICID

# get the NVA network interface's name
NICNAME=$(az vm nic show --resource-group "[resource group name]" --vm-name nva --nic $NICID --query "{name:name}" --output tsv)
echo $NICNAME

# enable IP forwarding for the network interface
az network nic update --name $NICNAME --resource-group "[resource group name]" --ip-forwarding true

# save the NVA virtual machine's public IP address to the variable
NVAIP="$(az vm list-ip-addresses --resource-group "[resource group name]" --name nva --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" --output tsv)"
echo $NVAIP

# enable IP forwarding within the NVA
ssh -t -o StrictHostKeyChecking=no azureuser@$NVAIP 'sudo sysctl -w net.ipv4.ip_forward=1; exit;'
# enter password you used when you created the VM
```

## 5. Route traffic through the NVA <a name="question5"></a>

```bash
# create a file named cloud-init.txt
code cloud-init.txt
```

Add the following configuration information to the file. With this configuration, the `inetutils-traceroute` package is installed when you create a new VM

```bash
#cloud-config
package_upgrade: true
packages:
   - inetutils-traceroute
```

```bash
# create the public VM
az vm create --resource-group "[resource group name]" --name public --vnet-name vnet --subnet publicsubnet --image Ubuntu2204 \
    --admin-username azureuser --admin-password <password> --no-wait --custom-data cloud-init.txt

# create the private VM
az vm create --resource-group "[resource group name]" --name private --vnet-name vnet --subnet privatesubnet --image Ubuntu2204 \
    --admin-username azureuser --admin-password <password> --no-wait --custom-data cloud-init.txt

# check that the VMs are running
# watch command periodically runs the az vm list command
watch -d -n 5 "az vm list --resource-group "[resource group name]" --show-details \
    --query '[*].{Name:name, ProvisioningState:provisioningState, PowerState:powerState}' \
    --output table"
# A ProvisioningState value of "Succeeded" and a PowerState value of "VM running" indicate a successful deployment

# save the public IP address of the public VM to a variable
PUBLICIP="$(az vm list-ip-addresses --resource-group "[resource group name]" --name public \
    --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
    --output tsv)"
echo $PUBLICIP

# save the public IP address of the private VM to a variable
PRIVATEIP="$(az vm list-ip-addresses --resource-group "[sandbox resource group name]" --name private \
    --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
    --output tsv)"
echo $PRIVATEIP

# trace the route from public to private
ssh -t -o StrictHostKeyChecking=no azureuser@$PUBLICIP 'traceroute private --type=icmp; exit'
# If you receive the error message bash: traceroute: command not found, wait a minute and retry the command
```

Successfull output:  
```bash
traceroute to private.kzffavtrkpeulburui2lgywxwg.gx.internal.cloudapp.net (10.0.1.4), 64 hops max
1   10.0.2.4  0.710ms  0.410ms  0.536ms
2   10.0.1.4  0.966ms  0.981ms  1.268ms
Connection to 52.165.151.216 closed.
```

> Notice that the first hop is to 10.0.2.4. This address is the private IP address of nva.
> The second hop is to 10.0.1.4, the address of private
> now all traffic from public to private is routed through the NVA

```bash
# trace the route from private to public
# when prompted, enter the password for the azureuser account
ssh -t -o StrictHostKeyChecking=no azureuser@$PRIVATEIP 'traceroute public --type=icmp; exit'

# output
traceroute to public.kzffavtrkpeulburui2lgywxwg.gx.internal.cloudapp.net (10.0.0.4), 64 hops max
1   10.0.0.4  1.095ms  1.610ms  0.812ms
Connection to 52.173.21.188 closed.
# private VM is using default routes, and traffic is routed directly between the subnets
```

## 6. Azure Load Balancer <a name="question6"></a>

**Load balancing** is a process in which you **distribute incoming traffic equitably across multiple computers**. A pool of computers that have lower levels of resources often responds to traffic more effectively than a single server with higher performance.  
**Azure Load Balancer** is an Azure service that allows you to evenly **distribute incoming network traffic** across a group of `Azure VMs`, or across instances in a `Virtual Machine Scale Set`. Load Balancer delivers **high availability and network performance** in the following ways:  
- Load-balancing rules determine how traffic is distributed to instances that comprise the back end.
- Health probes ensure the resources in the back end are healthy and that traffic isn't directed to unhealthy back-end instances.

**Public load balancers** are used to load **balance internet traffic to your virtual machines** (VMs). A **public load balancer** maps the **public IP address** and **port number** of incoming traffic **to the private IP address** and port number of the **back-end pool VMs**. A public load balancer can also provide **outbound connections** for VMs **inside your virtual network**.  

An **internal load balancer** directs traffic to **resources** that are **inside a virtual network** or that use a **VPN to access Azure infrastructure**. **Internal load balancer** front-end IP addresses and virtual networks are **never directly exposed to an internet endpoint**. Internal line-of-business (LOB) applications run in Azure and are accessed from within Azure or from on-premises resources. An **internal load balancer** is used where **private IPs are needed at the front end only**. Internal load balancers are often used to **balance traffic from the front-end web tier infrastructure as a service (IaaS)** VMs across a set of secondary VMs that perform tasks such as performing calculations or data processing.  

### Types of load balancing:

- **Within a virtual network**: Load balancing from VMs in the **virtual network** to a set of VMs that reside **within the same virtual network**.
- **For a cross-premises virtual network**: Load balancing **from on-premises** computers to a set of VMs that reside **within the same virtual network**.
- **For multi-tier applications**: Load balancing for **internet-facing multi-tier applications** where the back-end tiers aren't internet-facing. The back-end tiers require traffic load balancing from the internet-facing tier.
- **For LOB applications**: Load balancing for LOB applications that are hosted in Azure without added load balancer hardware or software. This scenario includes **on-premises servers** that are in the set of computers whose traffic is load balanced.

> Each Load Balancer type can be used for inbound and outbound scenarios and scale up to millions of Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) application flows.

## 7. How Azure Load Balancer works <a name="question7"></a>

**Azure Load Balancer** operates at the **transport layer of the Open Systems Interconnection (OSI) model**. This Layer 4 functionality allows traffic management based on **specific properties of the traffic**. Properties including source and destination address, TCP or UDP protocol type, and port number.  

> see elements here

### Front-end IP

The **front-end IP** address is the address clients use to connect to your web application. A **front-end IP** address can be either a **public** or a **private** IP address. Azure load balancers can have **multiple front-end IPs**.

- **Public IP address**: A **public load balancer**: A public load balancer maps the public IP and port of incoming traffic to the private IP and port of the virtual machine (VM). You can distribute specific types of traffic across multiple VMs or services by applying load-balancing rules. The load balancer maps the response traffic from the private IP and port of the VM to the public IP and port of the load balancer. Then, it transmits the response back to the requesting client.
- **Private IP address**: An **internal load balancer**: An internal load balancer distributes traffic to resources that are inside a virtual network. Azure restricts access to the front-end IP addresses of a virtual network that are load balanced. Front-end IP addresses and virtual networks are never directly exposed to an internet endpoint. Internal line-of-business applications run in Azure and are accessed from within Azure or from on-premises resources through a VPN or ExpressRoute connection.

### Load Balancer rules

A **load balancer rule** defines h**ow traffic is distributed** to the back-end pool. The rule **maps a given front-end IP** and port combination **to a set of back-end IP** addresses and port combination.  
Traffic is managed using a **five-tuple hash** made from the following elements:

- **Source IP**: The IP address of the requesting client.
- **Source port**: The port of the requesting client.
- **Destination IP**: The destination IP address of the request.
- **Destination port**: The destination port of the request.
- **Protocol type**: The specified protocol type, Transmission Control Protocol (TCP), or User Datagram Protocol (UDP).
- **Session affinity**: Ensures that the same pool node always handles traffic for a client.

> Load Balancer allows you to load balance services on multiple ports, multiple IP addresses, or both  
> You can configure different load balancing rules for each front-end IP  
> !!! Multiple front-end configurations are only supported with IaaS VMs  

**Load Balancer** **can't apply** different **rules based on internal traffic content** because it operates at Layer 4 (transport layer) of the OSI model. **If you need to manage traffic based on its Layer 7** (application layer) properties, you need to deploy a solution like **Azure Application Gateway**.  

### Back-end pool

The back-end pool is a group of VMs or instances in a Virtual Machine Scale Set that responds to the incoming request. To scale cost-effectively to meet high volumes of incoming traffic, computing guidelines generally recommend adding more instances to the back-end pool.

Load Balancer implements automatic reconfiguration to redistribute load across the altered number of instances when you scale instances up or down. For example, if you added two more VMs instances to the back-end pool, Load Balancer would reconfigure itself to start balancing traffic to those instances based on the already configured load balancing rules.

### Health probes

A health probe is used to determine the health status of the instances in the back-end pool. This health probe determines if an instance is healthy and can receive traffic. You can define the unhealthy threshold for your health probes. When a probe fails to respond, the load balancer stops sending new connections to the unhealthy instances. A probe failure doesn't affect existing connections. The connection continues until: application ends the flow, idle timeout occurs, VM shuts down.  

Health probe types for endpoints: TCP, HTTP, and HTTPS:

- **TCP custom probe**: This probe relies on **establishing a successful TCP session** to a defined probe port. If the specified listener on the VM exists, the probe succeeds. If the connection is refused, the probe fails. You can specify the Port, Interval, and Unhealthy threshold.
- **HTTP or HTTPS custom probe**: The load balancer regularly probes your endpoint (**every 15 seconds, by default**). The instance is healthy if it responds with an HTTP 200 within the timeout period (**default of 31 seconds**). Any status other than HTTP 200 causes the probe to fail. You can specify the port (Port), the URI for requesting the health status from the back end (URI), amount of time between probe attempts (Interval), and the number of failures that must occur for the instance to be considered unhealthy (Unhealthy threshold).

### Session persistence

By default, **Load Balancer** distributes network traffic **equally** among multiple VM instances. It provides stickiness only within a **transport session**. **Session persistence** specifies how **traffic from a client** should be handled. The default behavior (`None`) is that a**ny healthy VM can handle successive requests from a client**.  
**Session persistence** is also known as **session affinity**, **source IP affinity**, or **client IP affinity**. This distribution mode uses a `two-tuple` (source IP and destination IP) or `three-tuple` (source IP, destination IP, and protocol type) hash to route to back-end instances. When you use session persistence, connections from the same client go to the same back-end instance within the back-end pool.  

- **None** (default): Specifies that any healthy VM can handle the request.
- **Client IP** (2-tuple): Specifies that the same back-end instance can handle successive requests from the same client IP address.
- **Client IP and protocol** (3-tuple): Specifies that the same back-end instance can handle successive requests from the same client IP address and protocol combination.

### High availability ports

A **load balancer rule** configured with `protocol - all` and `port - 0` is known as a **high availability (HA) port rule**. This rule enables a single rule to load balance all TCP and UDP flows that arrive on all ports of an internal standard load balancer.

HA ports load-balancing rules help you with **critical scenarios**, such as high availability and scale for network virtual appliances (NVAs) inside virtual networks. The feature can help when a large number of ports must be load balanced.

### Inbound NAT rules

You can use load balancing rules in combination with **Network Address Translation (NAT) rules**. For example, you could use `NAT` from the load balancer's public address to TCP 3389 on a specific VM. This rule combination **allows remote desktop access from outside of Azure**.

### Outbound rules

An **outbound rule** configures **Source Network Address Translation (SNAT)** for all VMs or instances identified by the back-end pool. This rule enables instances in the back end to communicate (outbound) to the internet or other public endpoints.

## 8. Azure Load Balancer: Use Cases <a name="question8"></a>

### When to use Azure Load Balancer

**Azure Load Balancer is best suited for applications that require ultra-low latency and high performance**.

Load Balancer is suitable for your organization's needs because you're **replacing existing network hardware devices** that load balance traffic across applications. The applications used multiple virtual machine (VM) tiers when the applications were on-premises with an Azure service that has the same functionality.

Because Load Balancer operates at Layer 4 like hardware devices that were used on-premises before the organization migrated to Azure, you can use Load Balancer to **replicate that hardware device functionality**. This functionality includes using health probes to ensure that Load Balancer doesn't forward traffic to failed VM nodes. It also includes using session persistence to ensure that clients only communicate with a single VM during a session.

You can configure public load balancers for **front-end traffic to web tiers of applications**. You can also configure internal load balancers to balance traffic **between the web tier** and the tier that performs data analysis and transformation tasks.

You can configure inbound NAT rules to **allow remote desktop protocol access to a VM instance** to perform administrative tasks.

### When not to use Azure Load Balancer

**Azure Load Balancer isn't appropriate if you have a web application that doesn't require load balancing running on a single IaaS VM instance.**

For example, if your web application only receives a small amount of traffic and the existing infrastructure already competently deals with the existing load, there's no need to deploy a back-end pool of VMs and no need to use Load Balancer.

Azure provides other load-balancing solutions as alternatives to Azure Load Balancer, including **Azure Front Door**, **Azure Traffic Manager**, and **Azure Application Gateway**:

- **Azure Front Door** is an **application-delivery network** that provides a **global load balancing and site acceleration service for web applications**. It offers **Layer 7 capabilities** for your application like **TLS/SSL offload**, **path-based routing**, **fast failover**, a web application firewall, and caching to improve performance and high availability of your applications. Choose this option in scenarios such as **load balancing a web app deployed across multiple Azure regions**.
- **Azure Traffic Manager** is a **DNS-based traffic load balancer** that allows you to d**istribute traffic optimally to services across global Azure regions** while providing high availability and responsiveness. Because Traffic Manager is a DNS-based load-balancing service, it **load balances only at the domain level**. For that reason, it **can't fail over as quickly as Front Door**, because of common challenges around **DNS caching** and systems not honoring DNS TTLs.
- **Azure Application Gateway** provides `Application Delivery Controller (ADC)` as a service, offering various **Layer 7 load-balancing capabilities**. Use it to optimize web farm productivity by **offloading CPU-intensive TLS/SSL termination to the gateway**. Application Gateway works within a **region** rather than globally.

**Azure Load Balancer** is a high-performance, **ultra-low-latency Layer 4 load-balancing service** (inbound and outbound) for all UDP and TCP protocols. Its built to handle millions of requests per second while ensuring your solution is highly available. Azure Load Balancer is **zone-redundant**, ensuring high availability across availability zones.  
If Adatum had applications that required web application firewall functionality, Azure Load Balancer wouldn't be an appropriate solution for the company.  

## 9. Azure Application Gateway <a name="question9"></a>

**Azure Application Gateway** **manages the requests** that client applications send **to web apps** that are hosted on a pool of web servers. The pool of web servers can be Azure virtual machines, Azure Virtual Machine Scale Sets, Azure App Service, and even on-premises servers.  
**Application Gateway** provides features such as **load balancing HTTP traffic** and **web application firewall**. It provides support for **TLS/SSL encryption** of traffic between users and an application gateway and between application servers and an application gateway.  
A**pplication Gateway** uses a `round-robin` process to load balance requests to the servers in each back-end pool. **Session stickiness** ensures client **requests** in the same session are r**outed to the same back-end server**. Session stickiness is especially important with **e-commerce applications** where you don’t want a transaction to be disrupted because the load balancer bounces it around between back-end servers.  

### Azure Application Gateway features

- Support for the HTTP, HTTPS, HTTP/2, and WebSocket protocols.
- A web application firewall to protect against web application vulnerabilities.
- End-to-end request encryption.
- Autoscaling to dynamically adjust capacity as your web traffic load change.
- Connection draining allowing graceful removal of back-end pool members during planned service updates.

### Azure Application Gateway Components

- **Front-end IP address**: Client requests are received through a **front-end IP address**. You can configure Application Gateway to have a **public IP address**, a **private IP address**, or **both**.  
    > Application Gateway can't have more than one public IP address and one private IP address.
- **Listeners**: Application Gateway uses one or more **listeners** to receive incoming requests. A listener **accepts traffic** arriving on a specified **combination of protocol, port, host, and IP address**. Each listener **routes requests to a back-end pool** of servers following routing rules that you specify. A listener can be `Basic` or `Multi-site`. A **Basic listener** only **routes** a request based on the **path in the URL**. A **Multi-site listener** can also **route requests using the hostname element of the URL**. Listeners also **handle TLS/SSL certificates** for securing your application between the user and Application Gateway.
- **Routing rules**: A routing rule **binds a listener to the back-end pools**. A rule specifies **how to interpret the hostname and path elements in the URL** of a request and direct the request to the appropriate back-end pool. A routing rule also has an **associated set of HTTP settings**. These HTTP settings indicate whether (and how) **traffic is encrypted between Application Gateway and the back-end servers**. Other configuration information includes **Protocol**, **Session stickiness**, **Connection draining**, **Request timeout period**, and **Health probes**.

### Load balancing in Application Gateway

**Application Gateway** uses a **round-robin mechanism** to automatically load balance the requests sent to the servers in each back-end pool. Load-balancing works with the **Open Systems Interconnection (OSI) Layer 7** routing implemented by Application Gateway routing, which means that it **load balances requests based on the routing parameters** (host names and paths) used by the Application Gateway rules. In comparison, **other load balancers**, such as Azure Load Balancer, function at the **OSI Layer 4 level** and **distribute traffic based on the IP address** of the target of a request.

You can configure session stickiness if you need to ensure that all requests for a client in the same session are routed to the same server in a back-end pool.

### Web application firewall

The **web application firewall (WAF)** is an **optional component** that **handles incoming requests before they reach a listener**. The **web application firewall checks each request for many common threats based on the Open Web Application Security Project (OWASP)**. Common threats include: **SQL-injection**, **Cross-site scripting**, **Command injection**, **HTTP request smuggling**, **HTTP response splitting**, **Remote file inclusion**, **Bots**, **crawlers**, and scanners, and HTTP protocol violations and anomalies.  
**OWASP** defines a **set of generic rules for detecting attacks**. These rules are referred to as the **Core Rule Set** (CRS). The rule sets are under continuous review as attacks evolve in sophistication. **WAF supports four rule sets: CRS 3.2, 3.1, 3.0 and 2.2.9**. CRS 3.1 is the default. If necessary, you can opt to select only specific rules in a rule set, targeting certain threats. Additionally, you can customize the firewall to specify which elements in a request to examine, and limit the size of messages to prevent massive uploads from overwhelming your servers.  

## 10.  <a name="question10"></a>
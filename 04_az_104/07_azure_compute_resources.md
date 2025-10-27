# Azure Compute Resources

## Table of contents
1. [Azure virtual machines](#question1)
2. [Some](#question2)
3. [Some](#question3)
4. [Some](#question4)
5. [Some](#question5)
6. [Some](#question6)
7. [Some](#question7)
8. [Some](#question8)
9. [Some](#question9)
10. [Some](#question10)

## 1. Azure virtual machines <a name="question1"></a>

An Azure resource is a manageable item in Azure. Just like a physical computer in your datacenter, VMs have several elements that are needed to do their job:

- The VM itself
- Disks for storage
- Virtual network
- Network interface to communicate on the network
- Network Security Group (NSG) to secure the network traffic
- An IP address (public, private, or both)

Azure creates all of these resources if necessary, or you can supply existing ones as part of the deployment process. Each resource needs a name that's used to identify it. If Azure creates the resource, it uses the VM name to generate a resource name - another reason to be consistent with your VM names!

### Network

Virtual networks (VNets) are used in Azure to provide private connectivity between Azure Virtual Machines and other Azure services. VMs and services that are part of the same virtual network can access one another. By default, services outside the virtual network can't connect to services within the virtual network. You can, however, configure the network to allow access to the external service, including your on-premises servers.

When you set up a virtual network, you specify the available address spaces, subnets, and security. If the VNet is connected to other VNets, you must select address ranges that aren't overlapping. This is the range of private addresses that the VMs and services in your network can use. You can use unroutable IP addresses such as 10.0.0.0/8, 172.16.0.0/12, or 192.168.0.0/16, or define your own range. Azure treats any address range as part of the private VNet IP address space if it's only reachable within the VNet, within interconnected VNets, and from your on-premises location.

After deciding the virtual network address space(s), you can create one or more subnets for your virtual network. You create these subnets to break up your network into more manageable sections. For example, you might assign 10.1.0.0 to VMs, 10.2.0.0 to back-end services, and 10.3.0.0 to SQL Server VMs.

By default, there's no security boundary between subnets, so services in each of these subnets can talk to one another. However, you can set up Network Security Groups (NSGs), which allow you to control the traffic flow to and from subnets and to and from VMs. NSGs act as software firewalls, applying custom rules to each inbound or outbound request at the network interface and subnet level. This way, you can fully control every network request coming in or out of the VM.

### VM deployment

1. $\color{Green}\large{\textsf{VM name}}$  
    The VM name is used as the computer name, which is configured as part of the operating system. You can specify a name of up to 64 characters on a Linux VM and 15 characters on a Windows VM. This name also defines a manageable Azure resource, and it's not trivial to change later. That means you should choose names that are meaningful and consistent, so you can easily identify what the VM does.  
2. $\color{Green}\large{\textsf{VM location}}$  
    When you create and deploy a virtual machine, you must select a region where you want to allocate the resources. You can place your VMs as close as possible to your users to improve performance and to meet any legal, compliance, or tax requirements.

    - Location can limit your available options
    - There are price differences between locations

3. $\color{Green}\large{\textsf{VM size}}$  
    Azure provides a wide range of VM size options allowing you to select the appropriate mix of compute, memory, and storage for what you want to do.  

    - $\color{Green}\large{\textsf{General purpose}}$  
        General-purpose VMs are designed to have a balanced CPU-to-memory ratio. Ideal for testing and development, small to medium databases, and low to medium traffic web servers.
    - $\color{Green}\large{\textsf{Compute optimized}}$  
        Compute optimized VMs are designed to have a high CPU-to-memory ratio. Suitable for medium traffic web servers, network appliances, batch processes, and application servers.
    - $\color{Green}\large{\textsf{Memory optimized}}$  
        Memory optimized VMs are designed to have a high memory-to-CPU ratio. Great for relational database servers, medium to large caches, and in-memory analytics.
    - $\color{Green}\large{\textsf{Storage optimized}}$  
        Storage optimized VMs are designed to have high disk throughput and IO. Ideal for VMs running databases.
    - $\color{Green}\large{\textsf{GPU}}$  
        GPU VMs are specialized virtual machines targeted for heavy graphics rendering and video editing. These VMs are ideal options for model training and inferencing with deep learning.
    - $\color{Green}\large{\textsf{High performance compute}}$  
        High performance compute is the fastest and most powerful CPU virtual machines with optional high-throughput network interfaces.

    > Azure allows you to change the VM size when the existing size no longer meets your needs.

    > The VM size can be changed while the VM is running, as long as the new size is available in the current hardware cluster the VM is running on. If you stop and deallocate the VM, you can then select any size available in your region since deallocation removes your VM from the cluster it was running on.

    > Be careful about resizing production VMs - they will be rebooted automatically which can cause a temporary outage and change some configuration settings such as the IP address.

### Parts of a VM and how they're billed

| Resource | Description | Cost |
|----|----|----|----|
| Virtual network | For giving your virtual machine the ability to communicate with other resources | https://azure.microsoft.com/pricing/details/virtual-network/ |
| A virtual Network Interface Card (NIC) | For connecting to the virtual network | There is no separate cost for NICs. However, there is a limit to how many NICs you can use based on your VM's size. Size your VM accordingly and reference Virtual Machine pricing. |
| A private IP address and sometimes a public IP address. | For communication and data exchange on your network and with external networks | https://azure.microsoft.com/pricing/details/ip-addresses/ |
| Network security group (NSG) | For managing the network traffic too and from your VM. For example, you might need to open port 22 for SSH access, but you might want to block traffic to port 80. Blocking and allowing port access is done through the NSG. | There are no additional charges for network security groups in Azure. |
| OS Disk and possibly separate disks for data. | It's a best practice to keep your data on a separate disk from your operating system, in case you ever have a VM fail, you can simply detach the data disk, and attach it to a new VM. | All new virtual machines have an operating system disk and a local disk.
Azure doesn't charge for local disk storage. The operating system disk, which is usually 127GiB but is smaller for some images, is charged at the regular rate for disks. https://azure.microsoft.com/pricing/details/managed-disks/ |
| In some cases, a license for the OS | For providing your virtual machine runs to run the OS | The cost varies based on the number of cores on your VM, so size your VM accordingly. The cost can be reduced through the Azure Hybrid Benefit. |

### Understanding the pricing model

There are two separate costs the subscription is charged for every VM: $\color{Green}\large{\textsf{compute and storage}}$. By separating these costs, you scale them independently and only pay for what you need.

$\color{Green}\large{\textsf{Compute costs}}$ - Compute expenses are priced on a per-hour basis but billed on a per-minute basis. For example, you're only charged for 55 minutes of usage if the VM is deployed for 55 minutes. You're not charged for compute capacity if you stop and deallocate the VM since deallocation releases the hardware. The hourly price varies based on the VM size and OS you select. Linux-based instances are cheaper because there's no operating system license charge. For Windows, the cost for a VM includes the charge for the operating system.

> You might be able to save money by reusing existing licenses with the Azure Hybrid benefit for Linux or Windows.

### Payment options

- Pay as you go  
    With the pay-as-you-go option, you pay for compute capacity by the second, with no long-term commitment or upfront payments. You're able to increase or decrease compute capacity on demand and start or stop at any time. Select this option if you run applications with short-term or unpredictable workloads that can't be interrupted. For example, if you're doing a quick test, or developing an app in a VM, pay-as-you-go is the appropriate option.
- Reserved Virtual Machine Instances  
    The Reserved Virtual Machine Instances (RI) option is an advance purchase of a virtual machine for one or three years in a specified region. The commitment is made up front, and in return, you get up to 72% price savings compared to pay-as-you-go pricing. RIs are flexible and can easily be exchanged or returned for an early termination fee. Select this option if the VM has to run continuously, or you need budget predictability, and you can commit to using the VM for at least a year.


## 2.  <a name="question2"></a>

## 3.  <a name="question3"></a>

## 4.  <a name="question4"></a>

## 5.  <a name="question5"></a>

## 6.  <a name="question6"></a>

## 7.  <a name="question7"></a>

## 8.  <a name="question8"></a>

## 9.  <a name="question9"></a>

## 10.  <a name="question10"></a>
# Basics

## Table of contents
1. [Microsoft Entra ID](#question1)
2. [Microsoft Entra Domain Services](#question2)
3. [Azure authentication methods](#question3)
4. [Azure external identities](#question4)
5. [Azure conditional access](#question5)
6. [Azure role-based access control (RBAC)](#question6)
7. [Zero Trust model](#question7)
8. [Defense-in-depth](#question8)
9. [Microsoft Defender for Cloud](#question9)

## 1. Microsoft Entra ID <a name="question1"></a>

Microsoft Entra ID is a directory service that enables you to sign in and access both Microsoft cloud applications and cloud applications that you develop. Microsoft Entra ID can also help you maintain your on-premises Active Directory deployment.  

With Microsoft Entra ID, you control the identity accounts, but Microsoft ensures that the service is available globally.  

When you secure identities on-premises with Active Directory, Microsoft doesn't monitor sign-in attempts. When you connect Active Directory with Microsoft Entra ID, Microsoft can help protect you by detecting suspicious sign-in attempts at no extra cost. For example, Microsoft Entra ID can detect sign-in attempts from unexpected locations or unknown devices.  

Microsoft Entra ID is for:  
- **IT administrators**. Administrators can use Microsoft Entra ID to control access to applications and resources based on their business requirements.
- **App developers**. Developers can use Microsoft Entra ID to provide a standards-based approach for adding functionality to applications that they build, such as adding SSO functionality to an app or enabling an app to work with a user's existing credentials.
- **Users**. Users can manage their identities and take maintenance actions like self-service password reset.
- **Online service subscribers**. Microsoft 365, Microsoft Office 365, Azure, and Microsoft Dynamics CRM Online subscribers are already using Microsoft Entra ID to authenticate into their account.

Microsoft Entra ID provides services such as:  
1. **Authentication:**  
    This includes verifying identity to access applications and resources. It also includes providing functionality such as self-service password reset, multifactor authentication, a custom list of banned passwords, and smart lockout services.
2. **Single sign-on:**  
    Single sign-on (SSO) enables you to remember only one username and one password to access multiple applications. A single identity is tied to a user, which simplifies the security model. As users change roles or leave an organization, access modifications are tied to that identity, which greatly reduces the effort needed to change or disable accounts.
3. **Application management:**  
    You can manage your cloud and on-premises apps by using Microsoft Entra ID. Features like Application Proxy, SaaS apps, the My Apps portal, and single sign-on provide a better user experience.
4. **Device management:**  
    Along with accounts for individual people, Microsoft Entra ID supports the registration of devices. Registration enables devices to be managed through tools like Microsoft Intune. It also allows for device-based Conditional Access policies to restrict access attempts to only those coming from known devices, regardless of the requesting user account.

If you had an on-premises environment running Active Directory and a cloud deployment using Microsoft Entra ID, you would need to maintain two identity sets. However, you can connect Active Directory with Microsoft Entra ID, enabling a consistent identity experience between cloud and on-premises.  

One method of connecting Microsoft Entra ID with your on-premises AD is using Microsoft Entra Connect. Microsoft Entra Connect synchronizes user identities between on-premises Active Directory and Microsoft Entra ID. Microsoft Entra Connect synchronizes changes between both identity systems, so you can use features like SSO, multifactor authentication, and self-service password reset under both systems.

## 2. Microsoft Entra Domain Services <a name="question2"></a>

Microsoft Entra Domain Services is a service that provides managed domain services such as domain join, group policy, lightweight directory access protocol (LDAP), and Kerberos/NTLM authentication. Just like Microsoft Entra ID lets you use directory services without having to maintain the infrastructure supporting it, with Microsoft Entra Domain Services, you get the benefit of domain services without the need to deploy, manage, and patch domain controllers (DCs) in the cloud.  

A Microsoft Entra Domain Services managed domain lets you run legacy applications in the cloud that can't use modern authentication methods, or where you don't want directory lookups to always go back to an on-premises AD DS environment. You can lift and shift those legacy applications from your on-premises environment into a managed domain, without needing to manage the AD DS environment in the cloud.  

Microsoft Entra Domain Services integrates with your existing Microsoft Entra tenant. This integration lets users sign into services and applications connected to the managed domain using their existing credentials. You can also use existing groups and user accounts to secure access to resources. These features provide a smoother lift-and-shift of on-premises resources to Azure.  

When you create a Microsoft Entra Domain Services managed domain, you define a unique namespace. This namespace is the domain name. Two Windows Server domain controllers are then deployed into your selected Azure region. This deployment of DCs is known as a replica set.  

You don't need to manage, configure, or update these DCs. The Azure platform handles the DCs as part of the managed domain, including backups and encryption at rest using Azure Disk Encryption.  

A managed domain is configured to perform a one-way synchronization from Microsoft Entra ID to Microsoft Entra Domain Services. You can create resources directly in the managed domain, but they aren't synchronized back to Microsoft Entra ID. In a hybrid environment with an on-premises AD DS environment, Microsoft Entra Connect synchronizes identity information with Microsoft Entra ID, which is then synchronized to the managed domain.  

## 3. Azure authentication methods <a name="question3"></a>

1. **Single sign-on**:  
    Single sign-on (SSO) enables a user to sign in one time and use that credential to access multiple resources and applications from different providers. For SSO to work, the different applications and providers must trust the initial authenticator.  
    Single sign-on is only as secure as the initial authenticator because the subsequent connections are all based on the security of the initial authenticator.  
2. **Multifactor authentication**:  
    Multifactor authentication is the process of prompting a user for an extra form (or factor) of identification during the sign-in process. MFA helps protect against a password compromise in situations where the password was compromised but the second factor wasn't.  
    Multifactor authentication increases identity security by limiting the impact of credential exposure (for example, stolen usernames and passwords). With multifactor authentication enabled, an attacker who has a user's password would also need to have possession of their phone or their fingerprint to fully authenticate.  
    Microsoft Entra multifactor authentication is a Microsoft service that provides multifactor authentication capabilities.  
3. **Passwordless authentication**:  
    Passwordless authentication methods are more convenient because the password is removed and replaced with something you have, plus something you are, or something you know.  
    Passwordless authentication needs to be set up on a device before it can work.  
    Microsoft global Azure and Azure Government offer the following three passwordless authentication options that integrate with Microsoft Entra ID:  
    - Windows Hello for Business:  
        The biometric and PIN credentials are directly tied to the user's PC, which prevents access from anyone other than the owner. With public key infrastructure (PKI) integration and built-in support for single sign-on (SSO), Windows Hello for Business provides a convenient method for seamlessly accessing corporate resources on-premises and in the cloud.
    - Microsoft Authenticator app:  
        Users can sign-in to any platform or browser by getting a notification to their phone, matching a number displayed on the screen to the one on their phone, and then using their biometric (touch or face) or PIN to confirm.
    - FIDO2 security keys:  
        The FIDO (Fast IDentity Online) Alliance helps to promote open authentication standards and reduce the use of passwords as a form of authentication. FIDO2 is the latest standard that incorporates the web authentication (WebAuthn) standard.  

## 4. Azure external identities <a name="question4"></a>

An external identity is a person, device, service, etc. that is outside your organization.  
External identities may sound similar to single sign-on. The external user’s identity provider manages their identity, and you manage access to your apps with Microsoft Entra ID or Azure AD B2C to keep your resources protected.  
The following capabilities make up External Identities:  
- **Business to business (B2B) collaboration** - Collaborate with external users by letting them use their preferred identity to sign-in to your Microsoft applications or other enterprise applications (SaaS apps, custom-developed apps, etc.). B2B collaboration users are represented in your directory, typically as **guest users**.
- **B2B direct connect** - Establish a mutual, two-way trust with another Microsoft Entra organization for seamless collaboration. B2B direct connect currently supports Teams shared channels, enabling external users to access your resources from within their home instances of Teams. B2B direct connect users aren't represented in your directory, but they're visible from within the Teams shared channel and can be monitored in Teams admin center reports.
- **Microsoft Azure Active Directory business to customer (B2C)** - Publish modern SaaS apps or custom-developed apps (excluding Microsoft apps) to consumers and customers, while using Azure AD B2C for identity and access management.

## 5. Azure conditional access <a name="question5"></a>

Conditional Access is a tool that Microsoft Entra ID uses to allow (or deny) access to resources based on identity signals. These signals include who the user is, where the user is, and what device the user is requesting access from.  
- Empower users to be productive wherever and whenever.
- Protect the organization's assets.

**Conditional Access** is **useful** when you need to:
- Require multifactor authentication (MFA) to access an application depending on the requester’s role, location, or network. For example, you could require MFA for administrators but not regular users or for people connecting from outside your corporate network.
- Require access to services only through approved client applications. For example, you could limit which email applications are able to connect to your email service.
- Require users to access your application only from managed devices. A managed device is a device that meets your standards for security and compliance.
- Block access from untrusted sources, such as access from unknown or unexpected locations.

## 6. Azure role-based access control (RBAC) <a name="question6"></a>

Azure provides built-in roles that describe common access rules for cloud resources. You can also define your own roles. Each role has an associated set of access permissions that relate to that role. When you assign individuals or groups to one or more roles, they receive all the associated access permissions.  

Role-based access control is applied to a scope, which is a resource or set of resources that this access applies to.  
Azure RBAC is hierarchical, in that when you grant access at a parent scope, those permissions are inherited by all child scopes.  

Azure RBAC is enforced on any action that's initiated against an Azure resource that passes through Azure Resource Manager. Resource Manager is a management service that provides a way to organize and secure your cloud resources.  
Azure RBAC uses an allow model. When you're assigned a role, Azure RBAC allows you to perform actions within the scope of that role. If one role assignment grants you read permissions to a resource group and a different role assignment grants you write permissions to the same resource group, you have both read and write permissions on that resource group.  

## 7. Zero Trust model <a name="question7"></a>

Zero Trust is a security model that assumes the worst case scenario and protects resources with that expectation. Zero Trust assumes breach at the outset, and then verifies each request as though it originated from an uncontrolled network.  
**Princilples:**
- **Verify explicitly** - Always authenticate and authorize based on all available data points.
- **Use least privilege access** - Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection.
- **Assume breach** - Minimize blast radius and segment access. Verify end-to-end encryption. Use analytics to get visibility, drive threat detection, and improve defenses.

## 8. Defense-in-depth <a name="question8"></a> 

The objective of defense-in-depth is to protect information and prevent it from being stolen by those who aren't authorized to access it.  
Layers:
- Physical security layer is the first line of defense to protect computing hardware in the datacenter.
- Identity and access layer controls access to infrastructure and change control.
- Perimeter layer uses distributed denial of service (DDoS) protection to filter large-scale attacks before they can cause a denial of service for users.
- Network layer limits communication between resources through segmentation and access controls.
- Compute layer secures access to virtual machines.
- Cpplication layer helps ensure that applications are secure and free of security vulnerabilities.
- Data layer controls access to business and customer data that you need to protect.

1. **Physical security:**  
    Physically securing access to buildings and controlling access to computing hardware within the datacenter are the first line of defense.
2. **Identity and access:**  
    The identity and access layer is all about ensuring that identities are secure, that access is granted only to what's needed, and that sign-in events and changes are logged.  
    - Control access to infrastructure and change control.
    - Use single sign-on (SSO) and multifactor authentication.
    - Audit events and changes.
3. **Perimeter:**  
    The network perimeter protects from network-based attacks against your resources. Identifying these attacks, eliminating their impact, and alerting you when they happen are important ways to keep your network secure.  
    - Use DDoS protection to filter large-scale attacks before they can affect the availability of a system for users.
    - Use perimeter firewalls to identify and alert on malicious attacks against your network.
4. **Network:**  
    At this layer, the focus is on limiting the network connectivity across all your resources to allow only what's required. By limiting this communication, you reduce the risk of an attack spreading to other systems in your network.  
    - Limit communication between resources.
    - Deny by default.
    - Restrict inbound internet access and limit outbound access where appropriate.
    - Implement secure connectivity to on-premises networks.
5. **Compute:**  
    Malware, unpatched systems, and improperly secured systems open your environment to attacks. The focus in this layer is on making sure that your compute resources are secure and that you have the proper controls in place to minimize security issues.  
    - Secure access to virtual machines.
    - Implement endpoint protection on devices and keep systems patched and current.
6. **Application:**  
    Integrating security into the application development lifecycle helps reduce the number of vulnerabilities introduced in code. Every development team should ensure that its applications are secure by default.  
    - Ensure that applications are secure and free of vulnerabilities.
    - Store sensitive application secrets in a secure storage medium.
    - Make security a design requirement for all application development.
7. **Data:**  
    Those who store and control access to data are responsible for ensuring that it's properly secured. Often, regulatory requirements dictate the controls and processes that must be in place to ensure the confidentiality, integrity, and availability of the data.

## 9. Microsoft Defender for Cloud <a name="question9"></a>

**Defender for Cloud** is a monitoring tool for security posture management and threat protection. It monitors your cloud, on-premises, hybrid, and multicloud environments to provide guidance and notifications aimed at strengthening your security posture.  
**Defender for Cloud** provides the tools needed to harden your resources, track your security posture, protect against cyber attacks, and streamline security management.  
**Defender for Cloud** helps you **detect threats** across:
- **Azure PaaS services** – Detect threats targeting Azure services including `Azure App Service`, `Azure SQL`, `Azure Storage Account`, and more data services. You can also perform anomaly detection on your Azure activity logs using the native integration with Microsoft Defender for Cloud Apps (formerly known as `Microsoft Cloud App Security`).
- **Azure data services** – `Defender for Cloud` includes capabilities that help you automatically classify your data in `Azure SQL`. You can also get assessments for potential vulnerabilities across `Azure SQL` and `Storage services`, and recommendations for how to mitigate them.
- **Networks** – `Defender for Cloud` helps you limit exposure to brute force attacks. By reducing access to virtual machine ports, using the just-in-time VM access, you can harden your network by preventing unnecessary access. You can set secure access policies on selected ports, for only authorized users, allowed source IP address ranges or IP addresses, and for a limited amount of time.

**Assess, Secure, and Defend:**  
- **Continuously assess** – Know your security posture. Identify and track vulnerabilities.
- **Secure** – Harden resources and services with Azure Security Benchmark.
- **Defend** – Detect and resolve threats to resources, workloads, and services.

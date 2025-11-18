# Active Directory

Active Directory simplifies the management of devices and users in an enterprise environment.

- The server running AD services is called a **Domain Controller (DC)**

- The server running certificate services is called [Active Directory Certificate Services](AD%20CS.md) (ADCS)

> The core of any Windows domain is the **Active Directory Domain Service (ADDS)**, which acts as a catalog containing information about all the "objects" that exist on the network.
> These objects can be: users, groups, machines, printers, shares, and many more.

# Users
Users are one of the objects called **Security Principals**, which means they can be authenticated by the domain and can be assigned privileges over **resources** such as files or printers.

Users can be used to represent two types of entities:

- **People:** Users will typically represent people in the organization who need access to the network, such as employees.

- **Services:** You can also define users that will be used by services like IIS or MSSQL. Each service requires a user to run under, but service users are different from regular users as they will only have the privileges needed to run their specific service.

> **Note:** A security principal is an object that can act on network resources.

# Computers
For each computer that joins the Active Directory domain, a machine object will be created. Machines are also considered "security principals" and are assigned an account just like any regular user.

This account has somewhat limited rights within the domain itself.

Identifying machine accounts is relatively simple. For example, a machine named `DC01` will have a machine account called `DC01$`.

# Groups
Groups can have both users and machines as members. If needed, groups can also include other groups.

> Security groups are also considered security principals and can therefore have privileges over network resources. Used to grant permissions on resources.

| **Security Group**                   | **Description**                                                                                                                                                             |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Domain Admins                        | Users in this group have administrative privileges over the entire domain. By default, they can administer any computer on the domain, including domain controllers.       |
| Server Operators                     | Users in this group can administer domain controllers. They cannot modify any administrative group memberships.                                                            |
| Backup Operators                     | Users in this group are allowed to access any file, ignoring their permissions. They are used to perform data backups on computers.                                        |
| Account Operators                    | Users in this group can create or modify other accounts in the domain.                                                                                                     |
| Domain Users                         | Includes all existing user accounts in the domain.                                                                                                                         |
| Domain Computers                     | Includes all existing computers in the domain.                                                                                                                             |
| Domain Controllers                   | Includes all existing domain controllers on the domain.                                                                                                                    |

Complete list of security groups in the [Microsoft documentation](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/active-directory-security-groups)

# Organizational Units
Organizational Units (OUs) are mainly used to define sets of users with similar policy requirements.

> A user can only be part of one organizational unit at a time.

# Delegation
Allows granting users specific privileges to perform advanced tasks on organizational units without requiring domain administrator intervention.

# Group Policy Objects (GPO)
Users and computers are organized into organizational units because the main idea behind this is to be able to deploy different policies for each OU individually.

This way, we can offer different configurations and security baselines to users based on their department.

Windows manages these policies through **Group Policy Objects (GPO)**, which are simply a set of settings that can be applied to OUs and can contain policies for `users` or `computers`, allowing you to define a baseline on specific machines and identities.

# Authentication Methods
When using Windows domains, all credentials are stored in the domain controllers. Whenever a user attempts to authenticate to a service using domain credentials, the service will need to ask the domain controller to verify if they are correct.

Two protocols can be used for network authentication in Windows domains:

- Kerberos
- NetNTLM (deprecated)

## Kerberos
Users who log into a service using Kerberos will be assigned tickets (proof of previous authentication).

Users with tickets can present them to a service to demonstrate that they have already authenticated to the network and are therefore authorized to use it.

The authentication process is as follows:

![](Images/kerberos-auth-1.png)
![](Images/kerberos-auth-2.png)
![](Images/kerberos-auth-3.png)

1. The user sends their username and a timestamp encrypted using a key derived from their password to the **Key Distribution Center (KDC)**, a service installed on the DC responsible for creating Kerberos tickets on the network.

2. The KDC will create and return a **Ticket Granting Ticket (TGT)**, which will allow the user to request additional tickets to access specific services.

> The need for a ticket to get more tickets allows users to request service tickets without passing their credentials every time they want to connect to a service. Along with the TGT, a **session key** is given to the user, which they will need to generate subsequent requests.

> Note that the TGT is encrypted using the password hash of the **krbtgt** account, so the user cannot access its content. It is essential to know that the encrypted TGT includes a copy of the session key in its content, and the KDC does not need to store the session key as it can retrieve a copy by decrypting the TGT if necessary.

3. When a user wants to connect to a service on the network such as a share, website, or database, they will use their TGT to request a **Ticket Granting Service (TGS)** from the KDC.

> TGS tickets only allow connection to the specific service for which they were created. To request a TGS, the user will send their username and a timestamp encrypted using the session key, along with the TGT and a **Service Principal Name (SPN)**, which indicates the name of the service and server we intend to access.

4. As a result, the KDC will send us a TGS along with a **service session key**, which we will need to authenticate to the service we want to access.

> The TGS is encrypted using a key derived from the **Service Owner Hash**. The service owner is the user or machine account under which the service runs. The TGS contains a copy of the service session key in its encrypted content so that the service owner can access it by decrypting the TGS.

5. The TGS can then be sent to the desired service to authenticate and establish a connection. The service will use its configured account password hash to decrypt the TGS and validate the service session key.

## NetNTLM
Works using a challenge-response mechanism. The authentication process is as follows:

![](Images/netntlm-auth.png)

1. The client sends an authentication request to the server it wants to access.

2. The server generates a random number and sends it as a challenge to the client.

3. The client combines its NTLM password hash with the challenge (and other known data) to generate a response to the challenge and sends it back to the server for verification.

4. The server forwards the challenge and response to the domain controller for verification.

5. The domain controller uses the challenge to recalculate the response and compares it to the original response sent by the client. If both match, the client is authenticated; otherwise, access is denied. The authentication result is returned to the server.

6. The server forwards the authentication result to the client.

> The described process applies when using a domain account and the user's password (or hash) is never transmitted over the network.

> If a local account is used, the server can verify the challenge response itself without requiring interaction with the domain controller, as the password hash is stored locally in its SAM.

# Trees, Forests, and Trusts

## Trees
Allows the integration of multiple domains that can be joined into a **Tree**.

Imagine a `microsoft.local` domain divided into two subdomains for UK and US branches. We could create a tree with a root domain of `microsoft.local` and two subdomains called `uk.microsoft.local` and `us.microsoft.local`, each with its own AD, computers, and users.

```
└───microsoft.local
    ├───uk.microsoft.local
    └───us.microsoft.local
```

This partitioned structure allows us to better control who can access what in the domain.

> A new security group must be introduced when talking about trees and forests. The **Enterprise Admins** group will grant a user administrative privileges over all domains in an enterprise.

## Forests

The union of multiple trees with different namespaces in the same network is called a **forest**.

## Trust Relationships
Trust relationships between domains allow authorizing a user from the `uk.microsoft.local` domain to access resources in the `us.microsoft.local` domain.

- The simplest trust relationship that can be established is a **one-way trust**.

In a one-way trust, if `Domain AAA` trusts `Domain BBB`, this means that a user on BBB can be authorized to access resources on AAA.

![](Images/trusts.png)

> The direction of the one-way trust is opposite to the direction of access.

- **Two-way trusts** can also be established to allow both domains to mutually authorize users from the other. By default, joining multiple domains under a tree or forest will form a two-way trust relationship.

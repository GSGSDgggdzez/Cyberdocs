# Active Directory Certificate Services

AD CS is Microsoft's implementation of Public Key Infrastructure (PKI).

AD CS is a privileged role and normally runs on selected domain controllers. AD CS is used for several things:

- File system encryption
- Creating and verifying digital signatures
- User authentication, making it a promising avenue for attackers.

> Certificates can outlive credential rotation, which means that even if a compromised account's password is reset, this will do nothing to invalidate the maliciously generated certificate, allowing persistent credential theft for up to 10 years!

Certificate request and generation flow:

![](Images/cs.png)

# Default Domain User Privileges
By default, any user who is a member of the Authenticated Users group (literally all AD accounts) can enroll up to 10 new machines on the domain.

This method is often used in organizations to allow users to bring their own device (BYOD) and enroll it for use on the domain. This is not really a vulnerability in itself, but it has led to privilege escalation vectors.

When we enroll a new host in AD, we are designated as the **owner** of that host. This gives us certain permissions on the AD object associated with that host.

Two permissions in particular are problematic here:
- **Validated Write to DNS Hostname** - This permission allows us to update the DNS hostname of our AD object associated with the host.

- **Validated Write to Service Principal Name (SPN)** - This permission allows us to update the SPN of our AD object associated with the host.

# Terminology

- **PKI (Public Key Infrastructure)** - A system that manages certificates and public key encryption.

- **AD CS (Active Directory Certificate Services)** - Microsoft's PKI implementation that typically runs on domain controllers.

- **CA (Certificate Authority)** - A PKI that issues certificates.

- **Certificate Template** - A set of parameters and policies that define how and when a certificate can be issued by a certificate authority.

- **CSR (Certificate Signing Request)** - A message sent to a certificate authority to request a signed certificate.

- **EKU (Extended/Enhanced Key Usage)** - Object identifiers that define how a generated certificate can be used.

Certipy is an offensive tool for enumerating and exploiting AD CS vulnerabilities and misconfigurations.

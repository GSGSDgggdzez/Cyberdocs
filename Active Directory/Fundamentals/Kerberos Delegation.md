# Kerberos Delegation

The ability to relay credentials can be given to a machine or service user if it has at least one SPN attribute.

There are three ways to authorize a machine or service account to impersonate a user to communicate with one or more other service(s):

[Unconstrained Delegation](../Attacking%20Kerberos/Unconstrained%20Delegation.md)

- Unconstrained Delegation
The server or service account that is assigned the `Unconstrained Delegation` right is able to impersonate a user to communicate with any service on any machine.

**Kerberos Constrained Delegation**
- Constrained Delegation
If a machine or service account has the `Constrained Delegation` flag, then a list of authorized services will be associated with this right.

**Resource Based Kerberos Constrained Delegation - RBCD**
- Resource-Based Constrained Delegation
In `Constrained Delegation`, it is at the delegating server level that the list of authorized SPNs is specified. In the case of `RBCD`, it is at the final services level that the list of services that can communicate with them via delegation is specified.

---
How can a machine or account impersonate a user to a resource?

---
layout: post
title: AWS security basics
image: /assets/img/aws-security-basics/cover.PNG
readtime: 15 minutes
---

### Physical Security

AWS take security very seriously, and there are many physical security measures that are taken place to improve security, such as the location of the AWS data centres, are not public knowledge, therefore not easy to find. Each data centre has controlled physical access, and has been rated the best in class in terms of data centre security. AWS has a lot of reputational damage to lose, so security is of upmost importance.

AWS has procedures and protocols in place and recieved accreditations from many security organisations such as:
HIPAA, Soc1, SSAE16, ISAE3402, Soc2, Soc3, PCI DSS, ISO 27000, RedRAMP, DIACAP, FISMA, ITAR, FIPS140-2, CSA, MPAA and more.

### Shared Security Responsibility

AWS works on a basis of shared security responsibility, which means that in order to remain secure, as a consumer you are expected to take some of the security responsibility. This tends to be split by:

AWS responsibility
- Virtual Host Security
- Physical Storage Security
- Network Security
- Data Centre Security
- Database Server Security

Customer responsibility
- AWS Account Security (MFA + API as well as console)
- Operating Systems
- Database Systems
- Applications running on Compute
- Data Encryption
- Authentication
- Network integrity.

## Security methods + Connectivity

There are many products available from AWS which aim to make the platform more secure, and are relatively simple to use. 

### Virtual private cloud level

You can use security groups and network control lists. A security group works as a virtual firewall to control inbound and outbound traffic. They work at the instance level, rather than the subnet level and a network control list acts as a firewall for controlling traffic in and out of one or more subnets.

Here is a more in depth comparison.

#### Security Groups
- Operates at the instance level (first layer of defense)
- Supports allow rules only
- Is stateful: Return traffic is automatically allowed, regardless of any rules
- We evaluate all rules before deciding whether to allow traffic
- Applies to an instance only if someone specifies the security group when launching the instance, or associates the security group with the instance later on

#### Network ACLs
- Operates at the subnet level (second layer of defense)
- Supports allow rules and deny rules
- Is stateless: Return traffic must be explicitly allowed by rules
- We process rules in number order when deciding whether to allow traffic
- Automatically applies to all instances in the subnets it's associated with (backup layer of defense, so you don't have to rely on someone specifying the security group)

### Other defences

AWS offers a more secure offering for network traffic between your office and the AWS data centre, called Direct Connect. It can reduce network costs, increase bandwidth throughput, and provide a more consistent network experience than Internet-based connections.

There is also a product that is available as a service called WAF (Web Application Firewall). A web application firewall can help to  protect web applications from common web exploits that could affect application availability, compromise security, or consume excessive resources.

More of a compliance issue, but it is also possible to provision compute resources as "Dedicated Servers" which cost much more, but mean that the compute resources you use, are not multi-tenant. 

## Identity and Access management.

IAM allows you to manage access to AWS services and resources securely. You can use it to create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources. IAM is also free of charge!

There are four main types of identity and access management, and use an RBAC type model.

#### Users
- Users can have permissions directly, or belong to a group, where the group stipulates the permissions
#### Groups
- Are used to group a bunch of permissions, for easier assigning to a user or multiple users.
#### Roles
- You apply a role to an User or an Instance. Roles are meant to be "assumed" rather than granted like you would in a group (i.e. its a temporary infation of privaledges).
#### Policies
- Policies are a collection of permissions that can be applied to users, groups or policies.

### Setting up policies

The policy language you use when creating permissions using IAMs has two elements. Specification (defining access policies) and Enforcement (evaluating policies). Policys are written in JSON, and each statement should contain "PARC"
- Principle
- Action
- Resource
- Condition

### Principal

A principal is an entity which is allowed or denied access to a resource. This can be indicated in different ways e.g.
```
- Anonymous Users
"Principal":"AWS":"*.*"  

- Specific Accounts
"Principal":{"AWS":"arn:aws:iam::123456789012:root"} 

- Individual IAM User
"Principal":{"AWS":"arn:aws:iam::123456789012:user/name"}

- Federated User
"Principal":{"Federated":"www.amazon.com"}

- Specific Role
"Principal":{"AWS":"arn:aws:iam::123456789012:role/rolename"}

- Specific Service
"Principal":{"Service":"ec2.amazonaws.com"}
```


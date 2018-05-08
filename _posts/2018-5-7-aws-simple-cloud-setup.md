---
layout: post
title: Setting up a simple cloud in AWS
image: /assets/img/aws-simple-cloud-setup/cover.jpg
readtime: 13 minutes
---

## Setting up a simple cloud

I do a lot of terraform configuration at work, but never had a chance to look at how to provision stuff the correct way, and within the AWS management console, so I've working to understand the basics of AWS architecture, to improve my knowledge and skills.

### What is a Virtual Private Cloud?

A VPC is a logically isolate network within te AWS global network. It is the primary subnet, that can be split into multiple smaller subnets, and allows you to control all your network infrastructure.

It allows for enhanced security against everything that sits within it, and is typicaly secured using network control lists (NCLs). You can also use a VPC to internetwork with other organisations or accounts, using VPC peering, to join VPCs together. You can also assign public IP addresses from within the VPC (in AWS these are termed Elastic IP addresses), you can also seup hybrid clouds, using site-to-site VPN. VPC is free within AWS, as it is everything else inside, which you pay for.

### VPC Elements

In the AWS console, there are various things you can setup, such as:
- Subnets
- Route Tables
- Internet Gateways
- Elastic IPs
- Endpoints
- NAT Gateways
- Peering Connections
- Network ACLs
- Security Groups
- VPNs

### VPC Characteristics

When setting up a subnet within a VPC, there a few quirks that are good to be aware of.

- AWS reserves 5 IP addresses per subnet, which is typically the first 4 and the last 1. These are used for management purposes. Also a subnet can either be made Public, Private or VPN only

- Subnets cannot span availability zones (as they site within a single AZ).

- VPCs span across a single region, but can span across multiple availability zones.

- When specifying a CIDR block, you can only specify between 16 and 28 (no more or less).

- You can specify the IP Prefix within the VPC.


### VPC Security

There are pros and cons for applying different security measures in AWS against a VPC. The two types of security you can apply are Security Groups, and Access Control lists.

Security Groups feature:
- Resource level traffic firewall, meaning you can block by resource such as Instance, ELB etc.
- Ingress and Egress rules
- Is stateful (return traffic is allowed)

Access Control Lists feature:
- Source and protocol filtering
- Subnet level traffic firewall
- Ingress and Egress rules are seperate
- Is stateless (traffic is strictly filtered and return traffic has to be specified.)

### An Example of setting up a simple VPC 

<amp-img src="/assets/img/aws-simple-cloud-setup/simple-architecture.png"
  width="936"
  height="674"
  layout="responsive">
</amp-img>

In this example I am designing a simple cloud structure.

First you need to create the VPC, and set the IP prefix to something like `192.168.0.0/16` and set the tenancy to default.

You then want to create 3 subnets, and set the CIDR block to be 192.168.1.0/24, 192.168.2.0/24 and 192.168.3.0/24 respectively. 

We are going to treat 1.0 as out DMZ containing our web servers and NATs, 2.0 as our DB server, and 3.0 as our Application servers.

Next add an Internet Gateway and attach to the VPC

Then add a new Route Table and attach to the VPC

Next add a route to the route table, selecting the internet gateway, and assign it to everyone 0.0.0.0/0.

Then add a subnet association, and select our DMZ subnet, 192.168.1.0/24

If you bring up an EC2 instance within the 192.168.1.0 subnet, and run a curl command, you should find that the box has internet traffic. 




Next create two
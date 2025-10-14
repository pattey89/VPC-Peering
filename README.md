<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** PATRICK ADDAI  
**Email:** patrickaddai1689@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational networking service that lets us create our own networks, control traffic flow and security and organise our resources into public/private subnets!

### How I used Amazon VPC in this project

We used Amazon VPC to set up a multi-VPC architecture (we set create a peering connection between them AND update security group rules ti run a successful connectivity test to validate our VPC peering set up/.

### One thing I didn't expect in this project was...

I didn't expect to need a public IPv4 address for EC2 Instance Connect to work. Also I didn't expect that Elastic IPs can assign static pulic IPv4 addresses to resources. 

### This project took me...

This project took me 2.5 hours including demo time.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, we are using the VPC resource map/launch wizard to create TWO VPCs and their components in just minutes.

### Step 2 - Create a Peering Connection

We are setting up a VPC Peering Connection, which is a VPC component designed to directly connect two VPCs together.

### Step 3 - Update Route Tables

In this step I will modify the route table to allow connection flow from one VPC to another.

### Step 4 - Launch EC2 Instances

I am launching an EC2 instances in each of the VPCs (VPC 1 and VPC 2) so that I can directly connect with my instances later and test my VPC peering connection.

---

## Multi-VPC Architecture

I started my project by launching two VPcs - they have unique CIDR Block and each have one public subnet.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16. Each VPC must have a unique IPv4 CIDR block so the IP addresses of their resources don't overlap

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances as EC2 Instance Connect, AWS actually manages a key pair for us. EC2 instance Connect will directly connect with my EC2.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a direct connection between two VPCs.

VPCs would use peering connections to lets VPCs and their resources route traffic between them using their private IP addresses. This means data can now be transferred between VPCs without going through the public internet. Without a peering connection, data transfers between VPCs would use resources' public address - meaning VPCs have to communicate over the public internet. . 

The difference between a Requester and an Accepter in a peering connection is that  the Requester is the VPC that initiates a peering connection whiles the Accepter is the VPC that receives a peering connection request!

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because the default route table doesn't have a route using the peering connection yet - this needs to be set up so that resources can be directed to the peering connection when trying to reach the other VPC.

My VPCs' new routes have a destination of the other VPC's CIDR block. The routes' target was the peering connection we set up.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step I am using EC2 instance connect to connect directly with my first EC2 instance. I need to do this because I need to use my EC2 instance for connectivity test ( to validate my VPC peering set up) later in this project.

### Step 6 - Connect to EC2 Instance 1

I am reattempting my connection to instance - Nextwork VPC 1, and resolving another error preventing me from using EC2 instance Connect to directly connect with the instance.


### Step 7 - Test VPC Peering

I am going to use the instance Nextwork VPC 1 to attempt a direct connection with the instance - Nextwork VPC 2 so that I can validate that my peering connection is set up properly.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to directly connect with my EC2 instance - Nextwork VPC 1 just by using the AWS Management Console.

I was stopped from using EC2 Instance Connect as my instance did not have a public IPV4 address. In order for EC2 Instance Connect to work, the EC2 Instance must have a public IPV4 address and be in a public subnet!

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static IPv4 addresses that get allocated to your AWS account, and is yours to delegate to an EC2 instance.

Associating an Elastic IP address resolved the error becauseit gives my EC2 instance a public IP address, fulfilling the requirements for instance Connect to work!

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command ping [the Private IPv4 address of  the other EC2 instance in VPC 2].

A successful ping test would validate my VPC peering connection - this ping test would not get ANY reply from the other EC2 instance if the peering connection did nt succesfully connect our two VPCs. Getting ping replies = peering connection was set up properly.

I had to update my second EC2 instance's security group because it was not letting in ICMP traffic whihc is the traffic type of a ping message. I added a new rule that allows ICMP traffic coming in from any resource in VPC2.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-peering_7a29d352)

---

---

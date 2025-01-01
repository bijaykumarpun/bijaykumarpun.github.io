---
layout: post
title: "Elastic IP Address"
date: 2025-01-01 12:00:00
description: "Elastic IP Addresses in AWS"
---

---
# Elastic IP in AWS

An **Elastic IP (EIP)** in AWS is a static, public IPv4 address designed for dynamic cloud computing. It allows you to mask the failure of an instance or software by quickly remapping the address to another instance in your AWS environment.

## Key Characteristics of Elastic IP
1. **Static Address**: Unlike regular public IPs that change when an instance is stopped and restarted, an Elastic IP remains the same until you explicitly release it.

2. **Reassignable**: You can detach an Elastic IP from one instance and reattach it to another, making it ideal for fault-tolerant applications.

3. **Public Access**: Elastic IPs are used to enable external communication with your instances (e.g., web servers or application servers that need to be accessible over the internet).

4. **Billing**: AWS charges for unused Elastic IPs. If you allocate an Elastic IP but don't associate it with a running instance, you incur a charge. This encourages efficient use of Elastic IPs.

## Use Cases
- **Failover and High Availability**: You can move the Elastic IP from a failed instance to a backup instance to quickly restore services.
- **Consistent Endpoint**: If your application requires a fixed IP address for whitelisting or DNS configurations, an Elastic IP ensures consistency.

## How to Use an Elastic IP
1. **Allocate an Elastic IP**:
   - Navigate to the EC2 dashboard in AWS Management Console.
   - Choose "Elastic IPs" from the left menu and click "Allocate Elastic IP address."

2. **Associate with an Instance**:
   - Once allocated, you can associate the Elastic IP with a running EC2 instance.
   - The Elastic IP will replace the instance's public IP address.

3. **Reassign or Release**:
   - You can detach the Elastic IP from one instance and attach it to another.
   - If no longer needed, release the Elastic IP to avoid charges.

## Advantages
- Provides a stable public IP for instances that may need to change frequently.
- Supports disaster recovery and scaling by quickly reassigning the IP to different resources.

## Limitations
- There is a default limit of 5 Elastic IPs per AWS account per region (can be increased via a service request).
- You may incur charges for Elastic IPs not associated with a running instance.

Elastic IPs are a critical tool for managing public-facing applications in the AWS cloud while maintaining reliability and flexibility.

*Summarized with ChatGPT
---
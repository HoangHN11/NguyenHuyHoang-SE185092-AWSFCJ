---
title: "Blog 2"
date: 2025-10-08
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---
---

# How Salesforce Business Technology Uses AWS Direct Connect SiteLink for Reliable Global Connectivity

*By Alexandra Huides and Corey Harris Jr – May 9, 2025, in the AWS Direct Connect SiteLink section.*

---

## Introduction

**Salesforce Business Technology** has used **AWS Direct Connect SiteLink** to build a global hybrid network architecture, ensuring flexible, high-performance, and reliable connectivity.  
This solution helped Salesforce scale its infrastructure, reduce operational costs, and accelerate innovation in its journey toward cloud modernization with AWS.

> *This article is brought to you in collaboration with Georgi Stoev and Ravi Patel – senior technical experts at Salesforce.*

---

## Overview

**Salesforce** is an AWS strategic partner and the world leader in customer relationship management (CRM).  
The **Business Technology** team is responsible for building and operating enterprise applications that support areas such as finance, data centers, security, data warehousing, and Salesforce's virtual machines.

With a global presence, Salesforce needed a network architecture that was:
- **Flexible and highly scalable.**  
- **Minimized latency and downtime.**  
- **Ensured high security and reliability.**

However, traditional internet-based network solutions couldn't meet these stringent requirements.  
This is why **AWS Direct Connect SiteLink** was chosen — providing a **private, dedicated connection**, bypassing the public internet to significantly improve security and latency.

---

## Prerequisites

Before deployment, the Salesforce technical team understood the following AWS network components:
- **Amazon Virtual Private Cloud (VPC)**  
- **AWS Transit Gateway**  
- **AWS Direct Connect**

These services form the foundation for the global hybrid network architecture, allowing for private, low-latency connectivity between multiple Direct Connect locations without going through intermediate AWS regions.

---

## AWS Direct Connect SiteLink

**AWS Direct Connect** provides a private network connection between on-premises infrastructure and AWS, optimizing performance, latency, and reliability.

**SiteLink** is an extension feature of Direct Connect that allows direct connections between on-premises networks via the **global AWS backbone**, enabling:
- Data transmission through the **shortest path**, bypassing AWS regions.  
- Leveraging the **global AWS network** to transfer data quickly and securely.  
- Pay-per-use pricing, without needing to establish new connections.

How it works:
1. Establish an on-premises connection to AWS at one of over **100 Direct Connect locations** worldwide.  
2. Create a **Virtual Interface (VIF)** on that connection and enable **SiteLink**.  
3. When VIFs are attached to the same **Direct Connect Gateway (DXGW)**, data is transmitted directly between locations using the AWS backbone.

---

## Salesforce Business Technology's Global Footprint

Salesforce Business Technology manages **7 strategic locations** globally:
- 3 in the United States  
- 3 in the Asia-Pacific region  
- 1 in Europe  

The network is built on **private MPLS backbone links** combined with **AWS Regions**, supporting complex data flows between data centers and cloud environments.

However, challenges arose including:
- **Static and hard-to-scale infrastructure.**  
- **High operational costs** and heavy reliance on multiple providers.  
- **Routing complexity** and **outages in some regions.**

![Blog Image 2 - 1](/images/3-BlogImage/blog2-1.png)
> *Figure 1. A sample global private data center connection using dedicated circuits.*

---

## Solution: SiteLink

To solve these problems, Salesforce Business Technology **modernized its network infrastructure** by deploying **SiteLink**.  
The main objectives were:
- Build a flexible, scalable network as needed.  
- Reduce operational costs and complexity.  
- Enhance resilience and security.

The team:
- Deployed SiteLink on **existing Direct Connect connections**.  
- Created new **dedicated VIFs** for production and development environments.  
- Maintained a **global segmentation** to meet on-premises data storage requirements.

![Blog Image 2 - 2](/images/3-BlogImage/blog2-2.png)
> *Figure 2. Sample global SiteLink deployment for Production and Development.*

---

## Achieved Benefits

The SiteLink solution delivered several outstanding benefits for Salesforce:

| Benefit | Description |
| ------- | ----- |
| **Simplified network management** | Eliminated the complexity of MPLS Layer 3 VPN routing while maintaining traffic isolation. |
| **Improved performance** | Increased stability, reducing global average latency by 15%. |
| **Cost optimization** | Utilized existing connections with pay-per-use billing. |
| **Enhanced security** | Applied MACSec Layer 2 encryption on all Direct Connect connections. |

Additionally, SiteLink helps:
- **Reduce single points of failure (SPOF)** and improve network reliability.  
- **Optimize data path routing** between data centers.  
- **Comprehensive monitoring** via CloudWatch Network Monitor.

> *“With SiteLink, Salesforce Business Technology has streamlined network operations and ensured maximum resilience for global connectivity. We can set up connections between 7 data centers in just a few minutes and expand into new markets in a few days.”*  
> — *Ravi Patel, Senior Technical Director at Salesforce.*

---

## Conclusion

Adopting **AWS Direct Connect SiteLink** has helped Salesforce:
- Unify its global network architecture.  
- Modernize infrastructure, reduce costs, and improve performance.  
- Be ready for scaling and rapid innovation.

> *To learn more about AWS Direct Connect SiteLink, you can refer to the official documentation or ask questions on AWS re:Post.*

---

## About the Authors

> ![Alexandra Huides](/images/3-BlogImage/blog2-3.png)  
> **Alexandra Huides**  
> *Senior Network Solutions Architect at AWS.*  
> Specializes in large-scale network architecture, helping clients adopt IPv6 and build flexible environments. Outside of work, she enjoys kayaking, traveling, and reading books.

---

> ![Corey Harris Jr](/images/3-BlogImage/blog2-4.jpg)  
> **Corey Harris Jr.**  
> *Senior Solutions Architect at AWS.*  
> A network and serverless expert, helping customers optimize their AWS systems. Outside of work, he enjoys gaming, traveling, and spending time with family.

---

> ![Georgi Stoev](/images/3-BlogImage/blog2-5.png)  
> **Georgi Stoev**  
> *Senior Technical Architect at Salesforce.*  
> With over 20 years of experience in networking, AI, and security, he is passionate about technology, beekeeping, and nature exploration.

---

> ![Ravi Patel](/images/3-BlogImage/blog2-6.jpg)  
> **Ravi Patel**  
> *Senior Technical Director at Salesforce.*  
> With over 15 years of experience in building flexible and high-performance networks, he enjoys surfing, mountaineering, and adventuring around the world.

---
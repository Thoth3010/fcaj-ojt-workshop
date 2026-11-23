---
title: "Week 2 Worklog"
date: 2026-11-23
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

{{% notice info %}}
📝 **`[TODO - Update later]`:** Review and adjust daily work items below to match your exact personal schedule if needed.
{{% /notice %}}

### Week 2 Objectives (21/09/2026 – 25/09/2026)

* Master AWS virtual networking: **Amazon VPC**, Public/Private Subnets, Route Tables, IGW, and NAT Gateway.
* Launch, harden, and administer **Amazon EC2** instances using Security Groups and **Systems Manager Session Manager**.

### Daily Worklog

| Day | Tasks | Start Date | Completion Date | References |
| :-: | :--- | :---: | :---: | :--- |
| **Mon** | - Studied **Amazon VPC** fundamentals: CIDR planning and Multi-AZ Public vs. Private Subnet isolation. | 21/09/2026 | 21/09/2026 | <https://docs.aws.amazon.com/vpc/> |
| **Tue** | - Built a custom VPC (`10.20.0.0/16`), attached Internet Gateway, configured Route Tables, and applied restrictive Security Groups. | 22/09/2026 | 22/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| **Wed** | - Explored **Amazon EC2** instance families (`t3`, `m7i-flex`, `g4dn` GPU), EBS `gp3` volumes, and On-Demand vs. Spot pricing. | 23/09/2026 | 23/09/2026 | <https://docs.aws.amazon.com/ec2/> |
| **Thu** | - Provisioned Ubuntu 24.04 LTS on EC2 with UserData bootstrap and connected securely via **SSM Session Manager** without opening port 22. | 24/09/2026 | 24/09/2026 | <https://docs.aws.amazon.com/systems-manager/> |
| **Fri** | - Practiced full lab teardown (EC2 termination, EBS/SG/VPC cleanup) and verified `$0.00` billing status. | 25/09/2026 | 25/09/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 2 Key Achievements

* Successfully built a Multi-AZ VPC separating public edge resources from private compute/data tiers.
* Eliminated SSH exposure (port 22 closed) by adopting SSM Session Manager for EC2 operations.
* Reinforced zero-waste resource clean-up habits after every lab.

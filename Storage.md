# Elastic Block Storage

Amazon EBS Snapshots are an easy and safe way to back up your EBS volumes (like your EC2 storage or boot volume).  
They create a point-in-time copy of your data — meaning it saves everything exactly as it was at that moment.

**Def: Persistent block storage that can be attached to an instance.**

- Survives instance stop/terminate (if not explicitly deleted).
- Can take snapshots (backups).
- Can be attached to multiple instances (read-only) in some cases.

### Use Case:
- Databases
- OS disks, application storage.

### Benefits:
- Simple and automated
- Cost-effective
- Secure
- Highly available and durable



### Types of Amazon EBS Volumes

EBS volumes come in two main categories:

1. SSD-based (for faster performance)  
2. HDD-based (for big data, lower cost)

1. gp3 (General Purpose SSD) – Balanced, default option.  
2. io1/io2 (Provisioned IOPS SSD) – High performance, low latency.  
3. st1 (Throughput Optimized HDD) – For big data, log processing.  
4. sc1 (Cold HDD) – Cheapest, less frequent access.



### Comparision table:

| EBS Type | Performance | Best Use Case | Cost Level |
|----------|-------------|-------------------------------|-------------|
| io2 | 🔥 Very High | Critical databases, enterprise apps | 💰💰💰 (Most costly) |
| io1 | 🚀 High | High-performance databases | 💰💰 (Costly) |
| gp3 | ⚡ Medium–High | Web apps, general workloads | 💰 (Balanced / Best value) |
| gp2 | ⚙️ Medium | Test servers, small databases | 💵 (Moderate) |
| st1 | 📀 Low–Medium | Big data, log processing | 🟩 (Cheap) |
| sc1 | 🧊 Low | Backups, rarely accessed data | 🟩 (Cheapest) |


# 2. AMI (Amazon Machine Image)

An Amazon Machine Image (AMI) is a pre-configured template
that provides the necessary information to launch an EC2
instance in AWS. <br>
With an AMI, you can launch new EC2 instances with
a consistent, predefined configuration.<br>


You can also create custom AMIs to include specific
software or settings, allowing for quick replication of
environments.<br>
<br><br><br>



### It includes:

- Operating system (e.g., Linux, Windows)

- Application server (e.g., Apache, Nginx)

- Pre-installed software and configurations<br><br>


Types of AWS AMIs


- Public AMIs: Available to all AWS users. Useful for basic use
cases like popular operating systems (e.g., Ubuntu, CentOS).


- Private AMIs: Created by a user and only available within that
account or shared with specific accounts.


- Paid AMIs/Marketplace AMIs: Provided by third parties
through AWS Marketplace, offering software like databases,
web servers, or pre-configured environments.
<br><br><br>
### Common use cases for each type:


- Public: Testing or development environments.

- Private: Customized setups for production.

- Marketplace: Deploying pre-built solutions (e.g.,
enterprise software).<br><br>

# Run Cleanup Script
#!/bin/bash

### Remove SSH keys----  rm -rf ~/.ssh/authorized_keys


- Clear user credentials and history

rm -rf ~/.aws/credentials<br>

rm -rf ~/.git-credentials<br>

rm -rf ~/.bash_history<br>


-  Clean system logs and temporary files

rm -rf /var/log/*<br>

rm -rf /tmp/*<br>

rm -rf /var/tmp/*<br>


- Remove user accounts

deluser tempuser --remove-home<br>


- Lock root account

passwd -l root<br>


- Reset configuration files (example for Nginx)

rm -rf /etc/nginx/nginx.con<br>







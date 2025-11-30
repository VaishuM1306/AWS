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

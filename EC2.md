# EC2 (Elastic Cloud Computing )<br>
•	Amazon EC2 is a core AWS service that provides virtual servers (instances) on demand. <br>
•	It eliminates the need to invest in physical hardware — you can provision compute capacity in minutes.<br> 
•	It’s called “elasticc” because resources can scale up or down based on demand. <br>


# Instance Types 
###  Definition: Defines the hardware configuraƟon of an instance (CPU, RAM, storage, networking).
**  Families of Instance Types: **
1. General Purpose → Balanced CPU + memory (e.g., t2, t3, m5,a).<br>
2. Compute Optimized → High CPU performance (e.g., c5)<br>.
3. Memory Optimized → For RAM-heavy workloads (e.g., r5, x1).<br>
4. Storage Optimized → For high disk throughput (e.g., i3, d2).<br> 
5. Accelerated CompuƟng → GPU, FPGA for ML/AI (e.g., p3, g4).<br><br><br>

# EC2 Purchase Plans 

1. **On-Demand** – Pay per use, no commitment, expensive.  <br> 
2. **Reserved Instances (RI)** – 1/3 year commitment, cheaper, steady workloads.<br> 
3. **Savings Plans** – Commit $/hour, flexible, up to 66% discount.  <br> 
4. **Spot Instances** – Use unused capacity, very cheap, can be terminated anytime.  <br> 
5. **Dedicated Hosts** – Entire server for you, expensive, compliance/BYOL.  <br> 
6. **Dedicated Instances** – Isolated hardware, cheaper than hosts, compliance workloads. <br>  
7. **Capacity Reservations** – Reserve capacity in AZ, no long-term commitment.<br><br>

# Placement Groups 
DefiniƟon: Control how your EC2 instances are placed across hardware. 
### Types: 
1. Cluster Placement Group → Instances packed closely for low-latency, high throughput.<br>
2. Spread Placement Group → Instances spread across different hardware for fault tolerance.<br>
3. ParƟƟon Placement Group → Instances grouped into parƟƟons; used in big data, Hadoop clusters.<br>


# Elastic IP (EIP) – AWS 

- **Definition:** Static public IPv4 address for EC2 that doesn’t change when instance stops/starts.
- **Features:**
  - Static & remappable to any instance in the same region.
  - Free when associated with a running instance; charged if unused.
  - Default limit: 5 per region.
  - IPv4 only.
- **Use Cases:**
  - Maintain static IP for web servers, DNS, VPN.
  - Failover & high availability.
- **Limitations:**
  - Charges for unused EIP.
  - One EIP per instance.
  - Cannot attach across regions.
- **Example:**  
  Re-associate EIP from a crashed EC2 to a new EC2 → users continue accessing without interruption.



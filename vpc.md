# vpc
-	Amazon VPC lets you create a logically isolated network inside AWS. 
-	 You control IP ranges, subnets, routing, firewalls, and connectivity.
- It’s like building your own data center inside AWS. 
- Every AWS account gets a default VPC, but you can also create custom VPCs for more control.
- You can have multiple VPC in ASW region (max 5oer region-soft limit)
- Currently, Amazon VPC supports VPCs between /28 (in CIDR notation) and /16 in size for IPv4.
-	The IP address range of your VPC should not overlap with the IP address ranges of your existing network.
-	One can create 200 subnets per VPC.
-	The minimum size of a subnet is a /28 (or 14 IP addresses)	There are 2 levels of security within the VPC itself
-	Security Groups which control the flow of traffic at an instance (EC2) level.
-	Network Access Control lists which control the traffic at a subnet level.
-	Amazon VPC Flow logs can be used to monitor traffic within a VPC.
-	A VPC can span multiple Availability Zones by using multiple subnets.



# 🧭 Default VPC – 
-	Default VPC is a pre-created Virtual Private Cloud provided by AWS in every region.
-	It lets you launch EC2 instances instantly with Internet access, without any network setup.

  
### 🧠 Note
-	Only one Default VPC per region
-	All subnets are public
-	Do not delete the Default VPC
-	For production, create a Custom VPC with private<br><br><br><br><br>


# 1.CIDR Block (IP Range) 
•	A CIDR (Classless Inter-Domain Routing) block defines the IP address range of your VPC.<br>
•	Example: 10.0.0.0/16 → gives you 65,536 IPs.<br>
•	Each subnet inside the VPC gets a smaller CIDR block. <br>
•	AWS reserves 5 IPs per subnet (first 4 + last 1). <br>
•	Use /16 for large VPCs (many subnets)<br>
•	Use /24 for small subnets (common)<br><br><br>

### Example Subnet division: 
 VPC CIDR: 10.0.0.0/16 <br>
Public Subnet: 10.0.1.0/24 (256 IPs)<br> 
 Private Subnet: 10.0.2.0/24 (256 IPs) <br>
Rule: You can’t overlap CIDR blocks if you plan to connect VPCs (peering/TGW).
<br><br><br><br>
# 🌐 2. What is a Subnet?( AZ)
- A Subnet (short for subnetwork) is a smaller section of your VPC’s IP address range.
- It divides your VPC CIDR block into smaller parts to organize and control network traffic.<br>
In AWS:
-	A VPC = your private virtual network
- A Subnet = a segment inside that network
- where you place your EC2 instances, databases, etc.

### Why Do We Need Subnets?
Because you want to:
•	Separate resources logically (e.g., web, database, application tiers)
•	Control access and routing (e.g., public vs. private)
•	Increase availability by spreading subnets across Availability Zones (AZs)<br><br><br>
### Types of Subnets
### There are mainly two types of subnets in AWS:
### 1️⃣ Public Subnet
•	Has a route to the Internet Gateway (IGW)
•	Used for web servers, bastion hosts, load balancers
•	Instances can get public IPs to access the Internet
•	Eg.use for web deployment

### 2️⃣ Private Subnet
•	No direct Internet access
•	Used for databases, backend services, internal apps
•	If Internet access is needed, traffic goes via a NAT Gateway

### 3️⃣ Isolated Subnet
•	No Internet access at all
•	Used for most secure internal workloads (e.g., internal data stores)
•	Use for database

### 🧭  Summary Table

| Concept | Explanation |
|--------|-------------|
| Subnet | A smaller range inside a VPC CIDR |
| Public Subnet | Has route to Internet Gateway |
| Private Subnet | Has route to NAT Gateway |
| Routing | Controlled by Route Table |
| IP Reservation | 5 IPs per subnet reserved |
| Purpose | Organize and isolate resources logically |



<br><br><br><br><br><br>
# 🌐 3. What is a Route Table?[ Region-Specific]
A Route Table is a set of rules that decides where network traffic is directed inside your VPC.<br>
Each rule is called a route, and it tells AWS where to send packets that match a specific destination IP range.<br>
In short:<br>
🧩 Route Table = Navigation Map for Your VPC Network Traffic<br>


- Component	Description
Destination	IP range (CIDR block) for traffic to match<br>
Target	The next hop or gateway to send traffic to (e.g., IGW, NAT, Peering, Local)<br>
Local Route	Automatically added route for communication within the VPC (cannot be deleted)<br><br><br>

- 🧾 Short Notes (for quick revision)<br>
•	Route Table: Set of rules deciding where traffic goes in a VPC.<br>
•	Default Route Table: Auto-created; used by new subnets.<br>
•	Local Route: Always present for internal VPC traffic.<br>
•	Public Subnet: Has route → Internet Gateway.<br>
•	Private Subnet: Has route → NAT Gateway.<br>
•	Each subnet → 1 route table (but table can serve many subnets).<br>
•	Used for: Internet access, peering, VPN, and internal routing.<br><br><br><br><br>



# 🌐4. Internet Gateway (IGW) — (Region)
🔹 Definition    FREE ✅
Internet Gateway (IGW) is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the Internet.<br>
Ist is used provide internate to public subnet.
### Very Important Practical Points
⭐ A subnet becomes public only when:<br>
1.	Its Route Table has route to IGW<br>
2.	Its instances have Public or Elastic IPs<br>
3.	Security Group allows inbound/outbound traffic<br>
4.	VPC has IGW attached<br>
5.	 IGW → Works at VPC level, not subnet level.<br>
6.	IGW → Mandatory for NAT Gateway (public subnet).<br>
### Interview-Focused Key Takeaways (Remember These!)<br>
1.	⭐ IGW must be attached to VPC → No Internet access without it.<br>
2.	⭐ Route Table must have 0.0.0.0/0 → igw-id.<br>
3.	⭐ Instance must have Public / Elastic IP to use IGW.<br>
4.	⭐ One IGW per VPC (cannot attach multiple IGWs).<br>
5.	⭐ IGW required for NAT Gateway to work.<br>
6.	⭐ IGW handles 1:1 NAT automatically.<br>
7.	⭐ Security Group + NACL rules must allow traffic for IGW connection.<br>
8.	⭐ VPC is isolated until IGW is attached.<br>
9. ⭐ Supports both IPv4 (0.0.0.0/0) and IPv6 (::/0) for Internet routes.<br>
<br><br><br><br><br>
# 5.AWS NAT Gateway  (AZ-specific)
What is a NAT Gateway?     [ PAID  💸] US $0.045 per hour.<br>
NAT Gateway (Network Address Translation Gateway) is a managed AWS service that allows instances in a private subnet to access the Internet, without exposing them to inbound Internet traffic.<br>
➡️ Purpose:
 Allow outbound Internet connections from private subnets (for updates, downloads, etc.)
while keeping inbound access blocked for security.<br>
1️⃣ Give Internet access to private subnet instances (outbound only)<br>
2️⃣ Hide private IPs from the Internet (security)<br>
3️⃣ Translate private IP → public IP for outbound traffic<br>
4️⃣ Work with IGW to send traffic to the Internet<br>
5️⃣ Allow private EC2s to download updates or access APIs<br>
6️⃣ One NAT can serve multiple private subnets (in same AZ)<br>
7️⃣ No inbound connections allowed – outbound only<br>

### ⚙️ Types of NAT (Network Address Translation) in AWS
Use    NAT Gateway in production for reliability and scale.<br>
       NAT Instance is older, used mainly for testing or custom routing.”<br><br>

 ###🔄 NAT Gateway vs NAT Instance Comparison

| Point | NAT Gateway | NAT Instance |
|-------|-------------|--------------|
| Management | ✅ AWS managed (no admin needed) | ❌ User managed |
| Scalability | Auto scales | Manual scaling |
| Availability | Highly available (within AZ) | Single point of failure |
| Performance | High & consistent | Depends on EC2 size |
| Security Groups | Not used | Can attach SGs |
| Cost | Higher | Cheaper but more effort |
| Use Case | Production | Testing / custom setup |
<br><br><br><br>


# 🌐6. AWS Transit Gateway (TGW)   (Region / Inter-Region optional)<br>
Definition [Paid 💸 ]<br>
•	TGW = a central hub that connects multiple VPCs, VPNs, and on-premises networks.<br>
•	Simplifies network management and reduces the need for complex VPC peering.<br>
•	Charged per attachment per hour($0.05 – $0.10) + data processing per GB. 💰($0.02 – $0.05 per GB)<br>
•	“Transit Gateway is a regional service. Global connectivity is only possible via inter region peering.”<br>
### Why Use Transit Gateway (TGW) When We Have IGW & NAT?
- 	IGW and NAT are limited in scope<br>
o	IGW: Only allows Internet access for public subnets.<br>
o	NAT Gateway: Allows outbound Internet for private subnets.<br>
o	❌ Neither handles VPC-to-VPC or multi-VPC on-prem connectivity.<br>
- 	Centralized VPC-to-VPC Communication<br>
o	If you have 5–10+ VPCs, connecting them with VPC Peering creates a full-mesh, which is hard to manage.<br>
o	TGW acts as a hub, so all VPCs can communicate through one central router.<br>
- 	Hybrid Cloud / On-Prem Connectivity<br>
o	TGW integrates with VPN or Direct Connect, enabling secure connections between on-prem networks → multiple VPCs.<br>
o	IGW/NAT cannot do this.<br>
- High Scalability & Management<br>
o	With TGW, you can scale to thousands of VPCs and centralize routing.<br>
o	IGW/NAT are per VPC / per subnet, no central routing.<br>
- 	Use Case Example<br>
o	Private VPCs in multiple regions → central NAT in one VPC → TGW allows all private subnets to access Internet securely.<br>
o	On-premises data center → VPN → TGW → multiple VPCs.<br>
<br><br><br><br><br>


# 🌐 7.AWS VPN(regional)
Definition [Paid 💸 ]<br>
•	VPN (Virtual Private Network) = a secure, encrypted connection between:]<br>
o	On-premises network ↔ AWS VPC (Site-to-Site VPN)]<br>
o	Remote user ↔ AWS VPC (Client VPN)]<br>
•	Ensures private, secure access over the Internet.]<br>
•	💰 Charged per VPN connection per hour + data transfer]<br>
•	“VPN itself is regional, because it attaches to regional VPC resources. Global access requires Transit Gateway inter-region peering.<br>
### Types of VPN in AWS

| Type | Description | Use Case | Protocol |
|------|-------------|----------|----------|
| Site-to-Site VPN | Connects on-prem network ↔ VPC | Hybrid cloud, office → AWS connectivity | IPsec |
| Client VPN | Connects individual remote users ↔ VPC | Remote employees accessing private resources | OpenVPN (TLS) |


### Components
1.	Customer Gateway (CGW) – Your on-prem device (router/firewall)<br>
2.	Virtual Private Gateway (VGW) – AWS side of the VPN, attached to VPC)<br>
3.	VPN Tunnel – Encrypted IPsec or TLS tunnel)<br>
4.	Transit Gateway (optional) – Connects multiple VPCs to centralized VPN)<br>
### Real-World Use Cases
1.	Hybrid cloud → on-prem servers access AWS EC2/RDS)<br>
2.	Remote workforce → employees access private VPCs)<br>
3.	Disaster recovery → secure backup to AWS)<br>
4.	Centralized multi-VPC access via TGW)<br>


<br><br><br><br>

# 🌐 6. AWS VPC Endpoints (Regional)

### 📌 Definition (PAID + FREE)
- VPC Endpoint allows you to privately connect your VPC to supported AWS services or VPC endpoint services without using an Internet Gateway (IGW), NAT device, VPN, or firewall.
- Traffic stays within the AWS network, improving security and performance.
- You cannot use the same endpoint across multiple regions.
- Gateway endpoints are free, but Interface endpoints are paid.


### 🔹 Types of VPC Endpoints

| Type | Description | Use Case |
|------|-------------|----------|
| Interface Endpoint | Uses Elastic Network Interfaces (ENIs) with private IPs in your VPC subnets. | Connect to AWS services like EC2 API, S3 (optional), SNS, SQS, or private SaaS services. |
| Gateway Endpoint | Targets S3 or DynamoDB only; configured in route tables. | Private access to S3 buckets or DynamoDB tables without Internet access. |


### 🎯 Use Cases
1. Private S3 Access — EC2 instances in private subnets access S3 without NAT Gateway.
2. Private API Access — Connect to AWS services or partner SaaS securely.
3. Hybrid Cloud — Use interface endpoints to access AWS services privately from on-premises networks.



---

# 🌐 7. AWS Security Group (SG) (Regional)

### 📌 Definition (FREE)
- Security Group = Virtual Firewall for EC2 instances (and other resources like RDS, ELB)
- Controls inbound and outbound traffic at the instance level.
- **Stateful**  
  If you allow inbound traffic, response traffic is automatically allowed even if outbound rules do not explicitly allow it.



### 🎯 Use Cases
1. Web server SG — Allow inbound HTTP/HTTPS (80/443), allow SSH (22) from admin IP only, allow all outbound.
2. Database SG — Allow inbound MySQL/Port 3306 only from app server SG; deny everything else.
3. Multi-tier architecture — Use SG references to control traffic between tiers instead of IPs.



---

# 🌐 8. AWS Network ACL (NACL) (AZ Level)

### 📌 Definition (FREE)
- NACL (Network Access Control List) = Subnet-level firewall in a VPC.
- Controls inbound and outbound traffic for the entire subnet.
- **Stateless**  
  You must explicitly allow return traffic in outbound rules.


### 🎯 Use Cases
1. Extra layer of security on top of Security Groups.
2. Restrict traffic to subnet-wide ranges (e.g., block a malicious IP).
3. Multi-tier architecture → subnet-level traffic control.


### 🔄 Difference Between Security Group & NACL

| Feature | Security Group | NACL |
|--------|---------------|------|
| Level | Instance | Subnet |
| Stateful / Stateless | Stateful | Stateless |
| Allow / Deny | Allow only | Allow & Deny |
| Multiple per instance | Yes | One per subnet |
| Default rule | Deny all inbound/outbound except allowed | Allow all inbound/outbound by default |



---<br><><br><br>

# 🌐 9. AWS VPC Peering (Region / Inter-Region Optional)

### 📌 Definition
- VPC Peering = A private network connection between two VPCs, allowing instances in those VPCs to communicate as if they are in the same network.
- Traffic is private, encrypted on the AWS network, and does not traverse the Internet.



### 🔹 Key Features

| Feature | Description |
|--------|-------------|
| Private connectivity | VPCs communicate via private IP addresses |
| One-to-One Connection | Each peering connection is between exactly two VPCs |
| Region | Can be intra-region or inter-region |
| No bandwidth bottleneck | Uses AWS internal network; high performance |
| No transitive peering | A → B, B → C ≠ A → C (must create explicit peering per pair) |
| Supports IPv4 & IPv6 | Both addressing schemes supported |


### 🎯 Use Cases
1. Multi-VPC architecture — Connect VPCs in same account or different accounts for internal services.
2. Centralized services — One VPC hosts shared services (database, APIs), others access via peering.
3. Inter-region communication — Share data or services across regions.



---<br><><br><br>

# 🌐 10. VPS (Virtual Private Server)

### 📌 Definition
- A VPS is a virtual machine hosted on a physical server, sharing resources with other VPSs but isolated from them.
- Provides dedicated resources like CPU, RAM, storage, and OS for a single user.<br><br>


### ElasƟc Network Interface (ENI)
- A virtual network card that aƩaches to an EC2 instance.
### Each ENI has: 
- Primary private IPv4 address.
- OpƟonal secondary private/public IPs.
- Security Groups. 
- MAC address. 
- ENIs can be moved between instances for high availability. 
- Example: If one EC2 fails, detach ENI → aƩach to backup EC2 → same IP → traffic resumes.






  
















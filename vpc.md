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
-	For production, create a Custom VPC with private<br><br><br>



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
•	Used for: Internet access, peering, VPN, and internal routing.<br>










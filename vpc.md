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

  
## 🧠 Note
-	Only one Default VPC per region
-	All subnets are public
-	Do not delete the Default VPC
-	For production, create a Custom VPC with private



# 1.CIDR Block (IP Range) 
•	A CIDR (Classless Inter-Domain Routing) block defines the IP address range of your VPC.
•	Example: 10.0.0.0/16 → gives you 65,536 IPs. 
•	Each subnet inside the VPC gets a smaller CIDR block. 
•	AWS reserves 5 IPs per subnet (first 4 + last 1). 
•	Use /16 for large VPCs (many subnets)
•	Use /24 for small subnets (common)

## Example Subnet division: 
 VPC CIDR: 10.0.0.0/16 <br>
Public Subnet: 10.0.1.0/24 (256 IPs)<br> 
 Private Subnet: 10.0.2.0/24 (256 IPs) <br>
Rule: You can’t overlap CIDR blocks if you plan to connect VPCs (peering/TGW).







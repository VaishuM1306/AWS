# vpc
-	Amazon VPC lets you create a logically isolated network inside AWS. 
-	You control IP ranges, subnets, routing, firewalls, and connectivity.
-•	It’s like building your own data center inside AWS. 
-•	Every AWS account gets a default VPC, but you can also create custom VPCs for more control.
-•	You can have multiple VPC in ASW region (max 5oer region-soft limit)
-•	Currently, Amazon VPC supports VPCs between /28 (in CIDR notation) and /16 in size for IPv4.
•	The IP address range of your VPC should not overlap with the IP address ranges of your existing network.
•	One can create 200 subnets per VPC.
•	The minimum size of a subnet is a /28 (or 14 IP addresses)
•	There are 2 levels of security within the VPC itself
o	Security Groups which control the flow of traffic at an instance (EC2) level.
o	Network Access Control lists which control the traffic at a subnet level.
•	Amazon VPC Flow logs can be used to monitor traffic within a VPC.
•	A VPC can span multiple Availability Zones by using multiple subnets.


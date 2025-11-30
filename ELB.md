# AWS ELB (Elastic Load Balancing)

### Scalability
Scalability means the ability to grow yoursystem's resources when your application or website gets more traffic or more users.

- a>Vertical Scalability (Scaling Up)<br>
Vertical Scalability means adding more power (CPU, RAM) to your existing server.<br>
Ex: t2.micro to m5.large


- b>Horizontal Scalability (Scaling Out)<br>
Horizontal Scalability means adding more instances (servers) to distribute the load.<br>
You can add more EC2 instances behind a load balancer<br>



### High Availability (HA)<br>
High Availability (HA) means keeping your service up and running with minimal downtime,so it's always accessible to users.<br>
Ex: running resources in multiple AZs<br>


### Elasticity<br>
Elasticity means the ability to automatically adjust resources as the demand changes—,adding more when needed and removing when it’s no longer necessary.<br>
Ex: ASG<br><br><br><br><br>


### Elastic Load Balancer Points<br>
- Distributes Traffic: It splits incoming traffic across multiple servers so no single server gets overloaded.<br>
- Improves Availability: If one server goes down, the load balancer automatically sends traffic to the working servers, ensuring your application stays available.<br>
- Scales Resources: It helps manage high demand by adding more servers during<br>
- peak times and distributing the load.<br>
- Single point of Access need to be expose.<br>
- HA across AZs<br>


# Auto Scaling Group (ASG)<br>
- AWS ASG (Auto Scaling Group) is a service that automatically adds or removes EC2 instances based on demand to ensure your application is always available.<br> 
- It helps scale up when more capacity is needed and scale down during low usage to save costs, keeping the right number of servers running at all times.<br>



# Functions<br>
- Automatic Scaling: Scale the number of EC2 instances up or down based on demand.<br>
- Maintain Instance Health: Replace unhealthy instances automatically to ensure reliability.<br>
- Use Scaling Policies: Set rules for scaling based on metrics like CPU usage or request count.<br>
- Ensure Availability: Always keep a defined number of instances running to meet application needs.<br>
- Schedule Scaling: Pre-configure scaling activities for specific times<br>
- (e.g., traffic peaks).<br><br><br>


**Distribute Instances**: Deploy instances across multiple Availability Zones for high availability.
Integrate with ELB: Attach instances to an Elastic Load Balancer to automatically balance traffic.
Optimize Costs: Scale down during low demand to save on infrastructure costs.









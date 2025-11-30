
 
 # AMI (Amazon Machine Image)
An Amazon Machine Image (AMI) is a pre-configured template that provides the necessary information to launch an EC2 instance in AWS.
With an AMI, you can launch new EC2 instances with a consistent, predefined configuration.

You can also create custom AMIs to include specific software or settings, allowing for quick replication of environments.




** It includes: **
Operating system (e.g., Linux, Windows)<br>

Application server (e.g., Apache, Nginx)<br>

Pre-installed software and configurations<br>


** Types of AWS AMIs **

Public AMIs: Available to all AWS users. Useful for basic use cases like popular operating systems (e.g., Ubuntu, CentOS).<br>

Private AMIs: Created by a user and only available within that account or shared with specific accounts.<br>

Paid AMIs/Marketplace AMIs: Provided by third parties through AWS Marketplace, offering software like databases, web servers, or pre-configured environments.<br><br><br>



### ** Common use cases for each type: **
Public: Testing or development environments.<br>

Private: Customized setups for production.<br>

Marketplace: Deploying pre-built solutions (e.g., enterprise software).<br>


### Run Cleanup Script
#!/bin/bash

- Remove SSH keys---- rm -rf ~/.ssh/authorized_keys

- Clear user credentials and history

rm -rf ~/.aws/credentials

rm -rf ~/.git-credentials

rm -rf ~/.bash_history

- Clean system logs and temporary files
rm -rf /var/log/*

rm -rf /tmp/*

rm -rf /var/tmp/*

- Remove user accounts
deluser tempuser --remove-home

Lock root account
passwd -l root

- Reset configuration files (example for Nginx)
rm -rf /etc/nginx/nginx.con

- Key Differences<br>
Feature	Create Launch Template	Create Image (AMI)<br>
Purpose	Create a reusable blueprint for launching instances	Create a custom AMI snapshot of an instance<br>
Content	Contains configuration settings (e.g., AMI, instance type, security groups, etc.)	Captures OS, applications, configurations, and data<br>
Reusability	Used repeatedly to launch new instances in a consistent way	Used to create new instances that replicate the captured image<br>
Use Cases	Auto Scaling, Spot Instances, Standardizing instance settings	Backup, Replication, Migrating instances to another region<br>
Versioning	Can have multiple versions for different configurations	Typically,<br><br><br>


### What AWS Image Builder Does
- Automates image creation pipelines
- Applies updates and security patches
- Runs tests on images
- Outputs AMIs, Docker images, and more
- Ensures consistent and compliant golden images
- Automate VM or Image Creation
- creation, testing, and deployment of AMIs
- Can be configured to run at regular intervals (e.g., daily, weekly, or monthly)
Free

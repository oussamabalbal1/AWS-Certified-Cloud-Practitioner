# AWS-Certified-Cloud-Practitioner
In this repository, I just write some things that I usually forget about AWS CCP Certificate to make it easier for me to review it later.



### How to choose an AWS Region?
- Compliance
- Proximity
- Available services
- Pricing

### The Five Characteristics of Cloud Computing
- On-demand self service:Users can provision resources and use them without human interaction from the service provider
- Broad network access:Resources available over the network, and can be accessed by diverse client platforms
- Multi-tenancy and resource pooling:
	- Multiple customers can share the same infrastructure and applications with security and privacy
	- Multiple customers are serviced from the same physical resources
- Rapid elasticity and scalability:
	- Automatically and quickly acquire and dispose resources when needed
	- Quickly and easily scale based on demand
- Measured service:
	- Usage is measured, users pay correctly for what they have used

## Six Advantages of Cloud Computing
- Trade capital expense (CAPEX) for operational expense (OPEX)
	- Pay On-Demand: don’t own hardware
	- Reduced Total Cost of Ownership (TCO) & Operational Expense (OPEX)
- Benefit from massive economies of scale
	- Prices are reduced as AWS is more efficient due to large scale
- Stop guessing capacity
	- Scale based on actual measured usage
- Increase speed and agility
- Stop spending money running and maintaining data centers
- Go global in minutes: 
	- leverage the AWS global infrastructure

# IAM : Identity and Access Management
- Users or Groups can be assigned JSON documents called policies
- These policies define the permissions of the users
- IAM Policies Structure: Version-ID-SID-Effect
- MFA:Multi Factor Authentication
- Access Keys:Access Key ID/Secret Access Key
- IAM Security Tools
	- IAM Credentials Report (account-level): 
		- lists all your account's users and the status of their various credentials
	- IAM Access Advisor (user-level) :
		- shows the service permissions granted to a user and when those services were last accessed

# EC2 : Elastic Compute Cloud
- EC2 User Data:
	- It is possible to bootstrap our instances using an EC2 User data script
- EC2 Instance Types:m5.2xlarge
	- m: instance class/5: generation/2xlarge: size

- Security groups only contain ALLOWS rules : acting as a “firewall” on EC2 instances	
	- rules can reference by IP or by security group
	- All inbound traffic is blocked by default
	- All outbound traffic is authorised by default
- EC2 Instance Connect: Connect to your EC2 instance within your browser

- Purchasing Options: On-Demand, Spot, Reserved (Standard + Convertible + Scheduled), Dedicated Host, Dedicated Instance

# EBS : Elastic Block Store (size in GBs, and IOPS)
- Volume is a network drive you can attach to your instances while they run(bound to a specific availability zone)
- It allows your instances to persist data, even after their termination
- EBS Snapshots : Make a backup of your EBS volume
	- Not necessary to detach volume to do snapshot, but recommended
	- Can copy across AZ or Region
- EBS Snapshots Features :
	- __EBS Snapshot Archive__ : 75% cheaper / 24 to 72 hours for restoring
	- __Recycle Bin for EBS Snapshots__ : Setup rules to retain deleted snapshots so you can recover them after an accidental deletion
## AMI : Amazon Machine Image
Customization of an EC2 instance, Built for a specific region (and can be copied across regions)
- You add your own software, configuration, operating system, monitoring…
- Faster boot / configuration time because all your software is pre-packaged
- You can launch EC2 instances from
	- A Public AMI
	- An AWS Marketplace AMI
	- Your own AMI
	![01](https://user-images.githubusercontent.com/46396011/226205226-513fc14f-2a04-4d12-9cec-aca5db7ea6ed.PNG)


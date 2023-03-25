# AWS-Certified-Cloud-Practitioner
In this repository, I just write some things that I usually forget about AWS CCP Certificate to make it easier for me to review it later.

##### Table of Contents  
- [IAM](#iam--identity-and-access-management)
- [EC2](#ec2--elastic-compute-cloud)
- [EBS](#ebs--elastic-block-store-size-in-gbs-and-iops)



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

## EC2 Image Builder
- Used to automate the creation of Virtual Machines or container images
- Automate the creation, maintain, validate and test EC2 AMIs
- Can be run on a schedule

![01](https://user-images.githubusercontent.com/46396011/226205359-c289b19d-5347-48ef-b695-6d6534e8a7d0.PNG)

## EC2 Instance Store
- EBS volumes are network drives with good but “limited” performance
- __If you need a high-performance hardware disk__, use EC2 Instance Store
- Better I/O performance
- EC2 Instance Store lose their storage if they’re stopped

## EFS – Elastic File System
- Managed NFS (network file system) that can be mounted on 100s of EC2
- EFS works with Linux EC2 instances in multi-AZ
- Highly available, scalable, expensive, pay per use, no capacity planning


![02](https://user-images.githubusercontent.com/46396011/226205550-80ff75a0-98b0-475f-adc2-e32cd821a026.PNG)
- ### EFS Infrequent Access (EFS-IA)
	- Storage class that is cost-optimized for files not accessed every day
	- Up to 92% lower cost compared to EFS Standard
	- EFS will automatically move your files to EFS-IA based on the last time they were accessed
	- Enable EFS-IA with a Lifecycle Policy : EXP: move files that are not accessed for 60 days to EFS-IA
	
	
	![03](https://user-images.githubusercontent.com/46396011/226205750-212a75c9-72d4-4f60-a105-2fbac1d45570.PNG)
	
- ### Amazon FSx
	- Launch 3rd party high-performance file systems on AWS
	- Fully managed service
	- #### Amazon FSx for Windows File Server
		- A fully managed, highly reliable, and scalable Windows native shared file system 
		- Supports SMB protocol & Windows NTFS
		- Integrated with Microsoft Active Directory
		- Can be accessed from AWS or your on-premise infrastructure
		
		![04](https://user-images.githubusercontent.com/46396011/226208511-543ffcd1-e8d7-40c6-93d4-b1b20d649ebe.PNG)

	- #### Amazon FSx for Lustre
		- Lustre (Linux+Cluster)
		- A fully managed, high-performance, scalable file storage for __High Performance Computing (HPC)__
		- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
		
		![01](https://user-images.githubusercontent.com/46396011/226208620-0fd0b592-c188-4a04-8580-cfdaac5ca103.PNG)
		
		
# ELB & ASG : Elastic Load Balancing & Auto Scaling Groups Section
- Some tearms :
	- _Scalability:_ ability to accommodate a larger load by making the hardware stronger (scale up), or by adding nodes (scale out)
	- _Elasticity:_ once a system is scalable, elasticity means that there will be some “auto-scaling” so that the system can scale based on the load. This is “cloud-friendly”: pay-per-use, match demand, optimize costs
	- _Agility:_ (not related to scalability - distractor) new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes.
- What is load balancing:
	- Load balancers are servers that forward internet traffic to multiple servers (EC2 Instances) downstream
- Why use a load balancer?
	- Spread load across multiple downstream instances
	- Expose a single point of access (DNS) to your application
	- Provide SSL termination (HTTPS) for your websites
	- High availability across zones
	- Do regular health checks to your instances and handle failures of downstream instances

## ELB (Elastic Load Balancer)
- An ELB (Elastic Load Balancer) is a managed load balancer
- 4 kinds of load balancers offered by AWS
	1. Application Load Balancer (HTTP / HTTPS only) – Layer 7
	2. Network Load Balancer (ultra-high performance, allows for TCP) – Layer 4
	3. Gateway Load Balancer – Layer 3
	4. Classic Load Balancer (retired in 2023) – Layer 4 & 7

![sd01](https://user-images.githubusercontent.com/46396011/226339047-71898d01-452a-4f3e-a009-503df275f493.PNG)


## ASG (Auto Scaling Group)
- The goal of ASG : 
	- Scale out (add EC2 instances) to match an increased load
	- Scale in (remove EC2 instances) to match a decreased load
	- Ensure we have a minimum and a maximum number of machines running
	- Automatically register new instances to a load balancer
	- Replace unhealthy instances
- Scaling Strategies : 
	- __Manual Scaling__ : Update the size of an ASG manually
	- __Dynamic Scaling__ : Respond to changing demand
		- _Simple / Step Scaling_
			- When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 units
			- When a CloudWatch alarm is triggered (example CPU < 30%), then remove 1
		- _Target Tracking Scaling_
			- Example: I want the average ASG CPU to stay at around 40%
		- _Scheduled Scaling_
			- Example: increase the min. capacity to 10 at 5 pm on Fridays
	- __Predictive Scaling__ : Uses Machine Learning to predict future traffic ahead of time




# S3 : Simple Storage Service 
- Use cases :
	- Backup, storage, Disaster Recovery, Archive..
- S3 Buckets (region level )
	- Amazon S3 allows people to store objects (files) in “buckets” (directories)
	- Buckets must have a globally unique name (across all regions all accounts)
- S3 - Objects
	- Objects (files) have a Key
	- The key is the FULL path
	- The key is composed of prefix + object name
	- __Contents__
		- VALUE : Max. Object Size is 5TB (5000GB)
		- Metadata
		- Tags
		- Version ID (IF enabled)
- #### S3 – Security
	- __User-Based__ : IAM Policies
	- __Resource-Based__
		- _Bucket Policies_ : bucket wide rules from the S3 console - allows cross account
		- _Object Access Control List (ACL)_
		- _Bucket Access Control List (ACL)_
	- __Encryption__ 
	- _Note:_ an IAM principal can access an S3 object if :
		- The user IAM permissions ALLOW it OR the resource policy ALLOWS it
		- AND there’s no explicit DENY
- S3 Bucket Policies 
	- JSON based policies
	- Use S3 bucket for policy to
		- Grant public access to the bucket or (Cross Account)
		- Force objects to be encrypted at upload
- Bucket settings for Block Public Access (account level)
	- These settings were created to prevent company data leaks
	- If you know your bucket should never be public, leave these on


	![001](https://user-images.githubusercontent.com/46396011/226212909-14b476b2-928b-4153-aef7-92d28373ab4e.PNG)
- S3 Static Website Hosting
	- S3 can host static websites and have them accessible on the Internet
- S3 Versioning
	- You can version your files in Amazon S3 ( __bucket level__ )
- S3 Replication (__CRR & SRR__)
	- __Must enable Versioning__ in source and destination buckets
	- __Cross-Region Replication__ (CRR) : compliance, lower latency access..
	- __Same-Region Replication__ (SRR) : – log aggregation..
	- Copying is asynchronous
	- Buckets can be in different AWS accounts
- ### S3 Storage Classes



# Security & Compliance Section

## AWS Shield
- AWS Shield Standard (Free service) 
	Provides protection from attacks such as SYN/UDP Floods, Reflection attacks and other layer 3/layer 4 attacks
- AWS Shield Advanced
	- Optional DDoS mitigation service ($3,000 per month per organization) 
	- Optional DDoS mitigation service
	- 24/7 access to AWS DDoS response team (DRP)
## AWS WAF – Web Application Firewall
- Protects your web applications from common web exploits (Layer 7)
- Deploy on Application Load Balancer, API Gateway, CloudFront
- Define Web ACL (Web Access Control List):
	- Rules can include IP addresses
	- Protects from common attack - SQL injection and Cross-Site Scripting (XSS)

## AWS KMS (Key Management Service)
AWS manages the encryption keys for us

## CloudHSM (Dedicated Hardware)
AWS provisions encryption hardware

## AWS Certificate Manager (ACM)
- Let’s you easily provision, manage, and deploy SSL/TLS Certificates
- Integrations with (load TLS certificates on) :
	- Elastic Load Balancers
	- CloudFront Distributions
	- APIs on API Gateway

## AWS Secrets Manager
- Newer service, meant for storing secrets
- Capability to force rotation of secrets every X days
- Integration with Amazon RDS 
- Secrets are encrypted using KMS

## AWS Artifact (not really a service)
- Portal that provides customers with on-demand access to AWS compliance documentation and AWS agreements
- Can be used to support internal audit or compliance

## Amazon GuardDuty	
- ntelligent Threat discovery to protect your AWS Account
- Uses Machine Learning algorithms
- Input data
	- CloudTrail Events Logs
	- VPC Flow Logs
	- DNS Logs
	- Kubernetes Audit Logs
- Can setup EventBridge rules to be notified in case of findings
- Can protect against CryptoCurrency attacks

## Amazon Inspector
- Automated Security Assessments
- Reporting & integration with AWS Security Hub
- Send findings to Amazon Event Bridge
- for EC2 instances, Container Images & Lambda functions




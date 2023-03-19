# AWS-Certified-Cloud-Practitioner
In this repository, I just write some things that I usually forget about AWS CCP Certificate to make it easier for me to review it later.

- [IAM](#S3 : Simple Storage Service)
- [S3 : Simple Storage Service](#usage)
- [Contributing](#contributing)
- [License](#license)


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





# Doe's awsGuide

### 이 repository 는 :

AWS 전반의 공부를 기록으로 남기고자 만들었습니다.\
AWS Certified Solutions Architect 시험을 위해 만들었습니다.

### Studied from :

[AWS Certified Solutions Architect - Associate 2020](https://www.youtube.com/watch?v=Ia-UEYYR44s&t=299s)

[Linux Academy AWS Essentials](https://www.youtube.com/watch?v=BDBvHOaaKHo&list=PLv2a_5pNAko0Mijc6mnv04xeOut443Wnk)

* ## [시험](https://aws.amazon.com/ko/certification/certified-solutions-architect-associate/)
  * ### [내용 (2021년 기준. Outdated 할 수 있으니 위 주소에서 확인 바랍니다.)](https://d1.awsstatic.com/ko_KR/training-and-certification/docs-sa-assoc/AWS-Certified-Solutions-Architect-Associate_Exam-Guide.pdf)
    * 탄력적 아키텍처 설계 30%
    * 고성능 아키텍처 설계 28%
    * 안전한 애플리케이션 및 아키텍처 설계 24%
    * 비용-최적화된 아키텍처 설계 18%
  * ### 문제
    * 단일 선택
    * 다중 선택
  * ### 합격
    * 720/1000 (2021년 기준. 이수자의 %에 따라 다를 수 있습니다.)

* ## S3 (Simple Storage Service)
  * ### Object based storage service
    * data as objects 
    * opposed to other storage architectures such as
      * file systems
      * block storage
  * ### Serverless storage in cloud
  * ### Unlimited storage
  * ### No worries for infrastructure
  * ### Upload Success returns HTTP 200
  * ### S3 Object
    * Like files
    * 0 Bytes ~ 5 Terabytes
    * Contains data
      * Owner
      * Last Modified
      * Key : Name of object
      * Value : data sequence of bytes
      * Version ID : Version of the object when enabled
      * Metadata : Additional information
  * ### S3 Bucket
    * Hold Objects and Folders
    * Universal namespace (Names need to be unique)
  * ### Storage Class
    * Standard (default)
      * Fast
      * 99.99% Availability
      * 11 9's Durability
      * Replicated at least three Availability Zone (AZ)
    * Intelligent Tiering
      * Uses ML
      * Data is moved to most cost effective tier
      * No performance impact or overhead
    * Standard Infrequently Accessed (IA)
      * Still Fast
      * 50% Cheaper than Standard
      * Reduced Availability
        * Access files once a month
        * Additional retrieval fee if accessed more
    * One Zone IA
      * Still Fast
      * 20% Cheaper than Standard IA
      * Reduced Availability 99.5%
        * Retrieval fee
      * Reduced Durability (Data could get destroyed)
    * Glacier
      * Long term cold storage
      * Very Cheap
      * Minutes to Hours for Retrieval
    * Glacier Deep Archive
      * Lowest Cost
      * 12 Hours for Retrieval
  * ### Security
    * All new buckets are PRIVATE by default
    * Logging per request can be turned on a bucket
      * Logs are generated and saved in a different bucket
      * Different account logging is possible
    * Access Control
      * Access Control Lists (ACL)
        * Legacy feature (Not Deprecated)
        * Simple
      * Bucket Policies
        * JSON
        * AWS Policy Generator
  * ### Encryption
    * Transit
      * Local Host <-> S3 achieved via SSL/TLS
    * Server Side Encryption (SSE) (Encryption At Rest)
      * S3 Managed Keys (Amazon Manages all Keys)
        * SSE-AES (AES-256 algorithm)
        * SSE-KMS (AWS Key Management System and YOU manage keys)
        * SSE-C (Customer Provided key, AWS and YOU manage keys)
    * Client Side Encryption (CSE)
      * You Encrypt files before upload
    * Existing files before Encryption on is not Encrypted
  * ### Data Consistency
    * New Object (PUT)
      * Read After Write Consistency
      * Able to read immediately after writing
    * Overwrite (PUT) or Delete (DELETE)
      * Eventual Consistency
      * Overwrite or delete takes time to replicate versions to AZs
      * Reading immediately may return old copy
      * Wait before reading
  * ### Cross Region Replication (CRR)
    * Automatic replication to other regions
    * Higher durability
    * Disaster recovery
    * Versioning must be on both source and destination
    * Can CRR to other accounts
  * ### Versioning
    * Once enabled, cannot be disabled. Can be suspended
    * Full Integration with S3 Lifecycle rules
    * Delete request will delete only the latest version
    * Previous version becomes latest if latest version is deleted
    * Version ID can be NULL if created before Versioning on
    * Properties like public is not inherited between versions
  * ### Lifecycle Management
    * Automate moving storage class(Tier), or delete
    * Can be used with Versioning
    * Can be applied to current or previous versions
    * Per-request fee
    * Minimum wait duration is 30 days
  * ### Transfer Acceleration
    * Uses CloudFront Edge Locations
    * User uploads to distinct URL from edge Location
    * Edge Location data is routed to S3 by AWS backbone network.
  * ### Presigned URLs
    * Generated URL
    * Temporary access to Object for Upload or Download
    * Access to Private Objects
    * Created by AWS CLI/SDK
    * Expire date
  * ### MFA Delete
    * Must provide MFA token/code to delete
    * Enable Conditions
      * By AWS CLI
      * Versioning on
    * Only Root User can delete
  * ### AWS CLI
    * ls
      * aws s3 ls : return all buckets
      * aws s3 ls s3://bucketName : return bucket objects
      * aws s3 ls s3://bucketName/folderName : return directory objects
    * cp
      * aws s3 cp s3://bucketName/folderName/objectName.jpg ~/Desktop/a.jpg : download object to a.jpg
      * aws s3 cp ~/Desktop/a.jpg s3://bucketName/folderName/objectName.jpg : upload a.jpg to object
    * presign
      * aws s3 presign s3://bucketName/folderName/objectName.jpg --expires-in 300 : creates a presigned url

* ## Snowball
  * ### Petabyte date transfer service (Use multiple snowballs)
  * ### AWS data to physical computer
    * Import and export
  * ### Low cost
    * Costs thousands of dollars to transfer 100 TB in high speed internet
    * Reduce cost by 1/5th
  * ### Speed
    * Takes 100 days to download 100 TB over high speed internet
    * Reduce time by less than a week
  * ### Features
    * E-link display (Shipping information)
    * Tamper/Weather proof
    * Data encrypted (256-bit encryption)
    * Trusted Platform Module(TPM)
      * Chip that stores RSA encryption keys for hardware authentication
      * Specific to the host system
    * Data transfers must be completed in 90 days
    * Can import and Export S3
  * ### Size
      * 50 TB (42 TB usable)
      * 80 TB (72 TB usable)
      
* ## Snowball Edge
  * ### Similar to snowball
  * ### More storage
  * ### Local processing
  * ### Petabyte data transfer service
  * ### Features
    * LCD Display (Shipping information / functionality)
    * Local processing
    * Edge-computing workloads
    * Can use in a cluster of 5 ~ 10 devices
  * ### Optimization Options
    * Storage optimized (24 vCPUs)
    * Compute optimized (54 vCPUs)
    * GPU optimized (54 vCPUs)
  * Size
    * 100 TB (83 of usable)
    * 100 TB Clustered (45 TB per node)
  
  
* ## Snowmobile
  * ### 45 foot long shipping container
  * ### Pulled by semi-trailer truck
  * ### Exabyte data transfer service
  * ### 100 PB per Snowmobile
  * AWS personnel will help connect, and when data transfer is complete, they'll drive it back to AWS and import to S3
  * ### Security
    * GPS tracking
    * Alarm monitoring
    * 24/7 video surveillance
    * Escort security vehicle while transit (Optional)
    
  
* ## Virtual Private Cloud (VPC)
  * ![](images/vpc.PNG?raw=true "")
  * ### Key Features
    * Region Specific
    * Do not span regions
    * Every region has default VPC
    * 200 subnets per VPC
    * Uses IPv4 ClDR Block
    * Can add IPv6 ClDR Block
    * DNS hostnames (VPC option)
      * Domain Name System (DNS)
      * Uniquely names a computer
      * DNS server connects hostnames to IP address
      * Off by default
      * EC2 DNS
        * ![](images/DNS_hostname_ec2.PNG)
    
  * ### Default VPC
    * Default VPC in every region
    * Can immediately deploy ec2
    * Features
      * Size /16 IPv4 [CIDR](https://www.youtube.com/watch?v=z07HTSzzp3o) (ex: 172.31.0.0/16)
      * Creates Size /20 default subnet in every AZ
      * Creates Internet Gateway
      * Creates default security group
      * Creates default network access control list (NACL)
      * Associate to default [DHCP](https://www.youtube.com/watch?v=e6-TaH5bkjo)
      * VPC creation automatically has route table
      
  * ### 0.0.0.0/0
    * All possible IP addresses
    * [Internet Gateway](https://www.youtube.com/watch?v=pAOrBxZ7584) (IGW)
      * Allow All Internet Access
    * Security Groups Inbound Rules
      * Allow All traffic from Internet
    
  * ### Components
    
    * #### Internet Gateway (IGW)
      * Allows VPC access to the Internet
      * Provide a target in VPC route tables
      * Performs network address translation ([NAT](https://www.youtube.com/watch?v=FTUV0t6JaDA))
        * Only Addresses with public IPv4
      * To connect to the Internet
        * Add route table
        * Route that table to Internet Gateway
        * Set destination to 0.0.0.0/0
      
    * #### Virtual Private Gateway (VPN Gateway)
      
    * #### [Route Table](https://www.youtube.com/watch?v=GrfOsWUVCfg)
      * Determines where network traffic is directed
      * Each Subnet must have a route table
      * One(Route Table) to Many(Subnet)
      * Can have multiple route tables in a VPC
      
    * #### Bastion / Jumpbox
      * ![](images/bastion.PNG)
      * EC2 instances for security
      * Help gain access to EC2 in private Subnet
      * Via SSH or RCP
      * NAT Gateways should not be used as Bastions
      * NAT Gateways intentions is for security updates
      * Systems Manager's Session Manager can replace Bastion
      
    * #### Security Groups (SG) Stateful
      * Firewall for EC2 instance
      * Associated with EC2 instances
      * Protocol / Port security
      * Allows IP range / Specific IP / Security group
      * Inbound and Outbound rules
        * Statefull (Inbound allowed is also Outbound allowed)
        * All inbound traffic blocked by default
        * All outbound traffic allowed by default  
      * No Defy rules, only access rules
      * Many(Security Group) to Many(EC2(Multiple Subnets possible))
      * Rules are permissive (Permit overrides deny)
      * Limits
        * Upto 10,000 (default 2,500) SG per Region
        * 60 inbound rules and 60 outbound rules per SG
        * Upto 16 (default 5) SG per Elastic Network Interface (ENI)
      
    * #### Public Subnets
      
    * #### Private Subnets
      
    * #### Network Address Translation (NAT) Gateway
      * Remapping one IP address to another
      * Help gain outbound internet access for private subnet
      * Remap private IP
      * Solve same IP addresses (Conflicting network address)
      * Redundant inside an AZ (AWS manages it/ no EC2 fails)
      * 1 NAT Gateway per AZ (Cannot span AZ)
      * Starts at 5 Gbps and scales up to 45 Gbps
      * Perferred than NAT Instance
      * Automatically assigned a public IP
      * Route Tables for the NAT Gateway must be updated
      
    * #### Customer Gateway
      
    * #### [VPC Endpoints](https://www.youtube.com/watch?v=MPaxxOsjOos)
      * Private connect VPC to other AWS services
      * No need for Internet Gateway / NAT / VPN / AWS direct connect
      * Instance do not require public IP
      * Traffic does not leave the AWS network
      * Secure communication
      * Fast / No bandwidth constraints
      * Types
        * Interface Endpoints
          * In private subnet
          * Uses Elastic Network Interfaces
          * Private IP address
          * Powered by AWS PrivateLink
          * Supports many AWS services  
          * Costs Money
        * Gateway Endpoints
          * Connect From Route table
          * Supports only two services
            * S3
            * Dynamo DB
          * Free
      
    * #### VPC Peering
      * Connecting VPC with VPC
      * Direct network route
      * Connection by private IP address
      * Peered VPC behave like they are on the same network
      * Can peer different AWS account VPC
      * Can peer different region VPC
      * No Transitive Peering
        * One(VPC) to One(VPC) 
        * Peering must be direct
        * Signal Traffic must be direct
      * Peering uses Star Configuration
        * ![](images/vpc_star_configuration.PNG)
        * 1 Central VPC
        * 4 Other VPC
      * No Overlapping CIDR Blocks
    
    * #### VPC Flow Logs
      * Log in CloudWatch Logs or S3   
      * Caputre IP traffic information
      * Within Network Interface in VPC
      * Cannot be tagged like other AWS resources
      * Cannot Change configuration after creation 
      * Cannot enable peered VPC flow logs unless in same account  
      * Monitor Levels  
        * VPC
        * Subnets
        * Network Interface
      * Log
        * version
        * account-id
        * interface-id (ID of network interface)
        * srcaddr (Source IPv4 or IPv6)
        * dstaddr (Destination IPv4 or IPv6)
        * srcport (Source port of traffic)
        * dstport (Destination port of traffic)
      * Not Logged
        * Traffic to AWS DNS Servers
        * Windows license activation traffic for instances
        * Instance metadata address traffic
        * DHCP traffic
        * Any traffic to reserved IP address of default VPC router
      
    * #### [Direct Connect](https://www.youtube.com/watch?v=jEcl5H8Ow_8)
      * Establish a dedicated network from Office to AWS
      * Very fast network
      * Private connectivity
      * Lower Bandwidth 50 M ~ 500 M
      * Higher Bandwidth 1 GB ~ 10 GB
      * Help reduce network cost for high traffic
      * More consistent network than internet
    
    * #### [Network Access Control List (NACL)](https://www.youtube.com/watch?v=vJzHn24TNQE)
      * Firewall subnet traffic
      * An optional layer of security
      * VPC is automatically given default NACL
        * Default NACL will deny all traffic
      * Subnets must have a NACL  
      * One(NACL) to Many(Subnets)
      * Allow or defy traffic (Security groups only allow)
      * Inbound or outbound rules (Like security groups)
      * Can block a single IP (Security groups can't) 
      * Order of evaluation Rule number #
        * Lower is higher priority
        * 10 to 100 increments recommended
      * Example
        * Malicious hacker IP block
        * SSH block
  
      

* ## Identity Access Management (IAM)
  
  * ### Manage access of AWS users and resources
  * ### Universal system (All AZ)
  * ### Free service
  * ### IAM Identities
    * #### IAM Users
      * End users using aws sdk or cli
    * #### IAM Groups
      * Group IAM Users
      * Shared permissions
      * Example : Administrators/Developers/Auditors
    * #### IAM Roles
      * Associate permissions to a Role
      * Give Roles to Users or Groups 
      * Roles can also be attached to AWS Resources
    
  * ### IAM Policies
    * #### JSON
      * Version (ex: 2012-10-17)
      * Statement (Container for multiple policy elements)
      * Sid (Optional, ways to name statements)
      * Effect (Allow/Deny)
      * Principal (Account/user/role/fedrated user)
      * Action (List of actions policy allows or denies)
      * Resource (Resource where action applies)
      * Conditional (Optional,circumstances when policy applies)
      * ![](images/IAM_policies_json.PNG)
    * Grants permission to Identities
    * Policies are attached to User/Group/Roles
    * Types
      * #### Managed Policies
        * Policy managed by AWS
        * Cannot be edited
        * Labeled with orange box
      * #### Customer Managed Policies
        * A policy created by a customer
        * Can be edited
        * No symbol
      * #### Inline Policies
        * Directly attached to user / resource
      * #### Password Policy
        * Rotate passwords to update after X days
        * Set minimum requirements
    
  * ### Access keys
    * Allow users use CLI/SDK
    * Cannot access console 
    * Two Access keys per user
    * Can make active/inactive
    * Only shown once, if lost delete, recreate
  
  * ### Multi Factor authentication (MFA)
    * Can be turned on per user
    * User can turn on themselves
    * Admin can not enforce MFA
    * Admin can create policy requiring MFA for resources
    * Should set MFA for Root 
    * Type
      * #### Virtual MFA device
      * #### U2F security key
      * #### Other hardware MFA device
  


* ### Amazon Cognito
  
  * #### Web Identity Federation
    * To exchange identity and security information between IdP and application
    
  * #### Identity Provider (IdP)  
    * Trusted provider for authentication (Facebook, Google ...)
    
  * #### Types of IdP
    * Security Assertion Markup Language (SAML) (Single Sign On SSO)
    * OpenID Connect (OIDC) (OAuth)
    
  * #### Types  
    
    * ##### Cognito User Pools
      * User directory with authentication to IpD to grant app access
      * User Pools
        * Directories to manage the actions such as
          * Sign in
          * Sign up
          * Account recovery
          * Account confirmation
      * Sign by User Pool or IdP
      * Uses JWT to persist authentication
      * Settings
        * Allow sign in with email/phone/username
        * Choose signup requirements
        * Choose password requirements
        * Apply MFA
        * Trigger custom logs, Lambdas
    
    * ##### Cognito Identity Pools
      * Temporary credentials for users to access AWS Services
      
    * ##### Cognito Sync
      * One line of code
      * Syncs user data and preferences across devices
      * Push synchronization to push updates and sync data
      * Uses Simple Notification services (SNS)
      * Sends Identity pools to sync data
  
  
* ### AWS Command Line Interface (CLI)
  * #### Interact with AWS via command line
  * #### Important CLI flags
    * --profile : switch between AWS accounts
    * --output : changes output between json, table and text
  * #### AWS User must have Programmatic Access
    * Access Key ID, Secret Access Key (AWS Credentials)
    * Store credentials in user home (~/.aws/credentials)
    * Multiple credentials can be managed by profiles   
      [ProfileName]   
      aws_access_key_id=   
      aws_secret_access_key=
    * ![](images/CLI_credentials_profile.PNG)
  
* ### AWS Software Development Kit (SDK)
  * #### Set of tools and libraries to use AWS in apps for specific language
  * #### AWS User must have Programmatic Access
    * Access Key ID, Secret Access Key (AWS Credentials)
    * Store credentials in user home (~/.aws/credentials)  
    * Multiple credentials can be managed by profiles
    

* ### Domain Name System (DNS)
  * #### Changes Domain name (google.com) -> IP address (142.250.196.132)
  * #### Internet Protocol (IP)
    * Uniquely identifies each computer for communication
    * Internet Protocol Version 4 (IPv4)
      * Address space is 32 Bits
      * Currently running out of space
    * Internet Protocol Version 6 (IPv6)
      * Address space is 128 Bits
  * #### Domain Levels
    * ##### Top Level Domain
      * Last word within a domain name (.com)
      * Controlled by Internet Assigned Numbers Authority (IANA)
    * ##### Second Level Domain
      * Second word within a domain name (.co.kr : .co)
  * #### Start of Authority (SOA)
    * Every Domain must have an SOA record
    * Information about the domain
    * Structure
      * NAME : name of zone
      * IN : zone class
      * SOA : start of authority
      * NNAME : master name server of zone
      * RNAME : admin email of zone
      * SERIAL : serial number for zone
      * REFRESH : ...
      * RETRY : ...
      * EXPIRE : ...
      * TTL : ...
  * #### Address Records (A Records)
    * Convert Domain name -> IP
  * #### Canonical Names (CNAME)
    * Convert Domain name -> Domain name
  * #### Name Server Records (NS Records)
    * Direct traffic to the DNS server containing DNS records
    * Multiple name servers are provided for redundancy
  * #### Time To Live (TTL)
    * Time that a DNS record gets cached
    * Time it takes to propagate across the internet
    * Measured in seconds under IPv4
  
* ### Route53
  * #### Domain name provider in AWS
  * #### Functionality
    * ##### Register Domain
    * ##### Create Records sets on a domain
    * ##### Implement complex traffic flow (Blue/Green, Deploy, Failovers)
    * ##### Monitor records via heath checks
    * ##### Resolve VPC outside AWS
    
  * #### Traffic flow
    * Visual editor for routing config
    * Supports versioning
    * 50$ per policy record / month
    
  * #### Record Set
    * ##### www. , api. , blog. to A, AAAA, CNAME...
    * Alias
      * Always should use Alias because resources changes IP
      * Route traffic to specific AWS Resources
        * CloudFront
        * Elastic Beanstalk
        * ELB load balancer
        * S3 website endpoint
        * Resource record set
        * VPC endpoint
        * API Gateway
  * #### Routing Policy
    * ##### Simple Routing
      * Default Policy
      * One(Record) to Many(IP)
      * Return all IP back to user in random order
      * User will be directed to random IP
    * ##### Weighted Routing
      * Split traffic based on weights
      * Good for A/B testing
      * ex) 85(EC2 Stable) : 15(EC2 Test)
    * ##### Geolocation Routing
      * Redirect Via Geolocation of request origion
      * ex) North America -> ALB US-NORTH-1
    * ##### Geoproximity Routing
      * Redirect Via Geolocation but with Bias Value
      * Bias value expand or shrink size of geolocation
      * Can only be set by Traffic Flow
      * ![](images/geoproximity_routing.PNG)
    * ##### Latency Routing
      * Direct traffic based on latency
      * Based on region
      * Requires latency resource record for EC2 or ELB
      * ex) 100ms(ALB WEST-1) : 12ms(ALB EAST-1)
    * ##### Failover Routing
      * If Primary fails Redirects to Secondary
      * Can check via Health Checks
    * ##### Multivalue answer Routing
      * Just like Simple Routing
      * Only difference is heath check
      * Returns IPs only if healthy
  * #### Health Checks
    * ##### Checks health every 30s by default
    * ##### Can be reduced to 10s
    * ##### Can Initial a failover if unhealthy
    * ##### CloudWatch Alarm can be created
    * ##### Can monitor other health checks for chain reactions
  * #### Route 53 Resolver
    * ##### Regional service that route DNS between VPC and your network
    * ##### Inbound(To VPC), Outbound(From VPC), Inbound and Outbound
    * ##### DNS Resolution for Hybrid Environments (On Premise with Cloud)
  
* ### Elastic Compute Cloud (EC2)
  * #### Choose OS, Storage, Memory, Network Throughput
  * #### Resizable computing capacity
  * #### Everyting on AWS uses EC2 instance underneath
  * #### Instance Types
    * ##### General Purpose
      * Balance of memory, compute and network
      * Use-cases : web servers and code repositories
    * ##### Compute Optimized
      * High performance processor
      * Use-cases : Scientific modeling, gaming servers and ad server engines
    * ##### Memory Optimized
      * Fast performance for workloads and large data sets in memory
      * Use-cases : In-memory caches, in-memory databases, real time big data analytics
    * ##### Accelerated Optimized
      * Hardware accelerators, co-processors
      * Use-cases : Machine learning, compute-finance, speech recognition
    * ##### Storage Optimized
      * High sequential read and write to large data sets on local storage
      * Use-cases : NoSQL, in-memory/transactional databases, data warehousing
  * #### Instance Sizes
    * ##### EC2 Instance Sizes generally double in price and attributes
    * ![](images/EC2_instance_sizes.PNG)
  * #### Instance Profile
    * Instead of embedding AWS credentials in Code
    * Let's instance have permission to access AWS services
    * Attach a IAM Role to an instance via Instance Profile
    * Always avoid unnecessary AWS credentials if possible
  * #### [Placement Groups](https://www.youtube.com/watch?v=-i1PfF4Jyuo)
    * ##### Cluster
      * Great performance, but has failure risk
      * Same rack, same AZ
      * Low latency, 10 Gbs bandwidth
      * If rack fails, all instance fails
      * Cannot be multi AZ  
      * ![](images/EC2_placement_group_cluster.PNG)
    * ##### Spread 
      * High availability, limited performance
      * Multi AZ  
      * Limited to 7 instance per AZ
      * EC2 on different physical hardware
      * Reduce simultaneous failure
      * For critical applications where each
      instance must be isolated from failure
      * ![](images/EC2_placement_group_spread.PNG)  
    * ##### Partition
      * Up to 7 partitions per AZ
      * Up to 100s of instances
      * Instances in a partition do not share
      rack with instances in another partition
      * EC2 metadata includes partition information
      * For HDFS, Cassandra, Kafka
      * ![](images/EC2_placement_group_partition.PNG)
  * #### UserData
    * Script that automatically run when launching EC2 instance
    * ![](images/EC2_user_data.PNG)
  * #### MetaData
    * Access information about EC2 via special url endpoint in EC2
    * curl http://169.254.169.254/latest/meta-data
    * Get information such as IPv4 address, instance type and more
    * Combind MetaData and UserData to automate AWS
  * #### Pricing Model
    * ##### On-Demand
      * Default pricing
      * No up-front payment
      * No long-term payment
      * For short-term, spiky, unpredictable, experimental, first-time apps
    * ##### [Spot Instances](https://www.youtube.com/watch?v=DI64Ol3dbAY)
      * Like hotels or planes, AWS offers vacant EC2
      * Save up to 90%
      * Instances can be terminated by AWS at anytime
      * If you terminate the instance you still will be charged for any hour it ran
      * Use-cases : Apps that can handle Interruptions, for non-critical background jobs
    * ##### [Reserved Instances (RI)](https://www.youtube.com/watch?v=01uV-clWkow)
      * Pricing = Class offering X Terms X Payment options
      * Class offering
        * Standard
          * Save up to 75%
          * Cannot change Instance Attributes
        * Convertible
          * Save up to 54%
          * Can change Instance Attributes only higher or equal in value
      * Terms
        * 1 year to 3 year contract
        * The longer the cheaper
      * Payment options
        * All Upfront
        * Partial Upfront
        * No Upfront
        * The greater upfront the cheaper
      * Can re-sell Reserved Instances
    * ##### Dedicated
      * Most expensive
      * Single Tenant instances with Isolated server
        * ![](images/EC2_dedicated_instance_multi_single_tenent.PNG)
      * Offered in On-demand and Reserved(70% save)
      * Enterprises and Large Organizations may have security concerns
  
  * #### [Amazon Machine Images (AMI)](https://www.youtube.com/watch?v=kkdr8Av2cQQ)
    * ##### EC2 into images to copy servers
      * Holds information such as
        * Root Volume
        * Operating system
        * Application Server
        * Application
        * Launch Permissions
        * Block device mapping
    * ##### AMI is region specific
      * You can copy to another region via Copy AMI
    * ##### AMI ID  
    * ##### Use Systems Manager Automation to patch AMIs with security updates
    * ##### Use LaunchConfigurations to update multiple instances with AMI
    * ##### Selection
      * Region
      * Operating System
      * Architecture
      * Launch Permissions
      * Root Device Type/Volume
        * Instance Store
        * EBS
    * ##### AMI marketplace
      * Community AMI
        * Free to use
      * Vendor AMI
        * Cost per hour
        * Security harden AMI such as CIS is popular
      * My AMI
    
  * #### Auto Scaling Groups (ASG)
    * ##### Group of EC2 for auto-scaling and management
    * ##### Launch Configuration
      * Launch settings for new EC2 from AGS
      * Cannot be edited
        * Clone the existing configuration or create a new configuration
      * Launch Templates
        * Launch Configuration with versioning
    * ##### Capacity settings
        * Min
        * Max
        * Desired Capacity
          * How much EC2 you want ideally
    * ##### Health check replacements
      * EC2 Health Check
        * Based on EC2 Status Checks
        * If considered unhealthy, restarts EC2
      * ELB Health Check
        * Pings an HTTP(S) endpoint and expects a response
        * If response not expected, restarts EC2
    * ##### Scaling policies
      * Scaling Out : Adding more Instances
      * Scaling In : Removing Instances
      * Scaling Up : Increase the EC2 Specs  
      * Types
        * Target Scaling Policy
          * ex) CPU exceeds 75%
        * Simple Scaling Policy
          * Scales when alarm is breached
          * Legacy, not recommended
        * Scaling Policy with steps
          * Scales when alarm is breached
          * Escalates based on alarm
          * ex) All 2 instances if alarm value is 2
    * ##### Elastic Load Balancers(ELB) with ASG
      * ASG can be associated with ELB
      * If associated richer health checks are available
      * Associated indirectly via Target Groups
    
  * #### Elastic Load Balancer (ELB)
    * ##### Must have at least two AZs
    * ##### Cannot go cross-region
    * ##### SSL Certificate can be attached to any Types  
    * ##### Rules of Traffic
      * ##### Listeners
        * Evaluate Traffic that matches the listeners port
        * Can attach SSL Certificate
      * ##### Rules
        * Rules will decide what ports goes to what target Groups
        * Only for Application Load Balancer
      * ##### Target Groups
        * EC2 instances are registered as target groups
        * Not for Classic Load Balancer
    * ##### Types
      * ##### Classic Load Balancer
        * Listeners and EC2 is directly registered
        * Can balance HTTP, HTTPS, TCP(Not at the same time)
        * Can use Layer 7 sticky sessions and Layer 4 TCP  
        * Can perform Cross Zone Load Balancing  
        * CLB does not allow you to apply rules to listeners
        * CLB -> Listeners -> Registered Targets
        * Responds 504(Timeout) error if not responding
      * ##### Application Load Balancer
        * Listeners, Rules and Target Groups
        * Designed to balance HTTP and HTTPS traffic
        * Operate at Layer 7 [(OSI Model)](https://www.youtube.com/watch?v=Ilk7UXzV_Qc)
        * Can use Sticky sessions  
        * Request Routing
          * Add routing rules to listeners based on HTTP protocol
          * Based on
            * Host Header
            * Http header
            * Source IP
            * Http header method
            * Path
            * Query String
        * Web Application Firewall can be attached
        * Great for Web Applications!
      * ##### Network Load Balancer
        * Listeners and Target Groups
        * Designed to balance TCP/UDP
        * Operate at Layer 4 (OSI Model)
        * Can handle millions of requests per second
        * Extremely low latency
        * Cross Zone Load Balancing
        * Great for Multiplayer Video Games or when network performance is critical
      
    * ##### Sticky Sessions
      * Specific user sessions goes to a specific EC2
      * All requests from that session are sent to the same EC2
      * Cookies are used to remember which EC2  
      * Can be used in 
        * Classic Load Balancer 
        * Application Load Balancer
      * Useful when specific information is stored in single instance
      
    * ##### X-Forwarded-For (XFF) Header
      * When using Load Balancers users IPv4 addresses can be changed to Load Balancers IPv4
      * Use X-Forwarded-For header to get the IP address
      * ![](images/X_Forwarded_For_header.PNG)
      
    * ##### Health Checks
      * Checks EC2 with HTTP(S)
      * Reports back as InService or OutOfService
      * ELB does not terminate(Kill) unhealthy instances
      * ELB just redirect traffic to healthy Instances unlike ASG
  
    * ##### Cross-Zone Load Balancing
      * Distributes traffic evenly within Zones
      * Distributes traffic evenly in all Zones
      * ![](images/cross_zone_load_balancing.PNG)
    
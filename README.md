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
    * DNS hostnames
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
      * Size /16 IPv4 [CIDR](https://www.youtube.com/watch?v=z07HTSzzp3o) (172.31.0.0/16)
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
    
    * Internet Gateway (IGW)
      * Allows VPC access to the Internet
      * Provide a target in VPC route tables
      * Performs network address translation ([NAT](https://www.youtube.com/watch?v=FTUV0t6JaDA))
        * Only Addresses with public IPv4
      * To connect to the Internet
        * Add route table
        * Route that table to Internet Gateway
        * Set destination to 0.0.0.0/0
      
    * Virtual Private Gateway (VPN Gateway)
    * [Route Table](https://www.youtube.com/watch?v=GrfOsWUVCfg)
      * Determines where network traffic is directed
      * Each Subnet must have a route table
      * One(Route Table) to Many(Subnet)
      * Can have multiple route tables in a VPC
      
    * Bastion / Jumpbox
      * ![](images/bastion.PNG)
      * EC2 instances for security
      * Help gain access to EC2 in private Subnet
      * Via SSH or RCP
      * NAT Gateways should not be used as Bastions
      * NAT Gateways intentions is for security updates
      * Systems Manager's Session Manager can replace Bastion
    * Network Access Control Lists (NACLs) Stateless
      
    * Security Groups (SG) Stateful
      
    * Public Subnets
      
    * Private Subnets
      
    * Nat Gateway
      
    * Customer Gateway
      
    * VPC Endpoints
      
    * VPC Peering
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
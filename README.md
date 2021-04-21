# Doe's awsGuide

### 이 repository는 :
AWS 전반의 공부를 기록으로 남기고자 만들었습니다.\
AWS Certified Solutions Architect 시험을 위해 만들었습니다.
### Studied from :
[AWS Certified Solutions Architect - Associate 2020](https://www.youtube.com/watch?v=Ia-UEYYR44s&t=299s)
* ## 시험
  * ### [주소](https://aws.amazon.com/ko/certification/certified-solutions-architect-associate/)
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
      * Reduced Avaiability 99.5%
        * Retrieval fee
      * Reduced Durabillity (Data could get destroyed)
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
    * Users uploads to distinct URL from edge Location
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

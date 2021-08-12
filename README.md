# aws-sa-associate-saac02
Course Files for AWS Certified Solutions Architect Certification Course (SAAC02) - Adrian Cantrill

If you find something wrong feel free to let me know at  saac02-feedback@cantrill.io 
- or - 
if you want to help fix something, feel free to submit a PR with your suggested fixes and I'll review

If you want to use any portion of this repo in your own projects, just make sure you are aware of the license terms ... and I'd appreciate a friendly heads-up :)


# aws accounts
- many companies use many aws accounts. 
- container for identities (resource) and resources 
- every account has an account root user - requires unique email address and credit card
- IAM - users, groups, and roles and also be created and given full and limited permissions (identity and access management)

# cli tips
- add user profile to your aws CLI
    ` aws configure --profile iamadmin-prod ` # This adds a profile to your aws cli.

# cloud computing
Set of 5 conditions that makes a platform a "cloud"
+ taken from NIST - national institute of standards and technology - 800-145
- 1. on demand self service - you can provision capabilities as needed **without requiring human interaction**.
- 2. Broad network access - Capabilities are available over the **network** and accessed through **standard mechanisms**. 
- 3. Resource Pooling - there is a sense of **location independence** no **control or knowledge** over the exact **location** of the resources. Resources are **pooled** to server multiple consumers using a **multi-tenant model**
- 4. Rapid Elasticity - Capabilities can be **elastically provisioned** and **released** to scale **rapidly** outward and inward with demand. "To the consumer, the capabilities available for provisioning often **appear** to be **unlimited**. 
- 5. Measured Service - Resource usage can be **monitored, controlled reported and billed** 

## Public vs Private vs Multi vs Hybrid Cloud
* Public Cloud - using 1 public cloud
* private cloud - using on-premisies **real** cloud
* Multi-Cloud - using **more than 1** public cloud
* hybrid cloud - Public and Private Clouds 
* hybrid cloud is NOT public cloud + legacy on-premis, that is a Hybrid network 

## Cloud Service - X as a Service
* Application Stack - Data/runtime/container/O.S./Virtualization/Servers/Infrastructure/
* on premises - manage the entire stack, hosting, and costs 
* ![Alt text](/screenshots/CloudServiceModel.jpg?raw=true "Cloud Service Model")

# YAML
* human readable for data serialization - human readable 
* unordered collection key:value pairs, each key has a value
* lists - ordered set of value - lists also have "-" hyphen 
* dictionary - data structure - 
```
Resources: (dictionary)
    s3bucket: (key which is also a dictionary)
        Type: "AWS::S3::Bucket" (proprety value string value )
        Properties: (dictionary containing)
            BucketName: "ac1337catpics" (key with the value of)
```

# JSON
* lightweight data-interchange format, easy for humans to ead and write, its easy for machines to prase and generate. 
* two main elements 
- Object, unordered set of key: value pairs enclosed by {&}
- Array, ordered collection of values, separated by commas & enclosed 

# OSI
- Physical - voltage and medium 
+ Data - Frames unique Hardware (MAC) - 48 bits in hex and 24 bits for manufacturer - OUI - Control access to the physical medium
1. Preamble 56 bits
2. SFD 8 bits - 
3. destination mac
4. Source Mac
5. ET EtherType - Protocol - 
6. Payload - Contains the data by the protocol - ethernet frame
7. FCS - Corruption Check
- carrier sense multiple access (CSMA) / CD (collision detection)
- Encapsulation - inside a frame and the payload is extracted from the frame - encapsulated 
- switches understand frames and mac addresses. they maintain a mac address table, which starts off empty. as the switch receives frames on its ports, it learns which  devices are connected and populates the mac address table 
- unicast 1:1 and broadcast 1:all 
## IPV4 addressing 
- Decimal Binary - Dotted-Decimal Notation 4x0-255

| Position              | 1     |     2 |     3 |     4 |     5 | 6     | 7     | 8     |
|   :---:               | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Binary Position Value | 128   | 64    | 32    | 16    | 8     | 4     | 2     | 1     |
| Binary Value          |       |       |       |       |       |       |       |       |

- ARP - Address resolution protocol (ARP)
- Network - Cross networking addressing
- ARP/Route/Route Tables/Routers
## Transport an Session 
+ TCP/IP and UDP/IP - Transport
- TCP Segments
    - Source port, destination Port
    - Sequence Number - error correction - and ordering
    - acknowledgement (syn/ack)
    - Flags n things 
    - window
    - checksum
    - urgent pointer 
    - options , padding
    - data
    - three way handshake 
     - Syn - sets CS
     - Syn-ack - increment cs+1, picks a random sequence ss (sends segment)
     - ack cs+2 and ss+1
- **Stateless firewall would see two things. Outbound, Response TWO rules for each TCP directions (in and out)**
- **Stateful firewall views seens one thing outbound, implicitly allows the inbound response** 
# NAT Network Address Translation 
- Static Nat - 1 priavte to 1 (fixed) public address (IGW)
- Dynamic Nat - 1 private to 1st available public
- Port address translation (PAT) - many private to 1 public (NATGW)
- Many:1(priateIP:PublicIP) Architecture The nat device records the source (private) IP and Source Port. Replaces the source IP with the single Public IP and public source port allocated from a pool which allows IP overloading (many to one)

# Subnetting 
## IPV4
- 4,294,967,296 total addresses available ipv4
- * ![Alt text](/screenshots/subnetting-visual.jpg?raw=true "Subnetting")

# DDoS
* distributed - hard to block individual IP/ranges
* application Layer - http flood
* protocol attack - Syn flood - doesnt send an ACK - fills up the network resources and the connections cant connect.
* volumetric - dns amplification
 - a botnet exploits a protocol where a response is significantly larger than the request. in this case making a spoofed request to dns, dns responds to spoofed IP for our application which is overwhelmed by the amount of data

 # SSL and TLS
 - TLS ensures privacy via encryption - asymmetric and then symmetric , identity (server/client server) verified - reliable connection protection 
 - Cipher suites - 
 - Authentication 
 - Key exchange 

 # AWS Fundamentals
 ## Aws Public vs Private Services
 - private and public - relate to the networking only
 - which network zone the service is in
 - aws public zone, directly connected to the internet. IE: s3 bucket - s3 service - hosted in the aws public zone - but doesnt mean you have access to it. 
 - aws private zone. No direct connectivity to the aws public or public internet. Isolated by default, and can be isolated via VPC - virtual private cloud - ie: ec2 instance 
 - you can allow selective connections to it via the aws public zone

 ## Aws global infrastructure 
 - AWS region , full compute storage db ai analytics
 - edge locations - local distribution points - content is stored in edge locations (CDN)
 - Geographic Separation - isolated fault domain
 - geopolitical separation - different governance. 
 - Region names: code or name
 - availability zone (multiple locations isolated infrastructure)
 - services can be placed across multile AV's with VPC - that can work across all AV's
 - define resilience level
    - Globally Resilient - data replication across entire regions 
    - region resilient - rds in Syndney - replicate data to multiple AV's 
    - AZ Resilient - single av zone service resilient

## VPC 
- VPC is a regional service that can operate in multiple AV's 
- Private and Isolated - from other VPCs and public AWS 
- Default VPC - 1 per region and Custom VPCs - but many custom VPCs
- VPC cidr defines the start and range of the addresses : its always 172.31.0.0/16
    - us-east-2a | us-east-2b    | us-east-2c 
    - configured for one subnet in every AV, its a smaller /20 
    - subnets assinged a public IPV4 addresses - default vpc they will have public IP addresses
    - tend to not use them on production services as they are to inflexible. 

## EC2
- IAAS - Provides Virtual Machines = instances 
- Private service by-default - uses VCP networking
- AZ resilient - instance fails if AZ fails
- sizes and capabilities 
- on demand billing - per second
- elastic block storage - EBS
- running - stopped - terminated 
- storage is still used even if its in a stopped state - EBS
- AMI - amazon machine image
    - attached permissions
    - public - everyone allowed
    - owner - implicit allow
    - explicit - specific aws accounts allowed 
    - ami contains the boot drive
    - block device mapping - boot volume or data volume
- create key pairs in advanced 

## S3 Buckets
- Global Storage platform - access from anywhere on the Internet. Regional based/resilient - at rest. 
- objects and buckets
    - object key is a file name - value is the data or content being stored. the value of the object can range from zero bytes to 5tb... 
    - buckets - primary home region unless you configure that data to leave that region - what laws and rules apply to that data
    - bucket name needs to be globally unique
    - bucket unlimited bytes of data - flat structure  
        - there are prefix on names though
        **Flash Cards**
        - exam power-up: - Bucket names are globally unique 
        - 3 and 63 characters all lowercase and no underscores 
        - limit of 100 buckets in an aws account 1000 hard limit 
        - unlimited objects in a bucket 0 bytes to 5tb
        - key = name, value = data
        - S3 is an object store - not file or block. Windows - file based storage. 

## Cloud Formation 
- Template written in yaml / json
- templates contains resoruces and all the other things 
- Resources are called logical resources - instance: type: aws::EC2::Instance
- stack is a living and reprentation of a template - physical resource - you update the resource/ it updates the stack

## Cloud Watch
Three Main Jobs
- Collects and Manages operational data - any logging 
1. Metrics - AWS Products, Apps, On-premises
    - cpu metrics, memory, disk, need cloud watch agent 
    - gathers and stores this data - api interface to access the data
2. CloudWatch Logs - AWS Products, Apps, on-premises
3. CloudWatch Events - AWS Services & Services 
    - generate an event to do something on a schedule or based off another event via SNS (Simple Notification Service)
+ CloudWatch Basics
- * ![Alt text](/screenshots/CloudWatchBasics.jpg?raw=true "CloudWatchBasics")
- Namespace 
    - Viewed as a "container" to keep the data in that namespace. 
    - AWS/${Service} ex: AWS/Ec2
        - can name them anything you want. 
- Metric 
    - Time Ordered Set of Data Points
    - Alarm - Metric is not in a good state and you can define an action 
- Dimension
    - Separate datapoints for different things or perspectives within the same metric. 

### Demo CloudWatch
- CLI Commands: `sudo amazon-linux-extras install epel -y` & ` sudo yum install stress -y ` 

## Shared Services 
- ![Alt text](/screenshots/SharedServices.jpg?raw=true "SharedServices")

## HA VS FT VS DR
- High Availability vs Fault-Tolerance vs Disaster Recovery 
+ HA - aims ot ensure an agreed level of operational performance, usually uptime, for a higher than normal period. Minimizing any outages.
+ FT - Fault Tolerance - is the property that enabled a system to continue operating properly in the event of the failure of some (one or more faults within) of its components. 
+ DR - A set of policies, tools and procedures to enable the recovery or continuation of virtual technology infrastructure and systems following a natural or human induced disaster. 

# IAM Identity Policies 
- Understanding their architecture and read them is required for the exam
- Grants access or denies access to your aws services
+ ARN: Amazon Resource Name - Uniquely Identify resources within any aws account(s)
+ Effect: action verb to the event: ie: deny,allow
+ Rules: First Priority
    - Explicitly Denies, nothing can overrule
    - 2nd Priority: Explicit Allow 
    - DENY, ALLOW, DENY
- Inline Policy (json) and Manged Policies - how they are managed. 
- Managed policy is their own object whic than can be attached to each identity. THey should be used for the normal default operational rights in your business. 
    - Low management overhead, update json, it updates all the identities asap.
    - use inline for special or exceptional allow/deny 
- Customer managed policies that you can modify; default aws policies. 

## IAM users
- IAM users are an identity used for anything requiring long term aws access. EG: Humans, Applications, Service Accounts 
- IAM Starts with a principal which represents an entity trying to access an aws account. They can be individual people, computers, services or a group of any of those things.
    - must been authenticated and authorized. 
- ARN: arn:partition:service:region:account-id:resource
- arn: arn:partition:service:region:account-id:resource-type/resource-id
- only **5,000** IAM user per account (remember the 5000)
- max of 10 groups
- Use federation or IAM Roles if its more than 5k IAM users.

## IAM GROUPS
- IAM groups are containers for Users 
- You can NOT log into a group - no credentials 
- Orginization of IAM users. Users can be on multiple groups. 
- Both in-lined and managed - which allow/deny that a user has directly - all still follow deny/allow/deny
- no max group membership - trick question around an "all users group" does not exist natively 
- no groups within group. 
- groups have users, and permissions.  - 300 groups per account max. can be increased. 
- groups are not a true identity - they cant be referenced as a principal in a policy 

## IAM Roles - The Tech - Review
- I am roles are also identities - by an unknown number or multiple aws users, humans, applications or services inside or outside of your aws account. 
- if you ahve more than 5,000 principals, its good idea to use iam role.
- TEMPORARY of time then stops
- role represents a level of access within inside an aws account. Short term.
- temporary credentials are time limited before they expire 
- STS secure token service - sts:AssumeRole = Roles
- Roles can be Assumed
- When assumed - temporary credentials are generated

## When to use IAM roles - When to use IAM roles - review
- Within the same AWS account - AWS Lambda - execution role , whever a function is executed 
- Emergency or out of the usual situation - break glass situation... ie fire alarm 
- to re-use...On-premises - existing identities active directory - external accounts or identities can not interact with AWS. 
- Web Identity Federation which uses IAM roles
- Partner Accounts - use a role in the partner account - get temp security credentials. 

## IAM AWS org
- Management account, can invite existing standard aws account into the AWS organization. 
- Change from standard accounts to being member accounts. 
- Billing is then removed and passed to the management account. aka Payer account - aws account that contains the payment method of the org. 
- use IAM roles in multi account setups 
- most orgs use one clean and one account for the logins. 

## AWS Org DEMO Part 1 & 2
- how to role switch into the production account. 
- When you create an account within the organization a **role is created within that account which an be role switched into by other accounts within the organization** 
- If you invite an existing aws account into the organization, then you need to manually add this role.

## SCP Service Control Policies
- Used to restrict AWS accounts. 
- Policies document that can be attached to the root container or one or more org units - even individual aws accounts. 
- Service Policies inherit downward. Or OU with inheritance. 
- SCP's are account permissions boundaries
- They limit what the account (including the account root user can do)
- they dont grant permissions. 
- Explicit deny always wins. 

## SCP Demo
- 

## CloudWatch Logs
- Public Service - AWS Public Zone - Usable from AWS or On Premises
- Store, Monitor and Access logging data
- AWS Integrations - ec2, vpc flow logs, lambda, CloudTrail, R53... 
- Needs connectivity and permissions. 
- Security normally provided by IAM roles or service roles
- Custom logs - unified cloud watch agent
- development kit form AWS and integration it directly into your application
- It can contain metrics like failed SSH connections then you can create alarms that watch for the metric.
- Regional Service 
- Log events inject it into the region YYYMMDDHHMMSS MESSAGE
    - /var/log/messages - each log log stream is unique, and ordered set
    - log groups - containers for log streams
    - log groups also contain, retention and permissions, metric filters

## Cloud Trail
- Logs API calls/activities as a CloudTrail Event 
    - by default stores 90 days in Event History
    - No cost, if 90 days. 
    - to customize create 1 or more trails
    - Management events and data events
- Cloud Trail is a regional service OR can be set to ALL regions TRAIL. 
- Data events has to be set manually 
- stores it in json and compresses them into an s3 bucket it can also go into cloud watch logs. (log parser)
- EXAM -
    * Enabled by default but 90 days
    * Trails are how you configure s3 and CWLogs - Default for Trails is to store management events ONLY (creating instance, stopping, logging into the console)
    * IAM, STS, CloudFront - global services, and that gets logged to the us-east-1
    * and a trail will need to be enabled to capture that. 
    * NO REALTIME - there is a delay - 15 mins normally 

## Cloud Trail Demo
- provides a certain amount of free tier service - only a certain amount of data

# S3

## S3 Security
- S3 is private by default
- S3 bucket policy aka a form of resource policy 
    - allow/deny same or different accounts
    - Resource perspective permissions
    - Like identity policies but attached to a bucket.  
    - allow/deny anonymous principals 
    - two main goals: give access to other aws accounts and 
    - ACLs are used, but not recommended. 
    - Block Public Access - 
* Exam Power Up
    - If you are granting or Denying permissions on lots of different resources across an aws account, then use Identity Policies
    - single place: IAM - IAM is the only single place where you can control permissions for everything. 
    - Permissions within the same account (no external access) - 
    - if you want to grant a single permission to everybody accessing one resource or everybody in one account, then its much more efficient to use resource policies to control that base level permission. 
    - Anonymous / external identities from other aws accounts: Resource Policies 

# S3 Static Hosting
- Index and Error documents are set , HTML files , 
- Static website hosting endpoint. Generating by region and bucket name. 
- custom name - bucket name requires the domain
- offloading - static media hosting , static html
- out-of-band pages - an error or a status notification system. Maintenance page, change dns the point it to a backup static HTML page / support page. 
- cost, per gig month fee, transfer fee (data / out) per gig charge 
- Free
    - 5 gb
    - 20k get requests
    - 2k put requests
## S3 Demo

## Object Versioning & MFA Delete
- Object is controlled at a bucket level - you can not disabled it again
    - you can suspend it, and then re-enabled. 
    - lets you store multiple version of objects within a bucket. Operations which would modify objects generate a new version. 
    - new object is known as the current object Latest version OR Current Version
    - individually accessed by specifying the ID. 
    - delete marker 
    - you can delete the object with the version number
    - MFA is required to change bucket versioning state
    - MFA is required to delete versions
    - need the Serial Number MFA + Code passed with API calls

## S3 Performance Optimization 
- Make the upload faster / safer with Multipart Upload
    - minimum size is for 100MB 
    - parts can fail and be restarted
    - improves transfer rate
    - transfer acceleration - must be enabled for transfer
        - no periods in name
        - uses edge locations
        - dns compatible in its naming
        - picks the closest, best performing S3 edge location

## Encryption 
- Plaintext - unencrypted data - image and applications 
- Algorithm - blowfish, aes, rc4, des, rc5, rc6
- key - "password" 
- ciphertext - encrypted data - need the key to decrypt 
- know what Asymmetric is and how it works
- Signing 
    - used to verify identity. 
    - encrypt using your private key
    - party can use your public key to decrypt to verify identity
- Steganopraphy 
    - message of hiding something 
    - hide a message in a image 

## Key Management Service KMS
- Regional and Public Service 
- Public Service, public zone access from anywhere but need permissions
- can handle symmetric and asymmetric keys (encrypt, decrypt)
- KMS Keys never leave (provides FIPS 140-2)
- CMK Customer Master Key - applications, services, and users can use them
    - logical - ID
    - backed by physical key material
    - generated and or imported
    - CMK can be used for encrypted and decrypt for only up to 4kb of data
- Data Encryption Key (DEKs)
    - Generate Data Key works on larger than 4kb
    - plaintext version first and ciphertext version 
    - discard the plaintext one
- Exam PowerUp
    - CMK's are isolated to a region and never leave. 
    - They also never leave the KMS service
    - AWS managed CMK's or Customer Managed CMK's 
        - Customer Much more configurable 
    - support key rotation - it cant be disabled every 1095 days (3 years)
    - CMK's backing key and previous backing keys - aliases
        - per region - alias no keys are globally
        - key policies - CMK has a IAM / Principal 
        - action KMS
        - identies can manage a key, also may not be able ot use a key

## KMS Demo
* using kms on CLI
    -   
        ```
            aws kms encrypt \ 
            --key-id alias/catrobot \ 
            --plaintext "path to file" \
            --output text \ 
            --query CipherTextBlob \
            --profile iamadmin-general | base64 \ 
            --decode > not_battleplans.enc
        ``` 

    - 
        ``` 
            aws kms decrypt \
            --ciphertext-blob fileb://not_battleplans.enc \
            --output text \
            --profile iamadmin-general \
            --query Plaintext | base64 --decode > decryptedplans.txt        
        ```

## Object Encryption - PART1 and 2
- Buckets arnt encrypted, objects are
    - client-side encryption
    - server side encryption (both are at rest on S3)
    - Both use in-transit encryption
- Server side encryption 
    - Server-Side Encryption with Customer Provided Keys (SSE-C) 
        - Need an plain text object and a key
        - when they arrive at teh S3 endpoint | hash is ta ken and attached to the object, then s3 encrypts the object. Then the key is discarded for security. 
    - Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)
        - put just the plaintext artifact 
        - s3 handles all encryption 
        - it is the default option
        - AES-256
    - Server-Side Encryption with Customer Master Keys (CMKs) Stored in AWS Key Management Service (SSE-KMS)
        - S3 will create an aws managed customer master key (CMK)
        - Roles are important, KMS policy and permissions must have decryption
        - s3 administrators can admin but not have a way to decrypt.
    - Bucket Default Encryption
        - x-amz-server-side-encryption PUT header. 
        - objects will not use encryption unless its passed. 

## Demo Object Encryption
- 

## Object Storage Classes 
- S3 Standard - 3 availability zones - 11 9's 
    - has a milliseconds first byte
    - standard for frequently access data which is important and none replaceable
- S3 IA - In frequent access
    - 3 av's 
    - first byte is still millisecond
    - Its cost effective using IA
    - There is a retrieval fee + transfer fee 
    - bill minimum duration charge of 30 days 
    - minimum capacity charge of 128 KB per object 
    - Should be used for long lived data which is important but where access is infrequent
- S3 IA - One Zone-IA
    - does not provide the multi-az resilience model - only one az is used
    - used for long lived data, which is infrequently accessed, also non CRTICAL data
    - 

## Object Storage Classes Part 2
- S3 Glacier 
    - 3 az
    - same durability 7 9's. 
    - 1/5th the cost of s3 standard 
    - first byte latency = minuets or hours - cold/chilled storage
    - 40kb min size and 90 day min duration
- S3 Glacier Deep Archive 
    - standard is 12 hours
    - bulk is up to 48 hours
    - rare or if ever need access   
    - legal and regulatory requirements, throw old archive data at.
- S3 Intelligent-Tiering
    - Intelligent-Tiering monitors and automatically moves any objects not access for 30 days to a low cost infrequent access tier and eventually to archive, or deep archive tiers.
    - As objects are accessed, they are moved back to the frequent access tier.
    - no retrieval fees for accessing objects, only a 30 day minimum duration
    - unknown or uncertain usage, use Intelligent-Tiering

## S3 LifeCylce Configuration
- Optimize costs
- Set of rules consist of actions on a bucket, or groups of objects.
- transition action (s3 standard to IA after 30, IA to glacier after 90 days)
- Expire action, objects for cost optimization
- ![Alt text](/screenshots/S3LifecycleConfigurationTransitions.jpg?raw=true "S3 Life Cycle")

# S3 Replication
- Cross-Region Replication (CRR)
- Same-Region Replication (SRR)
- if its in a different aws account
    - role is configured for replication
    - you need an additional requirement, bucket policy to allow the role in the source account to write to its bucket form the origin bucket
- what to replicate ? 
    - All objects or a subset of objects (tags, prefix, ect..)
    - Storage Class - defaults to maintain 
    - storage class is the same as the destination and origin
    - ownership - default is the source account
        - different accounts - by the owned source bucket account
    - Replication Time Control 
        - 15 min SLA guaranteed replication 
        - only use if you have really strict requirements on storage replication
- Exam Power up
    - **Replication is not Retroactive & Versioning needs to be ON**
    - One-way replication Source to Destination only. 
    - Unencrypted, SSE-S3 & KMS (with extra config)
    - Source bucket owner needs permissions to objects
    - No System events, Glacier, or Glacier Deep archive
    - no deletes are replicated
    - SRR - Log Aggregation
    - Prod and Test sync - replicate data dev to prod
    - Resilience with strict sovereignty 
    - 
## DEMO Cross-Region Replication of an S3 Static Website 
- Disaster Recovery 

## S3 Presigned URLs
- Presigned URLs are a way that you can give another person or application access to an object inside an s3 bucket using your credentials in a safe and secure way. 
- can enable put or get request via the iamadmin who generates a presignedURL
- Exam Power Ups
    - You can create a URL for an object you ahve no access too
    - When using the URL, the permissions match the identity which generated it
    - access denied could mean the generating ID never had access or doesnt know
    - Dont generate with a role, URL stops working when temporary credentials expire
    - never a good idea to generate a presigned URL using an IAM role. Generally use an IAM user vs role. 

## S3 Select and Glacier Select
- Select let you use sql-like statement
- part of the object pre-filtered by s3

## S3 Events
- event notifications on a bucket
- delivered to sns, sqs, lambda functions 
- Object created (put,post,copy,completemutlipartUpload)
    - on object creation, send the object to some destination, then have an event driven automated workflow
- EventBridge is a bit newer and more features. 

## Access Logs
- access logging can be enabled via the console UI or via PUT Bucket logging
- S3 Log Delivery Group, bucket acl, allows s3 log delivery group

# Virtual Private Cloud (VPC) Basics
## Networking Refresher Part 1 & 2
- IP - Refresher
- 10.0.0.0`
- 172.16 - 172.31.255
- 192.168.0.0 - 192.168.255
- /8 A /16 B /32 C

## VPC Sizing and Structure - Part 1 & 2
- VPC cider / range - need to know what range the VPC will use In advance
- what size should your VPC be? 
- are there any networks we cant use? 
- try to predict the future
- vpc structure - tiers, and resiliency and AV's 
- starting point of 10.16 ~ 
- how many aws regions the aws account will operate in
    - pre-allocating - reserve 2+ networks per region being used per account

- VPC Sizing
    - a subnet is in one AV 
    - **how many availabilty zones your VPC will use**
    - this decision impacts high availability and resilience and it depends on somewhat on the region that the VPC is in.
    - generally start with three as the default, because it will work in almost any region, with one spare.
    - need to split the VPC into at least 4 networks or 4 / 18's 
    - teir: Web, app, db, spare
    - ![Alt text](/screenshots/VCPSizing.jpg?raw=true "Structure Example")

- Guidelines
    1. You consider the business needs
    2. avoid the ranges that you cant use
    3. allocate the remainder based on your business Physical, or logical layout, and then decide upon and create VPC and subnet structure from there.
    4. work either with top down or bottom up, you can start with the minimum subnet size that you need and work up or reverse

## Custom VPCs
- Nat gateway - which will give private instances outgoing only access
- Internet gateway which will give resources in the VCP public access
- bastion  - connect securely into the VPC
- Regionally Service and ALL Az's in the region 
- nothing in or out without explicit configuration
- flexible configuration - simple or multi-tier 
- hybrid networking
- default or dedicated tenancy (dedicated hardware)
    - ipv4 private cidr blocks and public
    - 1 primary private ipv4 cider block
    - min /28 max /16
    - optional secondary ipv4 block
    - optional single assigned ipv6 /56
    - dns in a vpc - base ip + 2
    - Exam - enableDnsHostnames - gives instances DNS Names
    - enableDnsSupport - enables DNS resolution in VPC 

## VPC Subnets
- Blue means private subnets, green means public 
- Subnet: AZ Resilient 
    - a subnetwork of a VCP - within a particualr AZ
    - 1 submnet => 1 AZ, 1 AZ => 0+ Subnets
    - IPV4 CIDR is a subset of the VPC Cider
    - Cannot overlap with other cidr
    - Subnets can communicate with other subnets in the VPC
    - Reserved IP addresses (5 in total)
        - example: 10.16.16.0/20 (10.16.16.0 => 10.16.31.255)
        - Network address (10.16.16.0)
        - Network + 1 (10.16.16.1) - VPC Router (dfg)
        - Network + 2 (10.16.16.2) - Reserved DNS
        - Network + 3 (10.16.16.3) - Reserved Future Use
        - Broadcast address (10.16.31.255 last ip in subnet)
    - DHCP Option set applied to one VPC at one time - flows to subnets

## VPC Design Demo
- ipv6 - can be allocated with a /56 CIDEr

## VPC Routing and Internet gateway Bastion Hosts
- simply routes traffic between subnets and VPC'
- local always takes priority
- IGW (internet gateway)
    - Region Resilient gateway attached to a vpc
    - you do not need a gateway per av
    - 1 vpc = 0 or 1 IGW
    - Internet gateway runs from the border of the VPC and the aws Public zone
    - its what allows services inside a PVC which are allocated with public IP's to be reached from th einternet.
    - IGW maintains the public IP
    - IPV4 has no public IP on the EC2
- Bastion Host / Jumpbox
    - incoming management connections arrive there
    - access internal VPC resources
    - integrate with SSH

## Network access control lists (NACls)
- "firewalls that surrounds subnets"
- in or out of a specific subnet 
- ephemeral ports - inbound and outbound 
- nothing is denied by the VPC by default
- Exam power up
    - stateless - initiation and response seen as different (need to add two rules)
    - only impacts data crossing subnet border 
    - Can explicitly allow and Deny traffic (one particular deny, use ACL)
    - IP's/network, ports and protocols - no logical resources
    - NACLs cannot be assigned to AWS resources only subnets
    - Use with SG's to add explicit Deny bad ip / s nets
    - One subnet = one NACL at a time

## Security Groups
- Security groups are assigned to an aws resource (network interface of a aws product)
- NACLS are stateless (initiation and response)
- Security groups are stateful 
    - only one rule is required for bi-directional traffic 
    - a default security group is created on a VPC
    - rule is allow all traffic
    - references itself
    - have a hidden implicet denied | if its not allowed, its denied. 
    - you can not explicity deny on a single rule/ip/resource. use ACLs for that.
- Exam Power up
    - Stateful - Traffic and Response = same rule
    - SG's can filter based on AWS logical Resources
        - Resoruces, other than SG's and even themselves.
    - Implicit Deny and Explict Allow
        - No Explicit Deny
    - NACLs on subnet for any products whic dont work with SG's (eg Nat Gateway's)
    - NACLs when adding explicit deny (bad ip's, bad actors)
    - SG's as the default **almost everywhere** 

## Network Address Tanslation (NAT) and NAT Gateways
- giving a private resource outgoing only access to the internet. 
- static nat - 1:1 ration
- ip masquerading - hiding CIDR blocks behind one IP - Classes Inter-domain routing
- Runs from a **public subnet** - already need a VPC where it has public subnets (internet gatway/and default routes/pointing at the IG)
- Uses elastic IP's (static ipv4 public)
- AZ resilient Service (HA in that AZ)
    - one nat gateway in each AZ that you are using in a VPC
        - route table to private subnets for each AZ with that NATGW as a target
- Managed, Scales to 45 gbps, $ Duration & data Volume
    - NAT Gateway is HA in the AZ, but you need them in each AZ - not the region
    - enable ec2 as nat: disable source destination checks. 
    - no bastion
    - can not do port forwarding
    - only NACL's - NO Security Groups
- EC2 - Nat Instance 
    - if the AZ fails, it fails entirely 
    - can be cheaper (ie dev/stage)
- NAT isnt required for IPv6
    - if you add IPV6 as a route, you get bi-directional connectivity to the aws public zone
    - will not work with NAT gateway/Nat-Instance
- SSH Agent Forwarding
    - generate ssh key pair
    - public part is added as authorized keys
    - only used int he initial phase connection
    - ssh-add - adds it to the ssh-agent service
    - -A (or ssh agent forwarding)

## NAT Gateway Demo
- Elastic IP doesn't change 
- explicitly set a route table with a subnet with that same AZ to enable routing.

# Ec2 Section

## Virtualization 101

## EC2 Architecture
- Use most often on AWS - a lot of exam questions
- ec2 instances run on ec2 hosts
- shared hosts or dedicated hosts 
- AV resilient service - if the AZ fails, the Ec2 instance could also fail
- Instances cannot natively move between AV. Hardware, networking, storage, locked inside one AV zone.
- when to use
    - application compute app needed
    - support requirements 
    - long running compute needs
    - bust or ready state
    - monolithic application stacks
    - migrated applicaiton workloads or DR 

## EC2 Instances Part 1 and 2
- General Purpose - default - diverse workoads, equal resource ration
- Compute optimized - media processing, hpc, scientific modelling, gaming, machine learning
- memory optimized - processing large in-memory datasets, some databse workloads
- accelerated computing - hardware gpu, field programmable gate arrays (FPGAs)    
- Storage Optimized - Sequential and Random IO - scaled-out transactional databases, data warehousing, esasticsearch, analytics workloads
- R5dn.8xlarge
    - R : Instance Family
    - 5 : Instance Generation 
    - 8xLarge : Instance Size
    - dn - Additional Capabilities 
- https://instances.vantage.sh/

## Storage Refresher 
- Direct (local) attached Storage - Storage on the ECT Host
- Network Attached storage - volumes delivered over network (EBS)
- Ephemeral Stroage - Temporary Storage
- Persistent Storage - Permanent storage - lives on past the lifetime of the instance
- Block Storage - volume presented to OS as a collection of blocks. 
    - Mountable, and Bootable 
- File Storage - Presented as a file share, mountable, NOT bootable. 
- Object Storage - collection of objects **flat** - Not mountable. not bootable.
- Storage Performance
    - IO (block size) X IOPS (input output operations per second) = Throughput
    - IOPS - You can think as speed at which the engine of a race car uns at, the revolutions per second.
    - IO - as the size of the wheels of the race car. 
    - Throughput as the end speed of the race car. 

## EBS Elastic Block Store
- Block storage - raw disk allocations (volume) - Can be encrypted using KMS
    - instances see block device, and create file system on this device (ext3/4, xfs/ ntfs)
- storage is provisioned in ONE AZ (resilient in that AZ) - single point of failure
- attached to *one ECT instance (or other services) over a storage. 
- can do multi attach - but the cluster application has to manage it, otherwise overwritten data
- can be detached and reattached to one instance .. persistent (on restart)
- snapshots backup into s3 - create volume from snapshot (migrate between az's)
- physical storage types, different sizes, different performance profiles
- billed based on GB-month 
- **no cross AV attachment possible**
- snapshot volumes to S3 to backup data - then create ebs volume in another AV - also regions

### EBS Volume Types
- General Purpose SSD - GP2
- as small as a 1gb or large as 16tb
- an IO credit is 16KB - IOPS assume 16KB - 1 IOPS is 1 IO in 1 Second
- 5.4 million IO credits, fills at rate of baseline performance (size / rate)
- 100 IO credits per second 
- max 16k 
- great for boot volumes, dev/test, low-latency interactive apps. 
- GP3
    - SSD based - removes the credit bucket arch
    - standard 3000 iops (3016kb / second 125 MB / second)
    - 1gb to 16 tb
    - !20% cheaper
    - higher max throughput - 1000 mb / second 
    - virtual desktops, medium sized single instances DB's MSSQL or Oracle
    - low-latency interactive apps, dev and test, boot volumes.

## EBS Provisioned IOPS SSD
- 3 types - Io1 / io2 / io2 block express
- iops are configurable independently of size - 
- highly performant drives 
- 256k iops per volume - block express 4/mb/s
- 4gb to 16 tb - express 64 tb volumes 
- io1 560IPS / gb max
- io2 500 iops/gb max
- express 1000iops/gb max
- per instance performance: 
    - io1 - 260k iopps and 7500 mb's
    - io2 - 160 iops & 4750 mb's
    - io2 express 260k 7500 mb's 

## EBS HDD Based
- st1 throughput optimized 
    - cheap
    - designed for data to be written or read
    - 125gb to 16tb
    - 500 mb / second
    - big datya, data warehouses, log processing
- sc1 - cold hdd
    - cheaper 
    - in frequent work loads
    - dont care about performance
    - 250 max iops 1mb 250 / mbs
    - 125 gb to 16 tb 

## Instance Store Volumes
- provide block storage devices - used as the basis for a filesystem
- physically connected to one ect host
- each ec2 host has its own instance volume
- highest storage peformance in AWS
- included in the instance price 
- have to attach them at launch time - cant do it afterwards. 
- view all instance store volume as ephemeral (temporary) data does not move to new instances, nor faster instances
- D3 = 4.6 gb's throughput 
- i3 = 16 gb's seconds - nvme storage
- Exam powerups
    - local on ec2 hosts
    - add only at launch time
    - lost on instance, move, resize, or hardware failure 
    - high performance 
    - you pay for it anyway - included in intance price 
    - temporary 

## EC2 Instance STore vs EBS 
- Persistance storage = use EBS (avoide instance store)
- Resilience = EBS
- Storage Isolated from instance lifecylce = ebs (attach and reattach)
- Resilience w/ app In-build Replication... it depends 
- High performance needs...depends
- Super high perofmrance needs .... instance store
- cost ..instance store (its often included)
- Cheap = ST1 or SC1
- Throughput..streaming..ST1
- Boot = NOT ST1 OR SC1
- Gp2/3 up to 16k iops per volume 
- Io1/2 up to 64k iops (block express 256k iops) 
- Raid0 + EBS up to 260k IPS (io1/2-BE/GP2/3)
- More than 260k ips = Instance Store (just keep in mind its not persistant)
- ![Alt text](/screenshots/InstanceStorevsEBS.jpg?raw=true "Instance store Vs EBS")

## EBS Snapshots
- Efficient way to backup
- snapshots are incremential volume copies ot s3
- new ebs volume = full performance immediately 
- snaps restore lazily - fetched gradually 
- requested blocks are fetched immediately 
- force a read of all data immediately 
- FSR (fast snapshot restore) - up to 50 per region
- billing
    - gigabye - month
    - used not allocated (only bill what you use)
    - 

## EBS Snapshot Demo 1 / 2
- set the UUID on the /etc/fstab for the replicated volume
- sudo mount .a
- sudo mount /dev/xvdf /ebstest
- sudo file -s /dev/**drive name**
- sudo mkfs -t xfs /dev/nvme1n1 
- sudo mkdir /instancestore

## EBS Encryption
- default no encryption is applied. 
- provides at rest encryption for volumes and snapshots
- Exam Powerup
    - Aws accounts can be set to encrypt by default - default CMK or use manually 
    - eaches volume uses 1 unique DEK per volume
    - snapshots and future volumes use the same DEK
    - can not change a volume ot NOT be encrypted. 
    - OS isnt aware of the encryption - no performance loss. 
    - if it states in some way that it needs the OS  needs to have the keys and or needs to be ecnrypted, then you need to performan wholde disk encryption
    
## Network Interfaces Instance Ip's and DNS
- In this lesson we deep dive into the Elastic Network Interfaces (ENIs) which can be allocated to EC2 instances - and the DNS, public, private and elastic IPs which can be assigned to those ENIs.
- primary private ip 
- 1 or more elastic IP per private ipv4
- Secondary ENI + MAC = Licensing
- multi-homed subnets 
- different security groups - multiple interfaces. 
- OS never sees the public IPV4. never configure network interface with public IP
- Public = Dynamic / Start/Stop = Change. Or forced migration.
- Static ip = elastic IP
- public dns = private IP in vpc, public IP everywhere else. 

## wordpress demo 1/2
- systemctl enable httpd - autostart on system startup
- systemctl enable mariadb - auto start on startup

## Amazon machine Images (AMI)
- AMI's can be used to launch EC2 instances. 
- community provided
- marketplace (can include commercial software) 
- regional/unique UID e.g ami-0a887e401
- Lifecycle
    1. Launch
    2. Configure
    3. Create Image
    4. Launch
- Exam Powerups
    - AMI's are in One region - in a particular region - can be used to deploy into all AV's
    - AMI Baking - creating an AMI from a configured instance + application
    - AMI can not be edited, launch instance, update configuration and make a new AMI
    - Can be copied between regions (includes it snapshots)
    - Remember permissions default = your account - can make the AMI completly public, or individual aws accounts
    - Will be billed for the EBS snapshots

## AMI Demo 1/2
- configure base image
- shutdown machine
- create ami > image and templates 
- create snapshot automatically on the OS drive

## Instance Billing Models 
- on-demand 
    - instances have an hourly rate 
    - billed in seconds or hourly 
    - default pricing model
    - no long-term commitments or upfront payments
    - new or uncertain application requirements 
    - short term, spiky, unpreditable workloads which cant tolerate any disruption 
- Spot Instances
    - Spot pricing offers up to 90% off vs on-demand
    - based on spare capacity 
    - specfify a max price, and if met, instances are terminated. 
    - apps which can tolerate failure and continue later
- Reserved Instances 
    - up to 75% off on-demand for a commitment
    - 1 or 3 years, all upfront, partial upfront, no upfront. 
    - reserved in region or az wich capacity reservation 
    - scheduled reservations
    - know steady state usage (email/domain/dns/)
    - lowest cost for app which cant handle disruption 
    - need reserved capacity 

## Instance Status Checks and Auto Recovery
- two default checks
    - system check (power/hardware/network)
    - Instant Status (OS issues, network configuration )
    - can auto recover - re-launch a new host 

## Horizaontal and Vertical Scaling
- Vertical
    - each resize requires a reboot - disruption 
    - larger instances often carry a $ premium
    - there is an upper cap on performance - instance size
    - No application modification required
    - works for ALL applications - even monliths 
- Horzontal Scaling 
    - Sessions are critical in your app
    - requires application support or off-host sessions
    - no disruption when scaling 
    - no real limits to scaling - other than cost
    - often less expensive - no large instance premium
    - more granular on how you scale 
- Exam Power up
    - ![Alt text](/08-EC2-Basics/00_LearningAids/Horizontal_Vertical_scaling.png?raw=true "Horizontal Scaling and Verticle")

## EC2 Instance Metadata
- Data about the instance that can be used or configured about the system/environment
- accessable inside ALL instances: http://169.254.169.254/latest/meta-data/
- Catagory's information 
    - environment
    - networking
    - instance metadata can be used by applications to get IP information
    - authentication 
    - user-data
    - not authenticated - authenticated
- Demo
    - curl http://168.254.169.254/latest/meta-data/public-ipv4
    - query tool
    - wget http://s3.amazonaws.com/ec2metadata/ec2-metadata
    - make execute chmod u+x ect-metadata
    - ./ec2-metadata --help

# Containers and ECS
## Intro
- docker image created from scratch or base image. 
- dockerfile - used to build docker images. 
- each step creats file system layer. 

## Containers ECS Demo
- review docker make / build commands

## ECS
- Elastic Container Service (ECS)
- Cointainer Definition
    - image and ports to use
    - task definition - security (task role), Cointainers, resoruces - what can they access inside aws
    - task role - IAM role which the TASK assumes
    - Service - How many copie, HA, Restarts 
- Service Definition 

## ECS Cluster Mode Types
- ECS EC2 mode
    - Runs in a VPC which benifits multiple av zones
    - Scheduling and Orchestration - Cluster Manager / Placement Engine
- Fargate Shared Infrastrucure
    - No visiblity of other customers
    - same task and service definitions
    - allocated resources 
    - still have the VPC on your own account - they auto allocate those form the fargate shared environment

## ECS Cluster Mode Types Demo
- EC2 vs ECS (EC2) VS Fargate
    - if you use containers already than use ECS
    - Make sense if you are just wanting to isolate applications
    - small overhead of running the tool
    - Large workload - price concious - EC2 Mode
        - only if admin overhead is minizmed
    - Large workload - overhead conscious - Fargate 
    - Small / Burst workloads - Fargate
    - batch / Periodic workload - fargate (pay for what you use)

# Advanced EC2
# Boot strapping EC2 using user data
- allows EC2 build automation 
- user data - accessed via the meta-data ip 
- excuted only once on launch
- user data is not secure - no passwords or long term credentials
- lmited to 16kb in size
- can be modified when instance stopped

## bootstrapping demo
- 

## Enahanced Bootstrapping with CFN-INIT
- helper script which is intalled on EC2 OS
- works with stack updates. 
- listens to the user-data

## Enhanced bootstrapping demo 

## EC2 Instance Roles and Profile Advanced Ec2 and Demo
- credentials are inside meta-data
- iam/security credentials/role-name
- temporariy secure credentials
- automatically rotate - always valid
- should always be used rather than adding access keys into instance
- Demo
    - create an IAM role
    - s3ReadOnlyAccess
    - attach IAM role to the instance. 

## System Manager Parameter store (SSM) and DEMO
- lets you create configuration and secrets 
- String, StringLists, and SecureString
- license codes, database strings, usn/pw's
- plaintext and ciphertext (uses KMS)
- app/lambda/ec2 can have access via IAM to the paramater store
- Demo
    - paramater store is located Under Systems Manager console
    - create paramater 

## System and Applicaton Logging on EC2 and DEMO
- CloudWatch is for metrics
- Logs is for logging data..CLoudwatch
- neither nativly capture data inside an instance 
- the cloudwatch agent is required 
- needs configuration and permissions 
- create an IAMRole CloudWatch Logs to the Ec2 instance
- DEMO
    - 

## Ec2 Placement Groups
- physically close together or not - 
- Cluster - Pack instances close together
    - highest level of permance possible inside of EC2
    - Have to be apart of a single AV zone. 
    - Run same phyical space (same rack sometimes same host)
    - 10gpbs single stream
    - Exam
        - Cant span AZ
        - Can VPC Peers but impacts performance 
        - Requires a supported instance type (not all images work)
        - use the same type of instance (not mandatory) but best practice
        - launch at the same time
        - 10gpbs single stream performance
        - performance, fast seepds, low latency
- Spread - keeps instance separated
    - for max amount of availability and resilience
    - can spread multiple AV zones
    - seperate isolated infrastructure racks, own networking, power supply 
    - limit 7 instances per AV
    - Exam
        - provides infrastrucutre isolation- each instance runs from a different rack
        - 7 instances hard limit
        - not supported for dedicated instances or hosts
        - usecase: small number of critical instances that need to be kept separated form each other
        - domain controllers
        - file servers
        - its handled by aws of orgnization of the spread placement group
- Partition - groups of instances spread apart
    - can be used in multiple AV's
    - max per 7 per region
    - partitions - has its own racks - no sharing between parttions
    - launch as many instances as you want 
    - aws can auto decide or you can decide 
    - share this information with toplogly aware information
        - HDFS, Hbase, Cassandra
        - make intelligent data replication decisions 
    - you need to adminiter the partition placement. 
    - Exam
        - 7 partitions per AZ
        - Instances can be placed in a specific partiion or auto placed
        - partition placement groups ar enot supported for dedicated hosts
        - great for HDFS, Hbase, Cassandra. 

## Dedicated hosts
- dedciated to you entirely
- family e.g a1,c5,m5
- no instance changes you pay for the host
- on demand, and reserved options available 
- host hardware has physical sockets and cores
- licensing model comes into play for this (via cpu core ect...)
- A1 - 1 socket - 16 cores
- R5 (nitro host) 2 sockets 48 cores. Use different sizes at one time
- Limitations and Features
    - AMI limits, RHEL, SUSE LInux and Widnows AMI's are not supported
    - Amazon RDS instances are not supported
    - Placement groups are not supported for dedicated hosts
    - Hosts can be shared with other ORG accounts...RAM
    - only control the hosts that you create / instances. 
    - general solves licensing issues

## Enhanced Networking & EBS Optimized 
- USES Single Route I/O Virtulization (SR-IOV) - Nic is virtulization aware
- physical network inside ec2 host is aware of virtulization
- allows for higher I/O and Lower host CPU usage
- More bandwidth faster networking speeds
- dedicated NIC card basically 
- available for most ec2 with no charge
- EBS optmized instances 
    - its either on or off
    - block storage over the network

# Route 53 (its always DNS)

## Public Hosted Zones
- dns database (zone file) hosted by r53 (public name servers)
- accessable from public internet and vpcs
- hosted on 4 r53 name servers specific for the zone
- resoruce records (RR) created within the hosted zone
- externally registered omains can point at R53 Zone
- walking the "dns" tree

## Private Hosted Zone
- assocated with VPC's and only accessible in those VPC's
- needs to be assoicated with the private hosted zone
- split view horizion dns
    - allows ot created a public hosted zone with the same name

## Cname vs ALIAS
- cname maps name to another name. 
- cname can not be used to the TLD record - that requires an alias
- alias record map a name to an aws resource
- nake/apex and normal records
    - api gateway, elb, cloundfront, global accelator and S3

## Routing policies Route 53
- simple routing supports 1 record per name
    - does not support health checks
- each record can have multiple values
- all values are returned in random order

## Health checks and Demo
- health checkers are located globally 
- anything accessible over the internet
- every 30 seconrds 
- tcp/http/https/ and with string matching (layer 7)
- Demo
    - 

## Failover Routing && Demo
- multiple records of teh same name. 
    - primary and secondary 
- if the target of the health check is unhealthy, any queries return the secondary record of the same name
- demo
    - 

## Multi Value Routing
- many records with the same name
- aims to improve availability by allowing a more active, active approach to DNS.
- ![Alt text](/screenshots/MultiValueRouting.jpg?raw=true "Multi Value Routing")
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
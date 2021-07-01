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
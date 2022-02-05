# certifications

## Cloudfront 
### Cloudfront origin
- S3 bucket 
- S3 web site
- Custom Origin ( ALB/on prem http)

Support origin HA 
OAI like IAM for cloud front 
Custom EC2/ALB - must be public ( need to allow edge location IPs in SG) 

* Cloud front vs S3 Cross region replication 
* signed url vs signed cookie ( mulriple files) 
* cache based on http headers/session cookies/Query string  


* Improve Cloudfront  caching
  - less headers values and whitelist headers
  - two caches : split static and dynamic content 

* Cloudfornt,APIGW  - 100000 TPS 

* cloudfront caching vs api gateway caching 
  - api gateway edge
  - api gateway regional with cloudfront (no cache) 
  - api gatweway regional with cloudront cahce

* lambda @ edge 
  - lambda is deployed in cloudfront and can change cloudfront requests and responses 
  - no caching 
  - intercept request and check authentication and autorization 
  - dynamic web application at the edge 
    https://aws.amazon.com/blogs/networking-and-content-delivery/lambdaedge-design-best-practices/ 

* Redis vs Memcache
  - Memcache - non persistent, no backup and restore
  - Redis - like RDS 
## Blocking IP address 
*  Blocking IP with NLB can bw done
  - no SG for NACL
  - SG group - allow 
  - Deny one address - only NACL 
* ALB + WAF
  - more expensive 
  - rules  

## S3 
### Encryption 
- SSE S3
- SSE KMS
- SSE C ( enforce https)
- Client side

### Events
- S3 access logs ( might take hours )
- S3 Events notifications 
- Trusted advisor
- Cloudwatch events 


## Security 
Type of attacks
- DDOS - infra level layer 3/4  -> Shield 
- Application level ( it http , invalidtiang cache etc)  

- Shield - R53/ALB/ENI/Cloudfront 
- Shield advanced - 3000$ , against more sophisticated attacks
- WAF is layer 7 - sql injection , , can help in DDos if rules defined 
- WAF ACL
  * rules on ip address 
  * Size/geo  constraints  
- WAF - ALB/APIGW/AppSync OR Cloudfront 
 
## AWS config
- remdiation using SSM automation 
- Rules can trigger cloudwatch event with can trigger Lambda 


## Guard duty 
Input :
- Cloud trail logs 
- VPC flow logs 
- DNS logs 

Notify Cloud watch events


## AWS orgnization policies 

AI services opt-out policies
Artificial Intelligence (AI) services opt-out policies enable you to control whether AWS AI services can store and use your content.Learn more 

Backup policies
Backup policies enable you to deploy organization-wide backup plans to help ensure compliance across your organization's accounts. Using policies helps ensure consistency in how you implement your backup plans.Learn more 

Service control policies
Service control policies (SCPs) enable central administration over the permissions available within the accounts in your organization. This helps ensure that your accounts stay within your organization’s access control guidelines.Learn more 

Tag policies
Tag policies help you standardize tags on all tagged resources across your organization. You can use tag policies to define tag keys (including how they should be capitalized) and their allowed values.Learn more 


## EC2
### placement group stratgies
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html

In Cluster Placement group, all instances are placed within a rack. If the rack fails (hardware failure), all instances fails at the same time. Hence, this is not suitable for High Availability or mission critical applications. But ideal for High Performance applications, as all the instances are in very close proximity to each other.

In Spread Placement group, each instance is placed in its own distinct rack. Each rack has at most one instance. A rack failure (hardware failure) will not affect more than one instance. Hence, this is ideal for High Availability or mission critical applications. But not really suitable for High Performance applications, as the instances are spread much further apart.

In Partition Placement group, each partition represents a rack. If a rack fails (hardware failure), it may affect multiple instances on that rack, but only within that partition. This way, failure of one partition is isolated from the rest of the partitions. So, if you have replication in other partitions, then your data will be safe. This placement group strikes a balance between High Performance and High Availability. This will be good for Big data applications like HDFS, HBase, Cassandra, Kafka, etc. which needs High Performance, but must also be Fault Tolerant at the same time.

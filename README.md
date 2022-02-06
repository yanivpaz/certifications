# Certifications

## VPN
- site to site (software VPN is needed on premise)
  - Static routing  (define routes)
  - Dynamic routing BGP ( define ASN in CGW on prem and VGW in AWS ) 

- client VPN  - using open VPN
- software VPN - on prem and AWS 

## DR
- RPO - backup
- RTP - recover time

stratgies
- backup and restore
- pilot light
- warm standby
- Hot site

## Migration services 
Application discovery service
- agentless discovery
- agent based discovery

SMS - server migration serivce ( replace vm export /import):
- vSphere.hyperV ,Azure
- increment replication of live servers

## Database migration 
- DMS - copy from source to data (only S3 and RDS can be source out of AWS services)
- SCT - schema migration when changeing the DB engine 

## Snow
- Data migration 
   - snowcone - small , light - 8 TB
   - snowball edge  80 TB storage 40 vcpu 80 Gib RAM /42 TB compute ,52vcpu ,208 Gib RAM
   - snow mobile - truck - 1EX- 1000000 TB
- Edge Computing 
  -  snowcone 
  -  snowball edge 

## Storage Gateway
- File Gateway(applicance)  - EFS backed by S3 - can restore single file
- Volume Gateway - local disk - need to restore all to access file
  * cached - full data on s3 
  * stored - scheduled backup to s3
- Tape  - Glacier - need to restore all to access file

## Step function 
Tasks: 
-lambda
-http
-service task - Batch , SNS , SQS, Dymo DB ,ECS task 
-wait 

AWS mechanical turk - use SWF only

## SQS
* Consumer need to implement idempotency as messages can appear twice
* Lambda event source mapping - use polling ( 1-10 message)
* sns-> several SQS = common practice 

## Route53
* Routing
  - Simple - no health , client will select random in case of multiple records
  - Weighthed - can be associated with health checks 
  - Active - passive ( if primary health check failes)
  - Latency  + failover 
  - Geo location 
  - Complex - nested records  
  - Multi value 

* Health check 
  - text search in the first 5120 bytes
  - pass codes is: 2XX 3XX 
  - Calculated health check - check other health check 
  - can access private endpoints 
  - Can create CW metric + alarms . health check can check the alarm .
 
## Load balancers 

* ALB
  - 400 ms latency
  - routes according to routes
  - hostnames
  - query strings in http headers 
  - ALB + lambda vs APIGW + lambda 
  - ALB trgets - ec2/ecs/lamnda/ip address 
  - SNI - support multiple certificate
  - always cross zone 
  - no charges for inter AZ data 
  
* NLB
  - 100 ms latency 
  - onr static IP per AZ
  - extreme perfomence
  - cant used lambda express 
  - not cross az by default
  - pay for inter AZ data if enabled 
  - no stickiness 
 
# API GW
  - Why - rate limiting , cachine , user autentication 
  - timoue is 29 seconds 
  - 10MB pay loads 
  - API changes are deployed to stages 
  - Integrations
    * http
    * Lambda
    * AWS service  (SQS , step function) 
   - Endpoints :
      - Edge optimized  - default - through cloudfront 
      - Regional
      - Private - per VPC 
  - Gateway Cache 
     - per stage
     - per mthod 
     - Client to bypass (max-age=0 in cache-control header ) cache 
     - API GW cache - TTL 5 min by default  TTL 0 - no cache
  - Errors
     - client 4XX - 403 WAD filtererd , 429 Quota 
     - server 5XX  -504 backend didnt answer more than 29 seconds     
  -Soft limit : 10000 api per second
 
## Lambda 
* docker dont use Lambda - but  ECS , Batch , Fargate 

Limits 
 - RAM 128MB - 3GB
 - CPU linked to RAM ( 1.5GB more CPU is added )
 - 15 minutes
 - /tmp id 512MB
 - deploymenyt package is 250MB
 - soft limit : 1000 concurrent by default 
 - cold (100ms ) vs waorm (ms ) invocation time
 - APIGW , Cloudfront - 100 ms invocation 

Invocation 
 - Synchronous
 - ASynchronous - S3,SNS,CW events - 3 retrys .
 - Event Source mapping - polling from Kinesis Data streams,SQS , DynmoDB  streams - reprocess until success 

Destionations
 - Asynchrinztion invocation - successful events only -  SQS/SNS/another Lambda/EventBridge bus (similar to DLQ . destinations is the recommended )
 - Event Source mapping -  discarded events only - SQS/SNS

Version 
 - code 
 - configuration ( resources , env variables ) 

Use DLQ for failure

Codedeploy integration 
- Linear
- Canary 
- All at once 

Can create pre and post Lambda hooks to check health of the Lambda function 


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

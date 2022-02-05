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

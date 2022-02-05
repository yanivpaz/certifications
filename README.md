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
 

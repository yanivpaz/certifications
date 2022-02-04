# certifications

## Cloud fronts 
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


* baetter caching
  - less headers values and whitelist headers
  - two caches : split static and dynamic content 


* cloudfront caching vs api gateway caching 
  - api gateway edge
  - api gateway regional with cloudfront (no cache) 
  - api gatweway regional with cloudront cahce

* lambda @ edge 
  - lambda is deployed in cloudfront and can change cloudfront requests and responses 
  - no caching 

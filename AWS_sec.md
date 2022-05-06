## SSO with ADFS
https://aws.amazon.com/blogs/security/aws-federated-authentication-with-active-directory-federation-services-ad-fs/  

https://d1.awsstatic.com/security-center/SecurityBlog/federated_auth_with_adfs_25.dc86ecbfbbf80af3f553e7374d2a55ad1afb7016.png  



## VPC scenario
https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html  

## Cognito 
identity pool vs users pool
user pool - authentication ,authorization 
identity pool - federation ( ie get access keys to AWS services)


https://docs.aws.amazon.com/cognito/latest/developerguide/identity-pools.html


## S3 access
* identity policy - user/group/role
* resource based - ie bucket policy 


By default, when another AWS account uploads an object to your S3 bucket, that account (the object writer) owns the object, has access to it, and can grant other users access to it through ACLs. You can use Object Ownership to change this default behavior so that ACLs are disabled and you, as the bucket owner, automatically own every object in your bucket. As a result, access control for your data is based on policies, such as IAM policies, S3 bucket policies, virtual private cloud (VPC) endpoint policies, and AWS Organizations service control policies (SCPs).

A majority of modern use cases in Amazon S3 no longer require the use of ACLs, and we recommend that you disable ACLs except in unusual circumstances where you need to control access for each object individually. With Object Ownership, you can disable ACLs and rely on policies for access control. When you disable ACLs, you can easily maintain a bucket with objects uploaded by different AWS accounts. You, as the bucket owner, own all the objects in the bucket and can manage access to them using policies. For more information, see Controlling ownership of objects and disabling ACLs for your bucket.
https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-walkthroughs-managing-access-example3.html  

### s3 acl 
- ACLs disabled (recommended)  
  All objects in this bucket are owned by this account. Access to this bucket and its objects is specified using only policies.  
- ACLs enabled  
  Objects in this bucket can be owned by other AWS accounts. Access to this bucket and its objects can be specified using ACLs.  


## Config 

- managed rule  
- custom lambda rule  
- custom rule using gurad  
Create custom rules using Guard Custom Policy that evaluates whether your AWS resources comply with the rule.  
 

trigger :
- periodic ( 1/3/6/12/24 hours) 
- when configuration changes
( all changes , resources , tags - any resource) 


remidiation - using system manager
custom rules -  via Event bridge and Lambda

## SSO
Enable SSO for AWS accounts / applications ( ie - Jenkins )  
Identity source can be AWS SSO / Active directory/ External identity provider  
https://www.pingidentity.com/en/resources/blog/posts/2021/sso-vs-federated-identity-management.html   

## Directory service
- AWS managed AD (standard < 5000  , enterprise > 5000 )  
- Simple AD (based on Samba4)  - not supporting trust relationshipds, DNS dynamic update ,MFA and other  
- AD connector (proxy - on premise AD and Cloud )  (small < 500 , large <5000)   

## Incident response

https://docs.google.com/document/d/11_1lNSNMI7tRTmfBR74FOkaQbDfVZPZ7u0H4tFXRrGs/edit?usp=sharing
prepare ,detect , containment , investigation , recovery, lessoned learned )

### Detect 
1. AWS console login error
 - cloudwatch and cloudtrail
 - aws config to detect changes


### containment
#### Access keys 
1. deactivate the keys 
2. Add deny all so temp credantials will not be valid 

#### EC2 
1. isolate the ec2 instance  (ie ingress only from specific machine , block egress)
2. memory dump
3. ebs snapshots 
4. perform forensic analysis
5. terminate the isntance 



### logging and monitoring
https://docs.google.com/document/d/1uv2T_huTXApm9Pu7fSz2D8Ir6gvHjC8wyiNy792LHTY/edit?usp=sharing  


### AWS security hub
* Guard duty
* AWS inspector
* AWS Macie
* IAM analyzer 
* AWS config for CIS / PCI checks 
* Many other AWS services
* External providers 

### Infra security
#### AWS WAF

Rule
contain : statement , condition , action 
- regular rule ( predefined rules / extrenal providers / my own rules ) 
- rated base rule ( ie - 100  request in 1 minute)

can be associated
-  ALB
- API GW
- App sync 
- Cloudfront 

#### AWS Firewall manager 
https://youtu.be/u27HLad-Wi8?t=2507  

* manage 
  - WAF rules
  - Sheild advanced 
  - Security group 
* Prerequistits :
  - Enable AWS Orgnization 
  - Enable AWS config in all the accounts
  - Designate an AWS account as Firewall admin 

### IAM 
### Data protection


## AWS tools
### AWS Security Hub

### Amazon GuardDuty 
Threat detection and continuous monitoring of your AWS Accounts.
Using
* Cloud trail
* VPC flow log
* DNS log 
* EKS ( new)

findings example - https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_finding-types-active.html

Amazon Inspector 
Analyze the behavior of your AWS resources and identify potential security issues.

Amazon Macie 
Classify and protect your sensitive and business-critical content.

Amazon Detective 
Investigate security issues.

AWS Systems Manager Patch Manager 
Centralized management for patching your fleet of Windows and Linux instances.

AWS Firewall Manager 
Central management of firewall rules.

AWS Config 
Assess, audit, and evaluate the configurations of your AWS resources.

AWS Sheild 

AWS Inspector 



- AWS Sheild - DDOS
- WAF ACL - 
  - global - cloud front
  - regional APIG/ALB

## related links
https://www.splunk.com/en_us/software/user-behavior-analytics.html  

Nessus vulnersbility tool - vs aws inspector 
meta sploit - penetration testing 

Penetration test require approval ( except sevarl services - EC2,RDS,Cloudfornt , Aurora,APIGW ,Lambda,Lighsail ,Beanstalk) 
several activities is not allowed at all 

metasploit - use expolits on various software
```
search easychat
use <>
set RHOST
webcam_snap
```
https://www.udemy.com/course/aws-certified-security-specialty/learn/lecture/7889384#announcements

CVE - updated from national vulnerability database 
https://nvd.nist.gov/  

https://owasp.org/www-project-top-ten/

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

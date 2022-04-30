
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
### Infra security
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

Nessus vulnersbility tool 
meta sploit - penetration testing 
Penetration test require approval ( except sevarl services - EC2,RDS,Cloudfornt , Aurora,APIGW ,Lambda,Lighsail ,Beanstalk) 

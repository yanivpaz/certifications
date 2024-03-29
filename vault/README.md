



## Links 
https://github.com/ned1313/Hashicorp-Certified-Vault-Associate-Getting-Started  
https://github.com/ned1313/Hashicorp-Certified-Vault-Associate-Vault-Management  


[seal](seal.md)    
[kv](kv.md)   
[approle](approle.md)  
[transit](transit.md)  
[curl](curl.md)  



## General terms 
accessor - view token properties /capabilities/renew or revoke token 
vault barrier - anything running in the memory

cfg file:
Vault storage backend ( consul / fs /AWS DynmoDB /AWS S3 )  - https://www.vaultproject.io/docs/configuration/storage
Vault seal type ( ie - AWS KMS ) 

UI:
Vault authentication ( LDAP /Approle/OIDC/JWT/TLS/AWS /K8s /Okta/Github  )


## Secrets types 


Some secrets engines simply store and read data - like encrypted Redis/Memcached. Other secrets engines connect to other services and generate dynamic credentials on demand. Other secrets engines provide encryption as a service, totp generation, certificates, and much more.

1) store : ie - kv https://www.vaultproject.io/docs/secrets/kv
2) generate: AWS - generate dynamic AWS credantials (support iam,assumed_role,federation_token) /DB /Other
3) encrypt: transit




## response wrapping
https://github.com/ned1313/Hashicorp-Certified-Vault-Associate-Getting-Started/blob/main/m7/5-response-wrapping.sh  
```
vault kv get -wrap-ttl=60m  mysecrets/test-secret  
vault unwrap hvs.CAESIIKLWcxQhj_6_pLGOyitMl9fX5QKTyUeRiL16fVW1c0wGh4KHGh2cy5MbnRScmxaSlhsZVhVbTZKSEFVSU5waU4  
vault unwrap hvs.CAESIIKLWcxQhj_6_pLGOyitMl9fX5QKTyUeRiL16fVW1c0wGh4KHGh2cy5MbnRScmxaSlhsZVhVbTZKSEFVSU5waU4  
#second time will fail as is single use  
```  


## Vault engine
vault agent
can be used for various cases 
- auto auth ( token is written to sink , renew the token ) 
- template - render secrets to files + run commands ( ie - create env files )
  very good solution for applications that reads property files / env variables 
- caching 
https://github.com/ned1313/Hashicorp-Certified-Vault-Associate-Vault-Management/blob/main/m7/vault-agent.hcl

vault agent -config=vault-agent.hcl




## leases and ttl 
similar terms 
service tokens - ttl  
dynamic secret - lease ( renew/revoke ) 
- no direct command for lookup /sys/lease/lookup


lease_id
lease_duration
lease_renewable



## secrets engine
static 
dynamic
transit- encryptions 

vault kv get/put - for kv only 
vault read/write - for all of secrets engine besides kv

identity engine
entity - client ( linked to token ) 
alias - Link  entity /group  auth method ( users/groups in AD )
group  - internal / external
https://github.com/ned1313/Hashicorp-Certified-Vault-Associate-Vault-Management/tree/main/m5


## Clustering
Node:
- Active (responsible for all read and write)
- Standby ( ready to take over )
- Performance standby - can process read request ( write forward to active nodes)

require load balancer in front of the cluster 
health check : v1/sys/health ==> 
200 is active ( initilized and unsealed )
429 is standby
503 sealed 

replication - enterprise level feature 
- DR ( KV , policies ,token - no client response)
- Performance ( KV , policies - response to client for reads )- for cross data centers / regions 


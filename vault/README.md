

[seal](seal.md)    
[kv](kv.md)   
[approle](approle.md)  



## General terms 
accessor - view token properties / capabilities/renew or revoke token 
vault barrier - anything running in the memory

cfg file:
Vault storage backend ( consul / fs /AWS DynmoDB /AWS S3 )  - https://www.vaultproject.io/docs/configuration/storage
Vault seal type ( ie - AWS KMS ) 

UI:
Vault authentication ( LDAP /Approle/OIDC/JWT/TLS/AWS /K8s /Okta/Github  )




## Secrets types 
Vault secret engine (default is KV /AWS ) 
1) store : ie - kv https://www.vaultproject.io/docs/secrets/kv
2) generate: AWS - generate dynamic AWS credantials (support iam,assumed_role,federation_token) /DB /Other
3) encrypt: transit

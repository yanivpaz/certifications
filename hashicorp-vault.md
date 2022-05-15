##  Components
- api
- storage backend
- components - audit , acl  , token store etc.
- barrier ( seal ) on all the components 

##  Backend 
official storage backends are consul and file 

## Secrets 

## Authentication methods
- can use github / LDAP 
- vault issue token that can be used by the client 
- default is tokens

## Audit tokens
```
vault aidit enable file file_path=/var/log/vault_audit.log 
```

## Vault Paths
- secrets/app,common

## Community vs Enterprise 



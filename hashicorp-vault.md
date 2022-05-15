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

## Unseal 
- unseal with key shards
- unseal with auto unsel 
- unseal transit selal 

## commands
start server   
```
vault server -dev
# will generate ~/.vault-token 
```

get status  
```
export VAULT_ADDR="http://127.0.0.1:8200"
vault status 
remarks:
-  shows that vault is initilized ( vault operator init is not needed )  
-  we should replace the the root token  with another authentication method  

```


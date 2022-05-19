## KV example 
```
# as root 
vault server --dev -dev-root-token-id="root" --log-level debug
vault kv put mysecrets/test1 key1=value1
#vault kv put mysecrets/test1 key2=@myfile # put myfile 
vault kv get mysecrets/test1 # we can use -version=1

vault auth enable userpass
vault write auth/userpass/users/myuser password=mypass policies=mypolicy
vault policy list # no mypolicy 

# as user
vault login -method=userpass username=myuser password=mypass
vault kv get mysecrets/test1

# as root 
mypolicy.hcl:
path "mysecrets/*" {
  capabilities = ["read"]
}

export VAULT_TOKEN=hvs.CvuPsSJ4MLY2otHgxcnIlDwQ
vault policy write mypolicy ./mypolicy.hcl

# as user 
unset VAULT_TOKEN # token is used from .vault-token
vault token capabilities mysecrets/test1

-- Adding policies 
# as root
vault write auth/userpass/users/myuser/policies  policies="mypolicy,mypolicy2"

# as user
vault login -method=userpass username=myuser password=mypass
vault token lookup | grep policies 
```



## KV 2 walk through 
 vault kv enable-versioning  mysecrets

vault kv put  mysecrets/test1 key1=value1
 vault kv get mysecrets/test1
 vault kv put  mysecrets/test1 key4=value4
 vault kv get mysecrets/test1
# will show version 2 with key4=value4

 vault kv delete  mysecrets/test1
 vault kv get mysecrets/test1
# will show version 2 with empty destroyed=false

vault kv destroy -versions=2 mysecrets/test1
# will show version 2 with empty destroyed=true


 vault kv get -version=1  mysecrets/test1
# will show version 1 with key1=value1




# to delete 
# vault kv metadata delete 

vault kv metadata get mysecrets/test1
# will show the max versions 


vault kv metadata put -max-versions 2 mysecrets/test1

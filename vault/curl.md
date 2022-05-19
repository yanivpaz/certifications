# Curl 
```
 cat data.json
{
   "password": "mypass"
}


1) curl --request POST --data @data.json $VAULT_ADDR/v1/auth/userpass/login/myuser --cacert tls.crt --capath . | jq
2) curl --header "X-Vault-Token: hvs.CAESIH1UwEL-HgeIQnEI1OH9EECR8K2ZqANYEkBCXN7HrbqmGh4KHGh2cy40Uk95eXRwU0pzR1BZdFk4SnFqaUYwOFM" --request GET  $VAULT_ADDR/v1/mysecrets/test1 --cacert tls.crt --capath . |jq

```

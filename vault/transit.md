Encryption (Transit engine):
- convergent - deterministic ( support in AES   , rsa not supporting)
  encrypted value will always the same all the time regardless the key version .
  less secure
- each key is actually map of keys 
  - working set - all available keys
  - archive set - can be retrived but not loaded to memory


## flow
- enable
- add keys (internal / external)
- view keys
- encrypt
- decrypt 
- rotate


https://github.com/ned1313/Hashicorp-Certified-Vault-Associate-Vault-Management/tree/main/m6

```
vault path-help transit/
vault write -force transit/keys/ccid
vault list  transit/keys
vault read transit/keys/ccid


#  value should be base64 encoded 
vault write transit/encrypt/ccid plaintext=$(base64 <<< "124")
```
encrypted value with metadata  :    
ciphertext     vault:v1:XzHaRwI0bJjbthAeVHNQ/ClIvvtzh9a6XHxB2wW31nM=


```
vault write transit/decrypt/ccid cyphertext=vault:v1:XzHaRwI0bJjbthAeVHNQ/ClIvvtzh9a6XHxB2wW31nM= 
json_data=$(vault write transit/encrypt/ccid plaintext=$(base64 <<< "124") --format=json)
ciphertext=$(echo $json_data |jq .data.ciphertext -r)

plaintext=$(vault write transit/decrypt/ccid ciphertext=$ciphertext  --format=json|jq .data.plaintext -r)
echo $plaintext | base64 -d

vault write -force transit/keys/ccid/rotate
```

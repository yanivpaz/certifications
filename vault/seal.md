## Seal 
* shamir secret sharing   
- key shares ( key shares , require thresholds, configured during initalization)  
* auto unseal  
- ie KMS  
- recovery key shares 
* transit seal  


 

rekey - update unseal and master key
vault operator 


keyshares -> assembeled to unsealed key ( key share OR cloud/hsm service) 

vault operator init 
-key-shares=3  -key-threshold=2  (shamir)
-recovery-shares 2 - recovery-threshold=2 ( autoseal)


seal - meaning that Vault throw away the master key and require unseal to perform further operations 
no operation possible  beside unseal and status 

When should I seal ?
- key shards
- detection of compromised or network intrusion 

key shards - split master keys to differnet members  ( total shares - number of shared keys , Threshold - minimal ammount to create master)
usualy encrypted with pgp keys 

cloud auto unseal ( need KMS/HSM/Another Vault ) - supported in  Enterprise and open source

Transit unseal - master key is saved in seperate vault cluster - supported in  Enterprise and open source


/etc/vault.d/vault.hcl

vault operator init -key-shares=3 -key-threshold=2
vault operator unseal

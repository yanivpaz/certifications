```
vault write  auth/approle/role/myrole name="myrole"
vault read auth/approle/role/myrole/role-id # 0d36ef87-e95d-dfea-3be0-5f3e47a35bdb
vault write  -force  auth/approle/role/myrole/secret-id # 2233fc56-01da-0669-fb7d-a259e97e3a3b 
vault write  auth/approle/login role_id=0d36ef87-e95d-dfea-3be0-5f3e47a35bdb secret_id=2233fc56-01da-0669-fb7d-a259e97e3a3b
# we need to use the provided token explicilty unlike login 
```

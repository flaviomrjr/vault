VAULT COMMANDS
==============

# VAULT READ
```shell 
# READ DEFAULT TOKENS POLICY
$ vault read sys/auth/token/tune

# READ TOTP CODE
$ vault read totp/code/secret

# READ APPROLE ID
$ vault read auth/approle/role/jenkins/role-id
```

# VAULT WRITE
```shell
# ENCRYPT WITH TRANSIT
$ vault write transit/encrypt/my-key plaintext=encode64

# DECRYPT WITH TRANSIT
$ vault write transit/decrypt/my-key cyphertext=

# CREATE TOTP
$ vault write -field=barcode totp/keys/flavio generate=true issuer=vault acount_name=flavio@gmail.com

# CREATE APPROLE
$ vault write auth/approle/role/jenkins token_policies=captalys-operator

# CREATE APPROLE SECRET
$ vault write -f auth/approle/role/jenkins/secret-id

# CREATE RANDOM 164 BYTES
$ vault write sys/tools/random/164 key=value

# CREATE HASH
$ vault write sys/tools/hash key=value
```

# VAULT LIST
```shell
# LIST TOKEN ACCESSORS
$ vault list auth/token/accessors
```

# VAULT SECRETS
```shell
# ENABLE SECRET ENGINE
$ vault secrets enable -path=secretkv -version=2 kv
$ vault secrets enable aws

# DISABLE SECRET ENGINE
$ vault secrets disable aws

# MOVE SECRET ENGINE
$ vault secrets move aws aws2

# LIST SECRETS ENGINE
$ vault secrets list

# TUNE (CHANGE DEFAULTS)
$ vault secrets tune -default-lease-ttl=72h secrets/
```

# VAULT KV
```shell
# CREATE SECRET
$ vault kv put secret/marvel name=flavio

# GET SECRETS
$ vault kv get secret/marvel
$ vault kv get -version=1 secret/marvel

# DELETE SECRET VERSION SOFT
$ vault kv delete -versions=1 secret/marvel

# RESTORE SECRET VERSION
$ vault kv undelete -versions=1 secret/mavrel

# DELETE SECRET VERSION PERMANENTLY
$ vault kv destroy -versions=1 secret/marvel

# DELETE SECRET
$ vault kv matadate delete secret/mavel
```

# VAULT AUTH
```shell
# ENABLE AUTH METHOD
$ vault auth enable approle
$ vault auth enable userpass

# DISABLE AUTH METHOD
$ vault auth disable userpass/

# LIST AUTH METHOD
$ vault auth list
```

# VAULT TOKEN
```shell
# CREATE TOKEN
$ vault token create
$ vault token create --ttl=300
$ vault token create -policy=operator
$ vault token create -ttl=200 -explicit-max-tl=600 -policy=operator

# CREATE WRAP TOKEN
$ vault token create -wrap-ttl=600

# CREATE ORPHAN TOKEN
$ vault token create -orphan -policy=operator

# CREATE BATCH TOKEN
$ vault token create -type batch -policy=operator

# LOOKUP TOKEN 
$ vault token lookup
$ vault token lookup <token>
$ vault token lookup -accessor <accessor-tokne>

# CHECK TOKEN CAPABILITIES
$ vault token capabilities secret/marvel
$ vault token capabilities -accessor <accessor-token> secret/marvel

# RENEW TOKEN
$ vault token renew -increment=200 <token>
$ vault token renew -increment=200 -accessor <accessor-token>

# REVOKE TOKEN
$ vault token revoke <token>
$ vault token revoke -accessor <accessor-token>
```

# VAULT LEASE
```shell
# LEASE RENEW
$ vault lease renew -increment=300 <lease-id>

# LEASE REVOKE
$ vault lease revoke <lease-id>
$ vault lease revoke -prefix aws/
```

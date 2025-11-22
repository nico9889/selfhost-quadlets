# Vaultwarden

These quadlets are used to self-host Vaultwarden.


Before starting these quadlets, three secrets need to be created:

```bash
openssl rand -base64 32 | tr -d "\n" | podman secret create vw_postgres_password -
echo "postgres://vaultwarden:$(podman secret inspect --showsecret --format '{{.SecretData}}' postgres_password)@vaultwarden-db/vaultwarden" | tr -d '\n' | podman secret create vw_database_url -
openssl rand -base64 32 | tr -d "\n" | podman secret create tandoor-secret-key -

# Not recommended
echo -n "YOUR_SECRET_PASSWORD" | argon2 "$(openssl rand -base64 32)" -e -id -k 65540 -t 3 -p 4| tr -d '\n' | podman secret create vw_admin_token - 
# ^^^
```

It's probably better, for the third secret, to write your password inside a temporary file, and then use this command instead:

```bash
cat YOUR_TEMP_FILE | argon2 "$(openssl rand -base64 32)" -e -id -k 65540 -t 3 -p 4| tr -d '\n' | podman secret create admin_token -
```

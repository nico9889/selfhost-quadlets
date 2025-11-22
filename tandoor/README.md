# Tandoor

These quadlets are used to self-host Tandoor Recipes.

Before starting these quadlets, two secrets need to be created:

```bash
openssl rand -base64 32 | tr -d "\n" | podman secret create tandoor-postgres-password -
openssl rand -base64 32 | tr -d "\n" | podman secret create tandoor-secret-key -
```

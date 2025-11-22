# Vikunja

These quadlets are used to self-host Vikunja.


Before starting these quadlets, three secrets need to be created:

```bash
openssl rand -base64 32 | tr -d "\n" | podman secret create vikunja-service-jwtsecret -
```

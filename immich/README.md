# Immich
These quadlets are used to self-host Immich.

Before starting these quadlets, a secret with the database password needs to be created:

```bash
openssl rand -base64 32 | tr -d "\n" | podman secret create immich_database_password -
```

If you want to bind mount a network drive to store your photos, and you are using AutoFS, you need the following parameters to set the loosen SELinux to permit Podman applications to access the folder

```bash
immich	-fstype=cifs,vers=3.0,rw,uid=1001,gid=1001,file_mode=0644,dir_mode=0770,credentials=/home/USER/.PASSWORD_FILE,iocharset=utf8,context=system_u:object_r:container_file_t:s0    ://YOUR_NAS_ADDRESS/SMB/PATH/TO/IMMICH/DATA
```

(Replace: USER, PASSWORD_FILE, YOUR_NAS_ADDRESS, /SMB/PATH/TO/IMMICH/DATA)

where the relevant part is:

```bash
context=system_u:object_r:container_file_t:s0
```

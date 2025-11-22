# Caddy
This quadlet starts a container to host Caddy and use it as a reverse proxy for self-hosted services.

The container builds from a custom image which contains Caddy with the extension to automate the Let's Encrypt DNS-0 Challenge using Cloudflare.

To create the image you need to save the Dockerfile somewhere, and change the working directory path accordingly inside the `caddy.build` file.

Before starting the container it's necessary to set the Cloudflare API Token, with DNS Edit capabilities, as a secret:

```bash
podman secret create caddy-cloudflare-key CLOUDFLARE_DNS_EDIT_TOKEN
```

After the first start, you may copy the Caddyfile outside from the container using:

```bash
podman copy caddy:/etc/caddy/Caddyfile ./Caddyfile
```

make the wanted changes, and copy it back inside the container reversing the command parameters.

You may need to make ports starting from 80 unprivileged, unless you change the Quadlet to use ports with a number >1024 and then traslate them with a NAT.

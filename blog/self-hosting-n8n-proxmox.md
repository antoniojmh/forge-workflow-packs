# How to Self-Host n8n on Proxmox

Running n8n on your own hardware gives full control over data and pipelines.

## Why Self-Host?
- Data never leaves your network
- No request limits
- Full control
- No monthly fees

## Quick Deploy
```bash
pct create 110 local:vztmpl/ubuntu-22.04-standard_22.04-1_amd64.tar.zst \
  --storage local-zfs --memory 2048 \
  --net0 name=eth0,bridge=vmbr0,ip=dhcp --onboot 1

pct exec 110 -- apt install -y docker.io docker-compose-v2
pct exec 110 -- mkdir -p /opt/n8n
# Add docker-compose.yml, then:
pct exec 110 -- docker compose up -d
```

## Docker Compose
```yaml
services:
  n8n:
    image: n8nio/n8n:latest
    ports:
      - '5678:5678'
    volumes:
      - ./n8n-data:/home/node/.n8n
    restart: unless-stopped
```

Visit http://your-ct-ip:5678 to start automating.

## More
For 1000+ ready-to-import workflows, check out the Forge Workflow Packs.

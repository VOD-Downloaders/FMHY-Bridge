# Configuration

The Docker container is configured through environment variables. The
recommended way to run is with Docker Compose:

```yaml
services:
  fmhy_bridge:
    image: ghcr.io/ggjorven/fmhy-bridge:latest
    container_name: fmhy_bridge
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
      - LOG_LEVEL=info
      - ENDPOINTS_PORT=3000
    ports:
      - 3000:3000
    restart: unless-stopped
```

```sh
docker compose up -d
```

## Runtime environment variables

These can be set via the `environment` block (or `-e`) at container start.

| Variable | Default | Description |
|---|---|---|
| `PUID` | `1000` | User ID the process drops privileges to. Set to match the host user owning mounted data |
| `PGID` | `1000` | Group ID the process drops privileges to |
| `TZ` | `UTC` | Timezone for the container (e.g. `Europe/Amsterdam`) |
| `LOG_LEVEL` | `info` | Log verbosity: `debug` / `info` / `warning` / `error`. `debug` (alias `trace`) enables trace logging |
| `ENDPOINTS_PORT` | `3000` | Port the API server listens on inside the container. Remember to map it in `ports` |

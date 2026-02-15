# Portainer Nextcloud

A Portainer-compatible Docker Compose stack template for deploying [Nextcloud](https://nextcloud.com/) with MariaDB and Redis.

## Stack Components

| Service | Image | Purpose |
|---------|-------|---------|
| Nextcloud | `nextcloud:latest` | Self-hosted productivity and file sync platform |
| MariaDB | `mariadb:lts` | Relational database backend |
| Redis | `redis:alpine` | In-memory cache for file locking and sessions |

## Prerequisites

- Docker Swarm mode enabled
- [Traefik](https://traefik.io/) deployed on the Swarm with:
  - `websecure` entrypoint (port 443)
  - `letsencrypt` certificate resolver configured
  - Connected to a shared overlay network (default: `traefik-public`)

## Quick Start

### Using Portainer

1. In Portainer, go to **Settings > App Templates**
2. Add the template URL:
   ```
   https://raw.githubusercontent.com/bhhaskin/portainer-nextcloud/main/template.json
   ```
3. Navigate to **App Templates**, find **Nextcloud**, fill in your environment variables, and deploy.

### Using Docker Compose

1. Clone the repository:
   ```bash
   git clone https://github.com/bhhaskin/portainer-nextcloud.git
   cd portainer-nextcloud
   ```

2. Copy the example environment file and edit it with your own values:
   ```bash
   cp .env.example .env
   ```

3. Start the stack:
   ```bash
   docker stack deploy -c docker-compose.yml nextcloud
   ```

4. Access Nextcloud at `https://cloud.example.com` (or your configured domain).

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `NEXTCLOUD_ADMIN_USER` | Nextcloud admin username | `admin` |
| `NEXTCLOUD_ADMIN_PASSWORD` | Nextcloud admin password | `admin_password` |
| `MYSQL_ROOT_PASSWORD` | MariaDB root password | `root_password` |
| `MYSQL_DATABASE` | Database name for Nextcloud | `nextcloud` |
| `MYSQL_USER` | Database user for Nextcloud | `nextcloud` |
| `MYSQL_PASSWORD` | Database user password | `nextcloud_password` |
| `REDIS_PASSWORD` | Redis instance password | `redis_password` |
| `NEXTCLOUD_DOMAIN` | Domain name for Nextcloud (Traefik routing & trusted domains) | `cloud.example.com` |
| `TRAEFIK_NETWORK` | External Docker network Traefik is connected to | `traefik-public` |

> **Note:** Change all default passwords before deploying to production.

## License

[MIT](LICENSE)

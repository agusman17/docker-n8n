# n8n Docker Quick Setup

A quick setup guide for running [n8n](https://n8n.io) using Docker Compose.

## Prerequisites

- [Docker Engine](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- Port `5678` available

## Quick Start

### 1. Clone or copy the project

Ensure `docker-compose.yml` is in your working directory.

### 2. Pull the latest image

```bash
docker compose pull
```

### 3. Start the container

```bash
docker compose up -d
```

### 4. Access n8n

Open your browser and navigate to:

```
http://localhost:5678
```

## Configuration

The `docker-compose.yml` mounts a local `./n8n-data` directory for persistent storage of workflows, credentials, and settings.

| Environment Variable        | Description                        |
|-----------------------------|------------------------------------|
| `N8N_HOST`                  | Hostname for n8n                   |
| `N8N_PORT`                  | Port for n8n                       |
| `N8N_PROTOCOL`              | Protocol (`http` or `https`)       |
| `N8N_SECURE_COOKIE`         | Enable secure cookies              |
| `NODE_TLS_REJECT_UNAUTHORIZED` | Allow self-signed certificates  |

## Managing the Container

| Command                          | Action                              |
|----------------------------------|-------------------------------------|
| `docker compose start`           | Start an existing container         |
| `docker compose stop`            | Stop the container                  |
| `docker compose restart`         | Restart the container               |
| `docker compose down`            | Stop and remove the container       |
| `docker compose logs -f`         | View live logs                      |

## Updating n8n

To update to the latest version:

```bash
# 1. Download the latest n8n docker image
docker compose pull

# 2. Stop and recreate the container using the new image
docker compose up -d

# 3. Clean up the old, unused image (optional)
docker image prune -f
```

> **Note:** As of this setup, the current stable version is **Version 2.43.5**.

## Data Persistence

All n8n data (workflows, credentials, execution history, settings) is stored in the local `./n8n-data` directory. To back up your data:

```bash
# Stop the container first
docker compose stop

# Copy the data directory
tar -czvf n8n-backup.tar.gz ./n8n-data
```

To restore from backup:

```bash
# Stop the container
docker compose stop

# Extract the backup
tar -xzvf n8n-backup.tar.gz

# Start the container
docker compose up -d
```

## File Structure

```
n8n-docker/
├── docker-compose.yml   # Docker Compose configuration
├── n8n-data/            # Persistent data directory (auto-created)
└── README.md            # This file
```

## Historical Stable Versions

Below is a historical record of recent stable versions:

| Version | Release Date |
|---------|-------------|
| 2.43.5  | Latest stable (current) |

To ensure you are running the latest stable version, follow the [Updating n8n](#updating-n8n) instructions above.

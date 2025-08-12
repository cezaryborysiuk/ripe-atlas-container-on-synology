# RIPE Atlas Probe on Synology NAS (Container Manager)

This repository provides a ready-to-use configuration file for deploying a **RIPE Atlas Software Probe** on a Synology NAS using **Container Manager**. The configuration is based on the [jamesits/ripe-atlas](https://github.com/Jamesits/docker-ripe-atlas) Docker image, allowing you to contribute to the [RIPE Atlas project](https://atlas.ripe.net/) directly from your NAS.

***

## Features

- **Quick deployment** of the RIPE Atlas software probe as a Docker container
- Designed for Synology's Container Manager with essential volume mounts and network settings
- Utilizes the **host network**
***

## Configuration

### 1. Environment Variables

You can control key aspects of the probe via environment variables:

| Variable         | Description                                   | Default     | Example                 |
|------------------|-----------------------------------------------|-------------|-------------------------|
| `TELNETD_PORT`   | Port used by Telnet daemon                    | `2023`      | `TELNETD_PORT=2023`     |
| `HTTP_POST_PORT` | Port for HTTP POST interface                  | `8080`      | `HTTP_POST_PORT=8080`   |
| `RXTXRPT`        | Enable RX/TX report (`yes` or `no`)           | `yes`       | `RXTXRPT=yes`           |

To override defaults, edit the relevant section in your Container Manager or adjust the `env_variables` entries:
```json
{
  "key": "HTTP_POST_PORT",
  "value": "2080"
}
```

### 2. Volume Bindings

Persistent data is mounted via volumes. You may customize the **host paths** to fit your storage preferences:

```json
{
  "host_volume_file": "/docker/ripe-atlas/atlas-probe-etc",
  "is_directory": true,
  "mount_point": "/etc/ripe-atlas",
  "type": "rw"
}
```

| Host Path                               | Container Mount Point        | Purpose                           |
|-----------------------------------------|------------------------------|-----------------------------------|
| `/docker/ripe-atlas/atlas-probe-etc`    | `/etc/ripe-atlas`            | Probe configuration files         |
| `/docker/ripe-atlas/atlas-probe-run`    | `/run/ripe-atlas`            | Runtime files                     |
| `/docker/ripe-atlas/atlas-probe-var`    | `/var/spool/ripe-atlas`      | Persistent probe data/spool files |

Modify host paths as needed; mount points must remain unchanged.

***

## Networking

- **Host Network Mode** is enabled

***

## Docker Image

- **Image:** [`jamesits/ripe-atlas:latest`](https://hub.docker.com/r/jamesits/ripe-atlas)

***

## Usage

1. **Import (`ripe-atlas.json`) to the Synology Container Manager**
2. **Container -> Action -> Import -> From local device**
3. **Deploy the container**

***

## References

- Docker Image and detailed documentation: [jamesits/docker-ripe-atlas](https://github.com/Jamesits/docker-ripe-atlas)
- RIPE Atlas Project: [atlas.ripe.net](https://atlas.ripe.net/)

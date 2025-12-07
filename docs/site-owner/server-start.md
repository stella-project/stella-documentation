Once the Docker Compose file is configured and all experimental systems are ready, the STELLA Server can be started by building and running the containers.


## Development Mode (Hot Reloading)

Development mode enables hot reloading and is recommended during local development and testing.

```bash
sudo docker compose -f docker-compose-dev.yml build
sudo docker compose -f docker-compose-dev.yml up -d
```

In this mode, local code changes are reflected immediately inside the running containers.

## Production-like Deployment

For a stable, production-style deployment without hot reloading, use:

```bash
sudo docker compose build
sudo docker compose up -d
```

This mode is intended for staged or production deployments.


## Expected Containers

A standard STELLA Server deployment starts several containers, including:

+ stella-server — Flask application service
Accessed internally and via reverse proxy (default: localhost:8000)
+ postgres — PostgreSQL database service
Default port: 5432
+ nginx — Reverse proxy and entrypoint
Default port: 80


Example output after starting containers in development mode:

```
CONTAINER ID   IMAGE                 COMMAND              PORTS                                         NAMES
3a2109cc6e0b   stella-dev-nginx       "/docker-entrypoint.…"     0.0.0.0:80->80/tcp                            stella-dev-nginx-1
2126e200ff8b   stella-dev-server      "flask run --host=0.…"    0.0.0.0:8000->8000/tcp                        stella-dev-server-1
f4d99530d31d   postgres:16            "docker-entrypoint.s…"    0.0.0.0:5432->5432/tcp                        stella-dev-db-server-1

```

## Container Names (Non-Development Mode)

When running without the development Compose file, container names follow the standard naming convention:

+ stella-nginx-1
+ stella-server-1
+ stella-db-server-1

These containers must all be running for the STELLA Server to operate correctly.




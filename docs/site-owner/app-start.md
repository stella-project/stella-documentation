Once the Docker Compose file is configured and all experimental systems are ready, the STELLA App can be started by building and running the containers.


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

A standard STELLA App deployment starts several containers, including:

+ stella-app — Flask application service
Accessed internally and via reverse proxy (default: localhost:8080)
+ postgres — PostgreSQL database service
Default port: 5430
+ all system containers


Example output after starting containers in development mode:

```
CONTAINER ID   IMAGE                                     COMMAND                     PORTS                                           NAMES
f630dda0536d   stella-dev-app                             "flask run --host=0.…"     0.0.0.0:8080->8000/tcp                         stella-dev-app-1
f4d99530d31d   postgres:16                               "docker-entrypoint.s…"     0.0.0.0:5430->5430/tcp                         stella-dev-db-app-1
0ac7ee6a1eb1   stella-dev-gesis_rank_pyserini_base       "/bin/sh -c 'python3…"                                                   gesis_rank_pyserini_base
c506ce89c5fa   stella-dev-gesis_rec_pyserini             "/bin/sh -c 'python3…"                                                   gesis_rec_pyserini
fb4eb14c69a4   stella-dev-gesis_rec_pyterrier            "/bin/sh -c 'python3…"                                                   gesis_rec_pyterrier
989e34cff880   stella-dev-gesis_rank_pyserini            "/bin/sh -c 'python3…"                                                   gesis_rank_pyserini
```

## Container Names (Non-Development Mode)

When running without the development Compose file, container names follow the standard naming convention:

+ stella-app-1
+ stella-db-app-1

These containers must all be running for the STELLA App to operate correctly.




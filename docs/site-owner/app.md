# STELLA App Setup


This documents the STELLA App codebase, deployment workflows and runtime behavior.

It is intended for developers, system integrators and portal partners who deploy the STELLA App to conduct Information Retrieval (IR) and recommender system experiments.

This documentation focuses on how to configure, run and interact with the STELLA App, once experimental systems are implemented and runnable independently.


## Documentation Structure

Use the following sections as a guided workflow. Each item links to a dedicated document with details and references.

1. [Docker Compose Configuration](../site-owner/app-docker-setup.md)
2. [Environment Variables](../site-owner/app-env.md)
3. [Database Initialization](../site-owner/app-init-db.md)
4. [Endpoints and API Usage](../site-owner/app-api.md)
5. [REST API Documentation](../site-owner/app-mca.md)
5. [Database Schema and Models](../site-owner/app-database-schema.md)

---

### Getting Started

Clone the STELLA App repository from GitHub:

```bash
git clone https://github.com/stella-project/stella-app.git
cd stella-app
```

Development Mode (Hot Reloading)

```
sudo docker compose -f docker-compose-dev.yml up
```

Production-like Deployment

```
sudo docker compose -f docker-compose.yml
```

Expected Containers
A standard deployment starts several containers, including:

+ stella-app — application service (localhost:8000)
+ postgres — database service (localhost:5430)
+ one container per experimental system (ranker or recommender)



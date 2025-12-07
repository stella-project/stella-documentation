# STELLA Server Setup


This documents the STELLA Server codebase, deployment workflows and runtime behavior.

It is intended for developers, system integrators and portal partners who deploy the STELLA Server to conduct Information Retrieval (IR) and recommender system experiments.

This documentation focuses on how to configure, run and interact with the STELLA Server, once experimental systems are implemented and runnable independently.


## Documentation Structure

Use the following sections as a guided workflow. Each item links to a dedicated document with details and references.

1. [Docker Compose Configuration](../site-owner/server-docker-setup.md)
2. [Environment Variables](../site-owner/server-env.md)
3. [Database Initialization](../site-owner/server-init-db.md)
4. [Endpoints and API Usage](../site-owner/server-api.md)
5. [REST API Documentation](../site-owner/server-mca.md)
5. [Database Schema and Models](../site-owner/server-database-schema.md)

---

### Getting Started

Clone the STELLA Server repository from GitHub:

```bash
git clone https://github.com/stella-project/stella-server.git
cd stella-server
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

+ stella-server — application service (localhost:8080)
+ postgres — database service (localhost:5432)




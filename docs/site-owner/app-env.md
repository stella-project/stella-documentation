# STELLA App Environment Variables

This document provides a complete reference for all environment variables used by the STELLA App.  

These variables control application configuration, experiment execution, system setup, server communication and database connectivity.

All environment variables documented here are defined in the STELLA App `docker-compose.yml` and `docker-compose-dev.yml` files.  

Unless explicitly stated otherwise, the same variables apply to both development and production deployments.

---


| Environment variable | Meaning |
| --- | --- |
| FLASK_APP | Entry point of the Flask application. Points to `app/app`, which contains the STELLA App initialization logic. |
| FLASK_CONFIG | Flask configuration profile. The value `postgres` enables PostgreSQL-backed configuration. |
| DEBUG | Enables Flask debug mode and automatic reloading. Should only be enabled in development. |
| INTERLEAVE | Enables interleaving of experimental results with the baseline system. Default is `True`. |
| BULK_INDEX | If `True`, all systems start indexing automatically on app startup. If `False`, systems must be indexed manually via the REST API or UI. |
| INTERVAL_DB_CHECK | Time interval in seconds for checking the database for completed sessions that can be sent to the STELLA Server. |
| SESSION_EXPIRATION | Time in seconds after which an active session is automatically marked as finished. |
| SESSION_KILL | Maximum lifetime of a session in seconds. After this time, the session is forcefully terminated. This variable is optional. |
| SENDFEEDBACK | Enables or disables sending feedback data to the STELLA Server. |
| SYSTEMS_CONFIG | JSON configuration describing all experimental systems. Each system must define a type (`ranker` or `recommender`). One system per type must be marked as the baseline using `base: true`. |
| STELLA_SERVER_ADDRESS | Base URL of the STELLA Server used for submitting session and feedback data. |
| STELLA_SERVER_USER | Email or user identifier used to authenticate the STELLA App with the STELLA Server. |
| STELLA_SERVER_USERNAME | Username associated with the STELLA App identity on the STELLA Server. |
| STELLA_SERVER_PASS | Password used to authenticate the STELLA App with the STELLA Server. |
| POSTGRES_USER | Username for authenticating with the PostgreSQL database. |
| POSTGRES_PW | Password for authenticating with the PostgreSQL database. |
| POSTGRES_DB | Name of the PostgreSQL database used by the STELLA App. |
| POSTGRES_URL | Hostname and port of the PostgreSQL database service (e.g. `db-app:5430`). |

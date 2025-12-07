# STELLA Server Environment Variables

This document provides a complete reference for all environment variables used by the STELLA Server.  

These variables control application configuration, experiment execution, system setup, server communication and database connectivity.

All environment variables documented here are defined in the STELLA App `docker-compose.yml` and `docker-compose-dev.yml` files.  

Unless explicitly stated otherwise, the same variables apply to both development and production deployments.


## Application Configuration

| Environment Variable | Meaning |
|---------------------|---------|
| `FLASK_APP` | Flask application entry point. Specifies the import path of the server application. |
| `FLASK_CONFIG` | Selects the runtime configuration profile. The value `postgres` enables PostgreSQL-backed configuration. |
| `SECRET_KEY` | Secret key used by Flask for session signing and security-related features. Must be changed in production. |

---

## Account and Authentication Configuration

The STELLA Server manages multiple roles with dedicated credentials. These are used for authentication between STELLA components and for administrative access.

| Environment Variable | Meaning |
|---------------------|---------|
| `ADMIN_MAIL` | Email address for the administrator account. |
| `ADMIN_PASS` | Password for the administrator account. |
| `SITE_MAIL` | Email address used by site-level STELLA App instances to authenticate with the server. |
| `SITE_PASS` | Password associated with the site account. |
| `EXPERIMENTER_MAIL` | Email address for experimenter users. |
| `EXPERIMENTER_PASS` | Password for the experimenter account. |

---

## Database Configuration

These variables define how the STELLA Server connects to its PostgreSQL database.

| Environment Variable | Meaning |
|---------------------|---------|
| `POSTGRES_USER` | Username used to authenticate with the PostgreSQL database. |
| `POSTGRES_PW` | Password for the PostgreSQL user. |
| `POSTGRES_DB` | Name of the PostgreSQL database used by the STELLA Server. |
| `POSTGRES_URL` | Hostname and port of the PostgreSQL service in the Docker network (e.g. `db-server:5432`). |

---

## Notes

- This configuration is intended for **development use** and enables hot reloading.
- All credentials shown here must be replaced with secure values in production deployments.
- The database service (`db-server`) runs inside the same Docker network and is not exposed externally except via port mapping for local development.
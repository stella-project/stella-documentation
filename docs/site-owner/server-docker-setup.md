The STELLA Server is also primarily configured via **Docker Compose**  and a set of environment variables.

Both configuration and runtime behavior are controlled through the `docker-compose.yml` files provided in the repository.

---

> **Important**
>
> Two Docker Compose files are provided:
>
> - `docker-compose.yml` — standard deployment
> - `docker-compose-dev.yml` — development deployment with hot reloading
>
> The **same environment variables** are used by both files.  
> The choice of file only affects developer ergonomics (e.g. local code reloads), not system behavior or configuration semantics.


## Setting up Credentials

Make sure to change the username and passwords in the Dockerfile for the following env variables:

**Important Security Notice**

Before deploying the STELLA Server in any environment, **you must change the default usernames and passwords** defined for the following environment variables. The provided values are placeholders and are **not safe for production use**.

| Environment Variable        | Description                                      |
|----------------------------|--------------------------------------------------|
| `ADMIN_MAIL`               | Email address for the administrator account       |
| `ADMIN_PASS`               | Password for the administrator account            |
| `SITE_MAIL`                | Email address for the site account                 |
| `SITE_PASS`                | Password for the site account                      |
| `EXPERIMENTER_MAIL`        | Email address for the experimenter account         |
| `EXPERIMENTER_PASS`        | Password for the experimenter account              |

These credentials are used to initialize user accounts in the STELLA system.  
Replace all default values in the Dockerfile or Docker Compose configuration **before starting the containers** to prevent unauthorized access.


## Full Docker Compose Reference

The complete Docker Compose configuration is included directly from the repository:

```yaml
--8<-- "server/docker-compose.yml"
```
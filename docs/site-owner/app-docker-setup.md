The STELLA App is primarily configured via **Docker Compose**  and a set of environment variables.

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

---

## System Configuration (`SYSTEMS_CONFIG`)

Each experimental system must be declared explicitly in the `SYSTEMS_CONFIG` environment variable within the Docker Compose configuration.


```yaml
SYSTEMS_CONFIG: |
{
    "gesis_rec_pyserini": {"type": "recommender"},
    "gesis_rec_pyterrier": {"type": "recommender", "base": true},
    "gesis_rank_pyserini": {"type": "ranker"},
    "gesis_rank_pyserini_base": {"type": "ranker", "base": true}
}

```


Configuration rules:

+ each system runs as an independent service
+ exactly one system per task should be marked as the `"base"` system
+ supported system types are `ranker` and `recommender`


## Full Docker Compose Reference

The complete Docker Compose configuration is included directly from the repository:

```yaml
--8<-- "app/docker-compose.yml"
```
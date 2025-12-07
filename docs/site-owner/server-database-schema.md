The STELLA Server also uses a relational database schema to track:


- **roles** – Defines authorization roles that govern access and permissions within the system.

- **users** – Represents all authenticated actors, including administrators, sites, and participants.

- **sessions** – Captures individual experimental sessions, linking site users with selected ranking and recommendation systems.

- **results** – Stores the outputs of ranking and recommendation requests, including returned items and query metadata.

- **feedbacks** – Records user interaction data and evaluative signals for specific results.

- **systems** – Contains metadata and configuration details for experimental and baseline systems evaluated in STELLA.

## Accessing the Database

To access the STELLA Server database, run the following command:

```bash
sudo docker exec -it stella-db-server /bin/bash
```


Then connect to PostgreSQL: 

```
>> psql -h localhost -p 5432 -U postgres
```

You can now execute SQL queries directly against the database.


## Model Definitions
The model definitions are documented directly from the codebase:

::: server.web.app.models
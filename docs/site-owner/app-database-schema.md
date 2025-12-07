The STELLA App uses a relational database schema to track:


- **sessions** – Tracks user sessions and interactions during experiments.
- **results** – Stores search or recommendation results returned to users.
- **feedbacks** – Records user feedback on results.
- **systems** – Contains metadata about the experimental systems.

## Accessing the Database

To access the STELLA App database, run the following command:

```bash
sudo docker exec -it stella-db-app /bin/bash
```


Then connect to PostgreSQL: 

```
>> psql -h localhost -p 5430 -U postgres
```

You can now execute SQL queries directly against the database.


## Model Definitions
The model definitions are documented directly from the codebase:

::: app.web.app.models
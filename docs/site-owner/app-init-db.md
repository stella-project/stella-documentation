Once the containers are running, the STELLA App database must be initialized before the application can be used.

The initialization process creates the required database schema and populates the database with initial data.


## Initialize and Seed the Database

Run the following commands to initialize and populate the database:

```bash
sudo docker exec -it stella-dev-app-1 flask init-db
sudo docker exec -it stella-dev-app-1 flask seed-db
```


## Command Implementation

The database initialization and seeding logic is implemented in the following module:

::: app.web.app.commands


## Application Entry Point (Reference)

For context, the Flask application entry point used by these commands is defined here:

::: app.web.app.app

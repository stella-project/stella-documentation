# Setup for Local Developments

This guide walks you through how the STELLA infrastructure can be setup locally on one single machine for development and testing purposes.

For local development, we recommend using the docker compose files with a `dev` suffix. They mount the local directory containing the source code and run the applications with hot reloading. By that, the applications can directly be modified while also connect to other applications in the docker network.

## 1. Clone Repositories and Dataset
We will clone the `stella-app`, `stella-server`, and the `stella-search` repositories. All experimental containers will be automatically pulled by the stella-app compose file.

```bash
gh repo clone stella-project/stella-app
```

```bash
gh repo clone stella-project/stella-server
```

```bash
gh repo clone stella-project/stella-search
```

Additionally we need to add a dataset that should be searched through. In this example, we download the data from this [link](https://th-koeln.sciebo.de/s/OBm0NLEwz1RYl9N?path=%2F). However, any other dataset can be used as long as it matches the indexing pipelines in the experimental systems.

After downloading the dataset, it needs to be extracted and placed into the directories.
```bash
tar -xf ~/Downloads/gesis-search.tar  

cp gesis-search/documents/publication.jsonl stella-search/data/index 

cp -r gesis-search stella-app/data/
```



## 2. Start Stella-Server
Now we can start the stella server. If you prefer to run the stella-app without the stella-server, you can skip this step.

To start the stella-server, we navigate into the `stella-server` directory and run the compose stack:
```bash
docker compose -f docker-compose-dev.yml
``` 

After the stella-server compose stack is running and no errors appear in the logs, its database need to be initiated. Therefore we login to the docker container and run a flask cli command that creates all tables:
```bash
docker exec -it stella-dev-server-1 flask init-db
```

Now we can additionally run a command that fills the tables with the systems and users that are defines in the compose stack:
```bash
docker exec -it stella-dev-server-1 flask seed-db
```

A good validation if this was successful is to check if the expected systems and users are created in the database.


## 3. Start Stella-App
If the stella-app is run without the stella-server, the stella-app compose stack needs to be modified accordingly. Especially the cron service that copies data between the two databases and the docker network needs to be modified.

!!! Warning

    At the first startup, the cron service might log some errors because the stella-app database is not initialized yet. This is expected but should be resolved after initializing the database.


Like before, we initialize the database of for the stella-app:
```bash
docker exec -it stella-dev-server-1 flask init-db
```
and also:
```bash
docker exec -it stella-dev-server-1 flask seed-db
```

## 4. Index Experimental Systems
After the stella-app and the stella-server is running, we need to index the dataset if the stella-app is not configured to index the data on startup. The systems are specified in the stella-app docker compose stack and should run by now. To trigger the indexing, the stella-app user interface at [localhost:8080](localhost:8080) can be used. 


## 5. Start Stella-Search
Stella search mimics the search service the stella-app is deployed to. Like the other container it can be started by navigating to the stella-search directory and running
```bash
docker compose up
```

The system should start and shortly after report that 110420 and 99541 documents were indexed from two directories.

Now everything is ready and the system can be used.

## 6. Running an Experiment
To test the setup, we can issue a query in the front end and explore some results. The clicks are logged by stella-search, send over to the stella-app, and then transfered to the stella-server where we can see the results on the dashboard. 




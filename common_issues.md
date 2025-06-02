:q
:q
### Docker Network Error
When the docker compose stack is started this error occurs:

!!! failure
    ```bash
    network stella-shared declared as external, but could not be found
    ```

Solution:
All container need to be in the same docker network. This network is created by the stella-server. If you run the stella-app without the stella-server or renamed the network, these changes need to be propagated to all other compose stacks.

### Cron Job Error
The stella-app logs repeatably errors like this:

!!! failure
    ```bash
    Job "update_server (trigger: interval[0:00:03], next run at: 2025-06-02 10:16:25 UTC)" raised an exception
    ```

This is most likely related to the scheduler job that transfers the data between the stella-app and the stella-server.

Solution:
Ensure that the both databases are initialized correctly, that the required systems are available and that their IDs align. Also make sure that the addresses and ports are correctly referenced and that all container are in the same network.

### So Results in the Frontend
The stella-search returns no results for a query and the stella-app logs this error:

!!! failure
    ```bash
    File "/app/app/services/ranking_service.py", line 40, in extract_hits
        if isinstance(hits[0], dict):
    IndexError: list index out of range
    ```

This can happen if the query does not match the dataset. Try a query like `arbeit`.
If this still happens, the experimental systems might not be indexed correctly. Please repeat the indexing.

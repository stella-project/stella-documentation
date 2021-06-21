| Environment variable | Meaning |
| --- | --- |
| RANKSYS_LIST | | 
| RANKSYS_PRECOM_LIST | | 
| RANKSYS_BASE | | 
| STELLA_SERVER_ADDRESS | | 
| STELLA_SERVER_USER | | 
| STELLA_SERVER_PASS | | 
| STELLA_SERVER_USERNAME | | 
| INTERLEAVE | You can choose to interleave the results with the baseline system via `INTERLEAVE`. Per default interleaving is activated (`INTERLEAVE=True`) | 
| BULK_INDEX | If all systems should start the indexing when launching the app leave `BULK_INDEX=True`. If `BULK_INDEX=False`, you can visit `<ip-of-stella-app>/` and index the systems individually or by calling the corresponding REST-endpoints. | 
| DELETE_SENT_SESSION | If `DELETE_SENT_SESSION=True`, all sessions will removed after they have been sent to the `stella-server`. | 
| INTERVAL_DB_CHECK | This environment variables controls the time interval for checking the database for finished sessions. Time is specified in seconds, i.e. `INTERVAL_DB_CHECK=3` will check every 3 seconds if there are new sessions that can be sent to the `stella-server`. | 
| SESSION_EXPIRATION | This environment variables controls the time interval after the state of a sessions will automatically be set to "finished". Time is specified in seconds, i.e. `SESSION_EXPIRATION=6` will make a session expire after 6 seconds. | 
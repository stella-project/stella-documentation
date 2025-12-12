
# STELLA App-Server Communication

This section documents how the STELLA App communicates with the STELLA Server, what data is stored on each side, how feedback is transferred and which configuration options control this behavior. The goal is to make the lifecycle of sessions, feedback and results explicit from an infrastructure and design perspective.

## Architectural Roles

STELLA App

+ Deployed at partner sites
+ Interfaces directly with the user-facing portal
+ Executes experimental ranking/recommendation systems
+ Collects user interactions and feedback
+ Temporarily stores sessions, feedback, and results locally
+ Periodically forwards completed data to the STELLA Server

STELLA Server

+ Acts as the central aggregation and persistence layer
+ Stores finalized experiment data across all sites
+ Manages users, sites, systems and long-term logs
+ Provides dashboards and analytics


## Data Ownership and Storage

Stored in the STELLA App

The STELLA App maintains a local postgres database containing:

+ Sessions – User interaction periods at a site
+ Feedback – Clicks and interaction signals per session
+ Results – Rankings or recommendations shown to users
+ Systems – Locally registered experimental systems (mirrors server-side systems for execution)


Stored in the STELLA Server

The STELLA Server permanently stores:

+ Sessions (metadata only)
+ Feedback records
+ Rankings and recommendation results
+ Site, user, and system identifiers

Once data is successfully transferred, it can optionally be deleted from the STELLA App database. This can be configured using the `SESSION_KILL` ENV variable which is an optional variable which can be set to a value (in seconds) or left to None if no data should be deleted from the app (although it is recommended that the data be transfered to the server.)


## Session Lifecycle (High-Level)

1. Session starts

    + User interacts with the portal
    + STELLA App creates a local Session

2. Results served

    + Ranking/recommendation systems return result lists
    + Results are stored locally and linked to sessions

3. User interactions

    + Each click is sent from the portal to the STELLA App as a JSON object (payload)
    + Feedback is immediately persisted locally

4. Session expiration

    + Sessions expire based on timeouts
    + Completion is inferred from whether feedback contains results

5. Data forwarding

    + Completed sessions are sent to the STELLA Server asynchronously
    + Controlled via configuration (see below)


## Authentication and Token Management

Token Retrieval

The STELLA App authenticates with the STELLA Server using a token-based mechanism:

+ Credentials (`STELLA_SERVER_USER`, `STELLA_SERVER_PASS`) are used to request a token via:

```
POST /tokens
```

The response includes:

+ `token`
+ `expiration` (in seconds)

The App:

+ Stores the token in memory
+ Refreshes it automatically 5 minutes before expiration

Token refresh is handled in  `update_token()`.

::: app.web.app.services.cron_service.update_token

## Site Identification

Before posting any data, the STELLA App resolves its site identifier:

```
GET /sites/{STELLA_SERVER_USERNAME}
```



## Posting Workflow to the STELLA Server

Once a session is marked as exited, the following sequence occurs:

### 1. Post Session

```
POST /sites/{site_id}/sessions
```

Sent data includes:

+ Site user identifier
+ Session start time
+ Ranking system name
+ Recommendation system name

The server returns a `session_id` used in all subsequent requests.


### 2. Post Feedback

For each feedback entry in the session:

```
POST /sessions/{session_id}/feedbacks
```

Payload includes:

+ Start/end timestamps
+ Interleaving method (if any)
+ Click data (JSON)

The server responds with a feedback_id.


### 3. Post Results

For each result associated with the feedback:

System ID is resolved remotely:

```
GET /system/id/{system_name}
```

Result data is then posted as either:

```
POST /feedbacks/{feedback_id}/rankings
POST /feedbacks/{feedback_id}/recommendations
```

Payload includes:

+ Query metadata
+ Paging details
+ Number of results
+ Serialized items list




## Periodic Execution (Cron-Based)

All communication is triggered by a scheduler-based cron service:

+ Periodically checks the local database
+ Updates session expiration
+ Refreshes authentication tokens
+ Sends completed sessions to the STELLA Server

::: app.web.app.services.cron_service.check_db_sessions


## Configuration and Control (via Docker Compose)

Several behaviors are controlled through environment variables in the STELLA App deployment:


| Variable               | Description                                                   | Values / Behavior |
|------------------------|---------------------------------------------------------------|-------------------|
| **SENDFEEDBACK**       | Controls whether sessions, feedback and results are sent to the STELLA Server | **True** → Send data to server<br>**False** → Keep all data local |
| **SESSION_EXPIRATION** | Time (in seconds) after which a session is considered expired | Numeric (seconds) |
| **SESSION_KILL**       | Optional hard timeout for incomplete sessions; triggers cleanup of partial data from STELLA App | Numeric (seconds), optional |
| **DELETE_SENT_SESSION**| Deletes local data after successful transfer                  | Enabled → Local copy removed |

## Feedback Handling

+ Queries without any associated feedback are **not** sent from the STELLA App to the STELLA Server.  

+ By default, each ranking or recommendation stored in the STELLA App database contains **three entries**, but only the **interleaved ranking** is transmitted to the server.

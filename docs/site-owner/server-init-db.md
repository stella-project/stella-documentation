Once the containers are running, the STELLA Server database must be initialized before the application can be used.

The initialization process creates the required database schema and populates the database with initial data.

## Setting up Roles and Systems

Before initializing the database, the experimental systems and default users must be registered in the application seed logic.

This is done in the `seed_db` function located in `web/app/commands.py`


### Step 1: Locate the `seed_db` Function

Open the `commands.py` file and find the `seed_db` function. This function is responsible for creating initial database entries such as roles, users and systems when the database is first initialized.

### Step 2: Define User Roles

Ensure that the required roles are created. STELLA distinguishes between administrators, site owners and experiment participants.

Add or verify the following role definitions inside `seed_db`:

```python
admin_role = Role(name="Admin")
participant_role = Role(name="Participant")
site_role = Role(name="Site")
```

### Step 3: Create Default Users

Next, define the initial users associated with each role. These users are created using credentials provided via environment variables. Fallback values are used only if the variables are not set.


```
user_site_a = User(
    username="site",
    email=os.environ.get("SITE_MAIL") or "site@stella-project.org",
    role=site_role,
    password=os.environ.get("SITE_PASS") or "pass",
)
```

Each user represents a specific actor in the STELLA ecosystem:

+ Admin users manage the overall platform
+ Participant users contribute experimental systems
+ Site users represent deployed STELLA App installations

### Step 4: Persist Roles and Users

Finally, add all created roles and users to the database session and commit them:

```
db.session.add_all(
    [
        admin_role,
        participant_role,
        site_role,
        user_admin,
        user_part_a,
        user_part_b,
        user_site_a,
    ]
)
```

These entries will be persisted when the database is initialized and seeded.

### Step 5: Register Experimental Systems

In addition to users and roles, the STELLA App requires all experimental systems (rankers and recommenders) to be registered in the database before the application can be used.

Each experimental system is represented by a `System` database model. A system typically defines:

- its operational status
- a unique system name
- the participant who contributed it
- its type (`RANK` or `REC`)
- how it was submitted (e.g. Docker-based)
- a reference URL to its implementation
- the site at which it is deployed
- the submission date

Example system definitions:

```python
# GESIS demo systems

gesis_rank_pyserini = System(
    status="running",
    name="gesis_rank_pyserini",
    participant_id=user_part_a.id,
    type="RANK",
    submitted="DOCKER",
    url="https://github.com/stella-project/gesis_rank_pyserini",
    site=user_site_a.id,
    submission_date=datetime.date(2019, 6, 10),
)

gesis_rank_pyserini_base = System(
    status="running",
    name="gesis_rank_pyserini_base",
    participant_id=user_part_a.id,
    type="RANK",
    submitted="DOCKER",
    url="https://github.com/stella-project/gesis_rank_pyserini_base",
    site=user_site_a.id,
    submission_date=datetime.date(2019, 6, 10),
)

gesis_rec_pyserini = System(
    status="running",
    name="gesis_rec_pyserini",
    participant_id=user_part_a.id,
    type="REC",
    submitted="DOCKER",
    url="https://github.com/stella-project/gesis_rec_pyserini",
    site=user_site_a.id,
    submission_date=datetime.date(2019, 6, 10),
)

gesis_rec_pyterrier = System(
    status="running",
    name="gesis_rec_pyterrier",
    participant_id=user_part_a.id,
    type="REC",
    submitted="DOCKER",
    url="https://github.com/stella-project/gesis_rec_pyterrier",
    site=user_site_a.id,
    submission_date=datetime.date(2019, 6, 10),
)
```

Each system must have a unique name, as this identifier is later referenced by the STELLA App configuration (for example in `SYSTEMS_CONFIG`).


## Initialize and Seed the Database

Run the following commands to initialize and populate the database:

```bash
sudo docker exec -it stella-dev-server-1 flask init-db
sudo docker exec -it stella-dev-server-1 flask seed-db
```


## Command Implementation

The database initialization and seeding logic is implemented in the following module:

::: server.web.app.commands


## Application Entry Point (Reference)

For context, the Flask application entry point used by these commands is defined here:

::: app.web.app.app

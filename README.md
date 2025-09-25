# Spanner Graph User360 Chatbot

## Let's create our tables

### Make sure we can connect to the database

```bash
gcloud alpha spanner cli ${GOOGLE_SPANNER_DB}  --instance=${GOOGLE_SPANNER_INSTANCE}  --project=${GOOGLE_CLOUD_PROJECT}
Welcome to Spanner-Cli Client.

Type 'help' or '\h' for help.
Type 'exit' or 'quit' or '\q' to exit.

spanner-cli> SELECT 1;
+---+
|   |
+---+
| 1 |
+---+
1 rows in set (9.04 msecs)

spanner-cli> quit
Bye...
```

### Load our Schema

```bash
gcloud alpha spanner cli ${GOOGLE_SPANNER_DB}  --instance=${GOOGLE_SPANNER_INSTANCE}  --project=${GOOGLE_CLOUD_PROJECT} < UserIdentityDB.sql
```


## Let's load all of our data

```bash
uv run load_data.py
```

## Run the agent

### Download and run the MCP Toolbox

```bash
cd Agent
make gettoolbox
make runtoolbox &

### Run the Agent

```bash
uv run adk web --host=0.0.0.0
```
```


## Feel free to run some sample queries in Spanner Studio

[Queries](./SampleQueries.md)

# Spanner Graph User360 Chatbot

## Clone the Repo

```bash
git clone https://github.com/maguec/SkeletonLab-SpannerGraphUser360Chatbot.git
cd SkeletonLab-SpannerGraphUser360Chatbot
```

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
```

### Run the Agent

```bash
uv run adk web --host=0.0.0.0
```


## Try the following script on the Chatbot
[Chatbot](./SampleScript.md)

## Feel free to run some sample queries in Spanner Studio

[Queries](./SampleQueries.md)

## Task

Add a new feature to the chatbot

Wrap the following sample hybrid query to the tools.yaml file, restart the bot and find the top 5 suspect emails and zip codes.

```sql
GRAPH UserIdentity MATCH (e:Email)-[:EMAIL_HAS_CC]->(c:CC) WHERE c.id IN (SELECT id from CC where sus=1) RETURN e.email as Email, c.zip as Zip;
```

hints:
- restart the ADK web
- no parameters are required
- ask the LLM to parse the data to build the report

# Spanner Graph User360 Chatbot

## Let's create our tables

```bash
gcloud alpha spanner cli ${GOOGLE_SPANNER_DB}  --instance=${GOOGLE_SPANNER_INSTANCE}  --project=${GOOGLE_CLOUD_PROJECT} < UserIdentityDB.sql
```


## Let's load all of our data

```bash
uv run load_data.py
```


## Feel free to run some sample queries in Spanner Studio

[Queries](./SampleQueries.md)

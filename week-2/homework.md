# Question 1. Load January 2020 data

```console
09:20:38.224 | INFO    | Task run 'clean-b9fd7e03-0' - rows: 447770
09:20:38.339 | INFO    | Task run 'clean-b9fd7e03-0' - Finished in state Completed()
```

# Question 2. Scheduling with Cron 
```console
prefect deployment build flows/02_gcp/etl_web_to_gcs.py:etl_web_to_gcs -n etl-homework --cron "0 5 1 * *" -a
```

# Question 3. Loading data to BigQuery

```console
Finished in state Completed()
05:19:58 PM
write_bq-f3b17cf5-1

Rows processed was: 14851920
05:19:58 PM

Finished in state Completed('All states completed.')
05:19:58 PM
```

[Code]()

# Question 4

```console

```

# Question 5

```console

```

# Question 6

```console

```

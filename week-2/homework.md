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
17:19:58.054 | INFO    | Task run 'write_bq-f3b17cf5-1' - Finished in state Completed()
17:19:58.060 | INFO    | Flow run 'fabulous-bustard' - Rows processed was: 14851920
17:19:58.213 | INFO    | Flow run 'fabulous-bustard' - Finished in state Completed('All states completed.')
17:19:59.525 | INFO    | prefect.infrastructure.process - Process 'fabulous-bustard' exited cleanly.
```

[Code](https://github.com/ronateds/data-engineering-zoomcamp-homework/blob/main/code/flows/02_gcp/etl_gcs_to_bq_no_transform.py)

# Question 4. Github Storage Block

```console
18:26:17.927 | INFO    | Task run 'clean-2c6af9f6-0' - rows: 88605
18:26:18.062 | INFO    | Task run 'clean-2c6af9f6-0' - Finished in state Completed()
```

[code](https://github.com/ronateds/data-engineering-zoomcamp-homework/blob/main/code/flows/02_gcp/etl_web_to_gcs_git.py)

# Question 5

```console

```

# Question 6

```console

```

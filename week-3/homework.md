My answers for the [homework 3](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2023/week_3_data_warehouse/homework.md) 

# Question 1:

Query:
```sql
SELECT count(*) FROM `direct-outlet-375818.nytaxi.fhv_tripdata`
```

Result in JSON: 
```json
[{
  "f0_": "43244696"
}]
```

# Question 2

Write a query to count the distinct number of affiliated_base_number for the entire dataset on both the tables.
What is the estimated amount of data that will be read when this query is executed on the External Table and the Table?

Query:
```sql
-- count the distinct number of Affiliated_base_number for external table
SELECT COUNT(DISTINCT(Affiliated_base_number)) FROM `direct-outlet-375818.nytaxi.fhv_tripdata_external`;

-- count the distinct number of Affiliated_base_number for non-partitioned table
SELECT COUNT(DISTINCT(Affiliated_base_number)) FROM `direct-outlet-375818.nytaxi.fhv_tripdata_non_partitioned`;
```

Preview: 0 MB for external and 317.94 MB for non-partitioned table

# Question 3

Query:
```sql
-- records that have both a blank (null) PUlocationID and DOlocationID in the entire dataset
SELECT count(*) FROM `direct-outlet-375818.nytaxi.fhv_tripdata_non_partitioned`
WHERE PUlocationID IS NULL AND DOlocationID IS NULL;
```

Result in JSON:
```json
[{
  "f0_": "717748"
}]
```

My answers for the [homework 3](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2023/week_3_data_warehouse/homework.md) 

## Question 1:

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

## Question 2

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

## Question 3

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

## Question 4

What is the best strategy to optimize the table if query always filter by pickup_datetime and order by affiliated_base_number?

For this question I've created the two first tables, the last two were not possible to create, and then I created a select query for each table and compared them with a query on the non-partitioned table.

```sql
-- Create a clustered table from external table
CREATE OR REPLACE TABLE `direct-outlet-375818.nytaxi.fhv_tripdata_clustered`
CLUSTER BY pickup_datetime, Affiliated_base_number AS
SELECT * FROM `direct-outlet-375818.nytaxi.fhv_tripdata_external`;

-- Create a partitioned and clustered table from external table
CREATE OR REPLACE TABLE `direct-outlet-375818.nytaxi.fhv_tripdata_partitioned_clustered`
PARTITION BY date(pickup_datetime)
CLUSTER BY Affiliated_base_number AS
SELECT * FROM `direct-outlet-375818.nytaxi.fhv_tripdata_external`;

-- select from the unpartitioned table
SELECT pickup_datetime, Affiliated_base_number
FROM `direct-outlet-375818.nytaxi.fhv_tripdata_non_partitioned`
WHERE pickup_datetime = '2019-03-31'
ORDER BY Affiliated_base_number;
-- estimates 647.87 MB

-- select from the clustered table
SELECT pickup_datetime, Affiliated_base_number
FROM `direct-outlet-375818.nytaxi.fhv_tripdata_clustered`
WHERE pickup_datetime = '2019-03-31'
ORDER BY Affiliated_base_number;
-- estimates 647.87 MB

-- select from the partitioned and clustered table
SELECT pickup_datetime, Affiliated_base_number
FROM `direct-outlet-375818.nytaxi.fhv_tripdata_partitioned_clustered`
WHERE pickup_datetime = '2019-03-31'
ORDER BY Affiliated_base_number;
-- estimates 608.12 KB
```

The best strategy to optimize the table is to partition by pickup_datetime and cluster on affiliated_base_number, as will take only 608.12 KB to process the query, compared with 647.87 MB from the other two queries.

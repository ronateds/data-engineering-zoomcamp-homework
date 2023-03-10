## Week 1 Homework

My week 1 [homework](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2023/week_1_docker_sql/homework.md)

## Question 1. Knowing docker tags

```console
~ docker build --help | grep "Write the image ID to the file"
      --iidfile string          Write the image ID to the file
```

## Question 2. Understanding docker first run

```console
~ docker run -it --entrypoint=bash python:3.9
root@a112498ca1dd:/# pip list
Package    Version
---------- -------
pip        22.0.4
setuptools 58.1.0
wheel      0.38.4
```

## Question 3. Count records 

```console
root@localhost:ny_taxi>
 SELECT
     count(1)
 FROM
     green_taxi_trips
 WHERE
    CAST(lpep_pickup_datetime as DATE) = '2019-01-15' AND
    CAST(lpep_dropoff_datetime as DATE) = '2019-01-15'
+-------+
| count |
|-------|
| 20530 |
+-------+
SELECT 1
Time: 0.253s
```

## Question 4. Largest trip for each day

```console
root@localhost:ny_taxi>
 SELECT
     CAST(lpep_pickup_datetime as DATE) as "day",
     EXTRACT(EPOCH FROM(lpep_dropoff_datetime - lpep_pickup_datetime)) as difference
 FROM
     green_taxi_trips
 WHERE
     CAST(lpep_pickup_datetime as DATE) = '2019-01-18' OR
     CAST(lpep_pickup_datetime as DATE) = '2019-01-28' OR
     CAST(lpep_pickup_datetime as DATE) = '2019-01-15' OR
     CAST(lpep_pickup_datetime as DATE) = '2019-01-10'
 ORDER BY "difference" DESC
 LIMIT 1;
+------------+------------+
| day        | difference |
|------------+------------|
| 2019-01-28 | 86389.0    |
+------------+------------+
SELECT 1
Time: 0.462s
```

The query above gives a wrong answer, the right one is bellow.

```console
root@localhost:ny_taxi>
 SELECT
     CAST(lpep_pickup_datetime as DATE) as date, MAX(trip_distance) as distance
 FROM
     green_taxi_trips
 GROUP BY CAST(lpep_pickup_datetime as DATE)
 ORDER BY distance DESC
 LIMIT 1
+------------+----------+
| date       | distance |
|------------+----------|
| 2019-01-15 | 117.99   |
+------------+----------+
SELECT 1
Time: 0.800s
```

## Question 5. The number of passengers


```console
root@localhost:ny_taxi>
 SELECT
     passenger_count as passengers,
     COUNT(1)
 FROM
     green_taxi_trips
 WHERE
     CAST(lpep_pickup_datetime as DATE) = '2019-01-01' AND
     (passenger_count = 3 OR passenger_count = 2)
 GROUP BY "passenger_count"
+------------+-------+
| passengers | count |
|------------+-------|
| 2          | 1282  |
| 3          | 254   |
+------------+-------+
SELECT 2
Time: 0.277s
```

## Question 6. Largest tip

```console
root@localhost:ny_taxi>
 SELECT
     zpu."Zone" as "pickup_zone",
     zdo."Zone" as "dropoff_zone",
     t."tip_amount"
 FROM
     green_taxi_trips t,
     zones zpu,
     zones zdo
 WHERE
     t."PULocationID" = zpu."LocationID" AND
     t."DOLocationID" = zdo."LocationID" AND
     zpu."Zone" = 'Astoria'
 ORDER BY t.tip_amount DESC
 LIMIT 1
+-------------+-------------------------------+------------+
| pickup_zone | dropoff_zone                  | tip_amount |
|-------------+-------------------------------+------------|
| Astoria     | Long Island City/Queens Plaza | 88.0       |
+-------------+-------------------------------+------------+
SELECT 1
Time: 0.294s
```

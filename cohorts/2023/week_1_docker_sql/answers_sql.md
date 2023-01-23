## Question 1. Knowing docker tags

Which tag has the following text? - *Write the image ID to the file*

- `--iidfile string`

```bash
docker build --help
```

## Question 2. Understanding docker first run

How many python packages/modules are installed?

- 3

```bash
docker run -it --entrypoint /bin/bash python:3.9
root@b07ad0314456:/# pip list
Package    Version
---------- -------
pip        22.0.4
setuptools 58.1.0
wheel      0.38.4
```

## Question 3. Count records

How many taxi trips were totally made on January 15?

- 20530

```sql
SELECT
	CAST(lpep_pickup_datetime AS DATE) AS pickup,
	CAST(lpep_dropoff_datetime AS DATE) AS dropoff,
	COUNT(1)
FROM
	green_taxi_data
WHERE
	(CAST(lpep_pickup_datetime AS DATE)='2019-01-15') AND
	(CAST(lpep_dropoff_datetime AS DATE)='2019-01-15')
GROUP BY
	pickup,
    dropoff
```

## Question 4. Largest trip for each day

Which was the day with the largest trip distance
Use the pick up time for your calculations.

- 2019-01-15

```sql
SELECT
	CAST(lpep_pickup_datetime AS DATE) AS pickup,
	trip_distance
FROM
	green_taxi_data
ORDER BY
	trip_distance DESC
LIMIT 100
```

## Question 5. The number of passengers

In 2019-01-01 how many trips had 2 and 3 passengers?

- 2: 1282 ; 3: 254

```sql
SELECT
	passenger_count,
	COUNT(1)
FROM
	green_taxi_data
WHERE
	CAST(lpep_pickup_datetime AS DATE)='2019-01-01'
GROUP BY
	passenger_count
```

## Question 6. Largest tip

For the passengers picked up in the Astoria Zone which was the drop off zone that had the largest tip?

- Long Island City/Queens Plaza

```sql
SELECT
	t."tip_amount",
	zpu."Zone" AS pickup,
	zdo."Zone" AS dropoff
FROM
	green_taxi_data t JOIN zones zpu
		ON t."PULocationID" = zpu."LocationID"
	JOIN zones zdo
		ON t."DOLocationID" = zdo."LocationID"
WHERE
	zpu."Zone" = 'Astoria'
ORDER BY
	tip_amount DESC
LIMIT 100
```


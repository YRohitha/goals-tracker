##### Attempted Solution
```
SELECT
  device_type, SUM(laptop_views) AS laptop_views, SUM(mobile_views) AS mobile_views
FROM
(SELECT
  device_type
  , CASE 
    WHEN device_type IN ('laptop') THEN COUNT(user_id)
  END AS laptop_views
  , CASE 
    WHEN device_type IN ('tablet', 'phone') THEN COUNT(user_id)
  END AS mobile_views
FROM 
  viewership
GROUP BY 1) views_per_device
GROUP BY 1
```

* `you are attempting to count the number of users based on different conditions (device_type being 'laptop' or 'tablet' or 'phone).
However, without a GROUP BY clause, the database system doesn't know how to group the data for these conditions.`
<img width="583" alt="Screenshot 2023-10-17 at 9 55 59 AM" src="https://github.com/YRohitha/goals-tracker/assets/22196915/5ba9f8a3-c704-49b2-b0cf-991cd858a9d8">

##### Correct Solution
```
SELECT
  SUM(CASE WHEN device_type = 'laptop' THEN 1 ELSE 0 END) AS laptop_views
  , SUM(CASE WHEN device_type IN ('tablet', 'phone') THEN 1 ELSE 0 END) AS mobile_views
FROM 
  viewership
```

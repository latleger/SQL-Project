<b>Question 1:</b> Is there a relationship between the amount time a someone is on the site and when they decide to make a purchase?

<b>SQL Queries:</b>


** review timeonsite and number of purchases
```<language-sql>
select
	timeonsite,
	productquantity,
	productprice,
	currencycode,
	city,
	country
from ALL_SESSIONS
wHERE PRODUCTQUANTITY > 0
GROUP BY
	timeonsite,
	productquantity,
	productprice,
	currencycode,
	city,
	country
ORDER BY 
	timeonsite desc,
	productquantity DESC
;
```
| timeonsite | productquantity | productprice | currencycode | city          | country       |
|------------|-----------------|--------------|--------------|---------------|---------------|
| 00:13:12   | 1               | 79.00        | USD          | Mountain View | United States |
| 00:11:47   | 1               | 249.00       | USD          | New York      | United States |
| 00:11:14   | 1               | 16.99        | USD          | Colombia      | Colombia      |
| 00:10:33   | 1               | 2.99         | USD          | United States | United States |
| 00:10:29   | 1               | 18.99        | USD          | Ann Arbor     | United States |
| 00:09:22   | 65              | 10.99        | USD          | United States | United States |
| 00:09:22   | 1               | 149.00       | USD          | San Francisco | United States |
| 00:09:05   | 4               | 11.20        | USD          | Atlanta       | United States |
| 00:09:04   | 1               | 55.99        | USD          | New York      | United States |
| 00:08:17   | 1               | 119.00       | USD          | Seattle       | United States |
| 00:07:18   | 1               | 119.00       | USD          | San Francisco | United States |
| 00:06:52   | 1               | 55.99        | USD          | United States | United States |
| 00:06:21   | 1               | 249.00       | USD          | Mountain View | United States |
| 00:06:09   | 1               | 16.99        | USD          | Bengaluru     | India         |
| 00:05:39   | 1               | 79.00        | USD          | United States | United States |
| 00:05:23   | 1               | 149.00       | USD          | United States | United States |
| 00:05:18   | 1               | 99.99        | USD          | Argentina     | Argentina     |
| 00:05:02   | 1               | 6.99         | USD          | Dallas        | United States |
| 00:04:49   | 1               | 10.99        | USD          | Canada        | Canada        |
| 00:04:49   | 1               | 16.99        | USD          | Mexico        | Mexico        |
| 00:04:08   | 1               | 18.99        | USD          | Columbus      | United States |
| 00:04:04   | 1               | 149.00       | USD          | Palo Alto     | United States |
| 00:03:22   | 1               | 17.49        | USD          | France        | France        |
| 00:03:13   | 1               | 59.99        | USD          | United States | United States |
| 00:03:03   | 1               | 149.00       | USD          | Mountain View | United States |
| 00:02:58   | 50              | 3.50         | USD          | United States | United States |
| 00:02:40   | 3               | 199.00       | USD          | United States | United States |
| 00:02:36   | 1               | 2.99         | USD          | Detroit       | United States |
| 00:02:30   | 1               | 13.59        | USD          | New York      | United States |
| 00:02:28   | 1               | 17.99        | USD          | Canada        | Canada        |
| 00:02:21   | 1               | 2.80         | USD          | Chicago       | United States |
| 00:02:20   | 1               | 10.99        | USD          | United States | United States |
| 00:02:14   | 1               | 15.99        | USD          | Mountain View | United States |
| 00:02:03   | 1               | 119.00       | USD          | Mountain View | United States |
| 00:01:48   | 10              | 8.99         | USD          | Madrid        | Spain         |
| 00:01:43   | 8               | 79.92        | USD          | Salem         | United States |
| 00:01:38   | 1               | 16.99        | USD          | New York      | United States |
| 00:01:35   | 1               | 99.99        | USD          | Dublin        | Ireland       |
| 00:01:28   | 1               | 16.99        | USD          | New York      | United States |
| 00:01:23   | 1               | 119.00       | USD          | Sunnyvale     | United States |
| 00:01:15   | 1               | 24.99        | USD          | United States | United States |
| 00:01:14   | 1               | 18.99        | USD          | Canada        | Canada        |
| 00:01:13   | 1               | 119.00       | USD          | United States | United States |
| 00:01:08   | 1               | 74.99        | USD          | Mountain View | United States |
| 00:01:03   | 1               | 199.00       | USD          | San Jose      | United States |
| 00:00:59   | 1               | 199.00       | USD          | Sunnyvale     | United States |
| 00:00:43   | 2               | 119.00       | USD          | New York      | United States |
| 00:00:33   | 1               | 24.99        | USD          | United States | United States |
| 00:00:33   | 1               | 51.99        | USD          | Los Angeles   | United States |
| 00:00:27   | 2               | 3.50         | USD          | Houston       | United States |
| 00:00:27   | 1               | 199.00       | USD          | United States | United States |
| 00:00:24   | 1               | 98.99        | USD          | Mountain View | United States |
| 00:00:18   | 1               | 1.99         | USD          | Finland       | Finland       |


** review the max and avg of timeofsite for all visitors
```<language-sql>
select
	max(timeonsite) AS max_timeonsite,
	avg(timeonsite) AS avg_timeonsite
from ALL_SESSIONS;
```
| max_timeonsite | avg_timeonsite  |
|----------------|-----------------|
| 00:47:01       | 00:01:59.450311 |


** all purchases have been under 15 mins, how many customers stay pass 15 mins?
```<language-sql>
WITH session_counts AS (
    SELECT
        CASE
            WHEN EXTRACT(MINUTE FROM timeonsite) < 15 THEN 'Less than 15 mins'
            ELSE 'More than 15 mins'
        END AS duration_category,
        COUNT(*) AS session_count
    FROM all_sessions
    GROUP BY duration_category
)
SELECT
    duration_category,
    session_count,
    round((session_count::numeric / SUM(session_count) OVER ()) * 100,2) AS percentage
FROM session_counts;
```
| duration_category | session_count | percentage |
|-------------------|---------------|------------|
| More than 15 mins | 224           | 1.48       |
| Less than 15 mins | 14910         | 98.52      |

 


<b>Answer:</b> All sales happened within 15 mins on being on the site. Based on our queries, we can see most visitors log off after 15 mins as well. Only about 1.5% of vistors stay over 15 mins, but as per the data, this does not result in sales. 

<br>
<br>

<b>Question 2:</b> Does as high orderquantity reflect in a high stocklevel?

<b>SQL Queries:</b>

```<language-sql>
SELECT
  reflects_stocklevel,
  COUNT(*) AS count
FROM (
  SELECT
    name,
    CASE
      WHEN avg_orderedquantity > avg_stocklevel THEN 'Yes'
      WHEN avg_orderedquantity < avg_stocklevel THEN 'No'
      ELSE 'Equal'
    END AS reflects_stocklevel
  FROM (
    SELECT
      name,
      AVG(orderedquantity) AS avg_orderedquantity,
      AVG(stocklevel) AS avg_stocklevel
    FROM products
    -- Group the data by relevant columns, such as product, category, etc.
    GROUP BY name
  ) AS subquery
) AS result
GROUP BY reflects_stocklevel;
```
| reflects_stocklevel | count |
|---------------------|-------|
| No                  | 284   |
| Yes                 | 12    |
| Equal               | 17    |


<b>Answer:</b> No, it does not.

<br>
<br>

<b>Question 3: </b> Does lead times reflect on stocklevels?

<b>SQL Queries: </b>

```<language-sql>
SELECT
  reflects_stock_level,
  COUNT(*) AS count
FROM (
  SELECT
    sku,
    name,
    ROUND(AVG(restockingleadtime), 0) AS avg_lead_time,
    ROUND(AVG(stocklevel), 0) AS avg_stock_level,
    CASE
      WHEN AVG(restockingleadtime) > AVG(stocklevel) THEN 'Yes'
      WHEN AVG(restockingleadtime) < AVG(stocklevel) THEN 'No'
      ELSE 'Equal'
    END AS reflects_stock_level
  FROM products
  GROUP BY
    sku,
    name
) AS subquery
GROUP BY
  reflects_stock_level;
```
| reflects_stock_level | count |
|----------------------|-------|
| No                   | 645   |
| Yes                  | 436   |
| Equal                | 11    |


Answer: No, it does not



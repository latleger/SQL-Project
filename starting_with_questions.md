Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:


```<language-SQL>
SELECT
	city, 
	country, 
	SUM(totaltransactionrevenue) AS total_transaction_revenue,
-- ranked by the SUM of the "total transaction revenue" in decending order
	RANK() OVER(
	ORDER BY SUM(totaltransactionrevenue) DESC) 
	AS rank
FROM 
	transactions
GROUP BY 
	city, 
	country
ORDER BY 
	rank
LIMIT 5;
```


<b>Answer:</b> The cities and country who have the highest level of transaction revenue on the site 
is Varying States, Mountain View, Salem, New York and Sunnyvale. All of the top 
cities are in the United States.


| city          | country       | total_transaction_revenue | rank |
|---------------|---------------|---------------------------|------|
| United States | United States | 2212.29                   | 1    |
| Mountain View | United States | 785.97                    | 2    |
| Salem         | United States | 639.36                    | 3    |
| New York      | United States | 590.56                    | 4    |
| Sunnyvale     | United States | 318.00                    | 5    |

<br>
<br>

**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

```<language-sql>
SELECT
	city,
	country, 
-- rounding the average quantity to a whole number
	ROUND(avg(productquantity),0) AS product_quantity
FROM transactions
GROUP BY 
	city, 
	country
ORDER BY 
	product_quantity DESC
LIMIT 10;
```

<b>Answer:</b> Visitors in Columbus, USA and Madrid, Spain buy an average of one item.




<br>
<br>

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

```<language-sql>
SELECT
	city,
	country, 
	v2productcategory,
	COUNT(v2productcategory) AS prod_cat
-- pulling data from products actually purchased by visitors
FROM (
	SELECT *
	FROM transactions
	WHERE productquantity > 0) AS prod_purchased
GROUP BY 
	city, 
	country,
	v2productcategory
ORDER BY 
	prod_cat DESC
LIMIT 25;
```

<b>Answer:</b> customers from the United States purchase more electrics than, those outside for the United States.

| city          | country       | v2productcategory                       | prod_cat |
|---------------|---------------|-----------------------------------------|----------|
| United States | United States | Home/Nest/Nest-USA/                     | 3        |
| Mountain View | United States | Home/Nest/Nest-USA/                     | 3        |
| United States | United States | Electronics                             | 2        |
| United States | United States | ${escCatTitle}                          | 2        |
| Canada        | Canada        | ${escCatTitle}                          | 1        |
| Canada        | Canada        | Home/Apparel/Kid's/Kids-Youth/          | 1        |
| Canada        | Canada        | Home/Shop by Brand/YouTube/             | 1        |
| Chicago       | United States | Lifestyle                               | 1        |
| Colombia      | Colombia      | Home/Apparel/Men's/Men's-T-Shirts/      | 1        |
| Columbus      | United States | (not set)                               | 1        |
| Dallas        | United States | Home/Shop by Brand/YouTube/             | 1        |
| Detroit       | United States | Drinkware                               | 1        |
| Dublin        | Ireland       | Home/Bags/                              | 1        |
| Finland       | Finland       | ${escCatTitle}                          | 1        |
| France        | France        | Headgear                                | 1        |
| Houston       | United States | ${escCatTitle}                          | 1        |
| Los Angeles   | United States | Home/Apparel/Men's/Men's-Outerwear/     | 1        |
| Madrid        | Spain         | ${escCatTitle}                          | 1        |
| Mexico        | Mexico        | (not set)                               | 1        |
| Mountain View | United States | ${escCatTitle}                          | 1        |
| Mountain View | United States | Apparel                                 | 1        |
| Mountain View | United States | Home/Apparel/Women's/Women's-Outerwear/ | 1        |
| Mountain View | United States | Nest-USA                                | 1        |
| New York      | United States | ${escCatTitle}                          | 1        |
| New York      | United States | (not set)                               | 1        |

<br>
<br>

**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

```<language-sql>
SELECT
-- ranks based on the sum of totaltransactionrevenue in decending order
	RANK() OVER(ORDER BY SUM(totaltransactionrevenue) DESC) AS rank,
	city, 
	country,
	v2productname,
	SUM(totaltransactionrevenue) AS prod_revenue
-- picks all rows with transactions over 0
FROM (
	SELECT *
	FROM transactions
	WHERE totaltransactionrevenue > 0
) AS ttr
GROUP BY 
	city, 
	country,
	v2productname
ORDER BY
	prod_revenue DESC
LIMIT 10;
```

<b>Answer:</b> Based on the results, most customers have been purchasing NEST Smarthome Products.

| rank | city          | country       | v2productname                                            | prod_revenue |
|------|---------------|---------------|----------------------------------------------------------|--------------|
| 1    | United States | United States | Nest® Cam Outdoor Security Camera - USA                 | 796.00       |
| 2    | United States | United States | Leatherette Journal                                      | 714.35       |
| 3    | Salem         | United States | Red Spiral Google Notebook                               | 639.36       |
| 4    | Mountain View | United States | Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel | 398.00       |
| 5    | New York      | United States | Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel | 249.00       |
| 6    | New York      | United States | Nest® Protect Smoke + CO White Wired Alarm-USA          | 238.00       |
| 7    | Sunnyvale     | United States | Nest® Cam Outdoor Security Camera - USA                 | 199.00       |
| 7    | San Jose      | United States | Nest® Cam Indoor Security Camera - USA                  | 199.00       |
| 9    | United States | United States | Reusable Shopping Bag                                    | 175.00       |
| 10   | Palo Alto     | United States | Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel | 149.00       |

<br>
<br>

**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

```<language-sql>
SELECT
    city,
    country,
    ROUND((SUM(totaltransactionrevenue) / (SELECT SUM(totaltransactionrevenue) FROM transactions)) * 100, 2) 
	AS revenue_percentage
FROM transactions
GROUP BY
    city,
    country
ORDER BY
    revenue_percentage DESC
LIMIT 10;
```


<b>Answer:</b> We can summarize that most of the revenue is generated in the United States. There is a significate drop after the United States, however Argentia, Ireland, and Spain have a similar revenue share. 

| city          | country       | revenue_percentage |
|---------------|---------------|--------------------|
| United States | United States | 37.86              |
| Mountain View | United States | 13.45              |
| Salem         | United States | 10.94              |
| New York      | United States | 10.11              |
| Sunnyvale     | United States | 5.44               |
| San Francisco | United States | 4.59               |
| San Jose      | United States | 3.41               |
| Palo Alto     | United States | 2.55               |
| Seattle       | United States | 2.04               |
| Argentina     | Argentina     | 1.71               |








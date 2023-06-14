<b>What are your risk areas? Identify and describe them. </b>
<br>
<br>
- My biggest risk areas was to delete table/columns too early in my cleaning stage. 
- Deleting data too early could result in data loss, incomplete analysis, and database integrity.
- That being said, I wanted to have a "running total" of the data I was cleaning and making sure I was working in the right direction.
<br>
<br>


<b>QA Process:</b>

I used the below queries to keep track of all the NULL values in each column. As I went through each table/column, I checked to see if the results were changing. 


** in SALES_REPORT
```<language-sql>
SELECT 
	COUNT(*) AS total_rows,
	COUNT(CASE WHEN productsku IS NULL THEN 1 END) AS productsku,
	COUNT(CASE WHEN total_ordered IS NULL THEN 1 END) AS total_ordered
FROM sales_by_sku;
```

** <b>RESULT:</b> <br>
Total rows: 462, <br>
no NULL values

<br>

** in SALES_REPORT
```<language-sql>
SELECT 
	COUNT(*) AS total_rows,
	COUNT(CASE WHEN productsku IS NULL THEN 1 END) AS productsku,
	COUNT(CASE WHEN total_ordered IS NULL THEN 1 END) AS total_ordered,
	COUNT(CASE WHEN name IS NULL THEN 1 END) AS name,
	COUNT(CASE WHEN stocklevel IS NULL THEN 1 END) AS stocklevel,
	COUNT(CASE WHEN restockingleadtime IS NULL THEN 1 END) AS restockingleadtime,
	COUNT(CASE WHEN sentimentscore IS NULL THEN 1 END) AS sentimentscore,
	COUNT(CASE WHEN sentimentmagnitude IS NULL THEN 1 END) AS sentimentmagnitude,
	COUNT(CASE WHEN ratio IS NULL THEN 1 END) AS ratio
FROM sales_report;
```
	
** <b>RESULT:</b> <br>
Total rows: 454, <br>
Ratio: 78 NULL values

<br>

	
** in PRODUCT
```<language-sql>
SELECT 
	COUNT(*) AS total_rows,
	COUNT(CASE WHEN sku IS NULL THEN 1 END) AS sku,
	COUNT(CASE WHEN name IS NULL THEN 1 END) AS name,
	COUNT(CASE WHEN orderedquantity IS NULL THEN 1 END) AS orderedquantity,
	COUNT(CASE WHEN stocklevel IS NULL THEN 1 END) AS stocklevel,
	COUNT(CASE WHEN restockingleadtime IS NULL THEN 1 END) AS restockingleadtime,
	COUNT(CASE WHEN sentimentscore IS NULL THEN 1 END) AS sentimentscore,
	COUNT(CASE WHEN sentimentmagnitude IS NULL THEN 1 END) AS sentimentmagnitude
FROM products;
```

** <b>RESULT:</b> <br>
Total rows: 1092, <br>
Sentimentscore: 1 NULL values, <br>
Sentimentmagnitude: 1 NULL values
	

<br>

** in ANALYTICS
```<language-sql>
SELECT 
	COUNT(*) AS total_rows,
	COUNT(CASE WHEN visitnumber IS NULL THEN 1 END) AS visitnumber,
	COUNT(CASE WHEN visitid IS NULL THEN 1 END) AS visitid,
	COUNT(CASE WHEN visitstarttime IS NULL THEN 1 END) AS visitstarttime,
	COUNT(CASE WHEN date IS NULL THEN 1 END) AS date,
	COUNT(CASE WHEN fullvisitorid IS NULL THEN 1 END) AS fullvisitorid,
	COUNT(CASE WHEN userid IS NULL THEN 1 END) AS userid,
	COUNT(CASE WHEN channelgrouping IS NULL THEN 1 END) AS channelgrouping,
	COUNT(CASE WHEN socialengagementtype IS NULL THEN 1 END) AS socialengagementtype,
	COUNT(CASE WHEN units_sold IS NULL THEN 1 END) AS units_sold, 
	COUNT(CASE WHEN pageviews IS NULL THEN 1 END) AS pageviews,
	COUNT(CASE WHEN timeonsite IS NULL THEN 1 END) AS timeonsite,
	COUNT(CASE WHEN bounces IS NULL THEN 1 END) AS bounces,
	COUNT(CASE WHEN revenue IS NULL THEN 1 END) AS revenue,
	COUNT(CASE WHEN unitprice IS NULL THEN 1 END) AS unitprice
FROM analytics;
```
	
** <b>RESULT:</b> <br>
Total rows: 4301122, <br>
Units_sold: 4205975 NULL values, <br>
Pageviews: 72 NULL values,<br>
Timeonsite: 477465 NULL values, <br>
Bounces: 477465 NULL values, <br>
Revenue: 4285767 NULL values

** drop columns with all NULL values
```<language-sql>
ALTER TABLE analytics
DROP COLUMN userid;
```

<br>
<br>

	
** in ALL_SESSIONS
```<language-sql>
SELECT 
	COUNT(*) AS total_rows,
	COUNT(CASE WHEN fullvisitorid IS NULL THEN 1 END) AS fullvisitoryid,
	COUNT(CASE WHEN channelgrouping IS NULL THEN 1 END) AS channelgrouping,
	COUNT(CASE WHEN time IS NULL THEN 1 END) AS time,
	COUNT(CASE WHEN country IS NULL THEN 1 END) AS country,
	COUNT(CASE WHEN city IS NULL THEN 1 END) AS city,
	COUNT(CASE WHEN totaltransactionrevenue IS NULL THEN 1 END) AS totaltransactionrevenue,
	COUNT(CASE WHEN transactions IS NULL THEN 1 END) AS transactions, 
	COUNT(CASE WHEN timeonsite IS NULL THEN 1 END) AS timeonsite,
	COUNT(CASE WHEN pageviews IS NULL THEN 1 END) AS pageviews,
	COUNT(CASE WHEN sessionqualitydim IS NULL THEN 1 END) AS sessionqualitydim,
	COUNT(CASE WHEN date IS NULL THEN 1 END) AS date,
	COUNT(CASE WHEN visitid IS NULL THEN 1 END) AS visitid,
	COUNT(CASE WHEN type IS NULL THEN 1 END) AS type,
	COUNT(CASE WHEN productrefundamt IS NULL THEN 1 END) AS productrefundamt,
	COUNT(CASE WHEN productquantity IS NULL THEN 1 END) AS productquantity, 
	COUNT(CASE WHEN productprice IS NULL THEN 1 END) AS productprice,
	COUNT(CASE WHEN productrevenue IS NULL THEN 1 END) AS productrevenue,
	COUNT(CASE WHEN productsku IS NULL THEN 1 END) AS productsku,
	COUNT(CASE WHEN v2productname IS NULL THEN 1 END) AS v2productname,
	COUNT(CASE WHEN v2productcategory IS NULL THEN 1 END) AS v2productcategory,
	COUNT(CASE WHEN productvariant IS NULL THEN 1 END) AS productvariant,
	COUNT(CASE WHEN currencycode IS NULL THEN 1 END) AS currencycode,
	COUNT(CASE WHEN itemquantity IS NULL THEN 1 END) AS itemquantity,
	COUNT(CASE WHEN itemrevenue IS NULL THEN 1 END) AS itemrevenue,
	COUNT(CASE WHEN transactionrevenue IS NULL THEN 1 END) AS transactionrevenue,
	COUNT(CASE WHEN transactionid IS NULL THEN 1 END) AS transactionid,
	COUNT(CASE WHEN pagetitle IS NULL THEN 1 END) AS pagetitle,
	COUNT(CASE WHEN searchkeyword IS NULL THEN 1 END) AS searchkeyword,
	COUNT(CASE WHEN pagepathlevel1 IS NULL THEN 1 END) AS pagepathlevel1,
	COUNT(CASE WHEN ecommerceaction_type IS NULL THEN 1 END) AS ecommerceaction_type,
	COUNT(CASE WHEN ecommerceaction_step IS NULL THEN 1 END) AS ecommerceaction_step,
	COUNT(CASE WHEN ecommerceaction_option IS NULL THEN 1 END) AS ecommerceaction_option
FROM all_sessions;
```

** <b>RESULT:</b> <br>
Total rows: 15134, <br>
Totaltransactionrevenue: 15053 NULL values, <br>
Transactions: 15053 NULL values,<br>
Timeonsite: 3300 NULL values, <br>
Sessioinqualitydim: 13906 NULL values, <br>
Productquantity: 15081 NULL values, <br>
Productrevenue: 15130 NULL values, <br>
Currencycode: 272 NULL values, <br>
Transactionrevenue: 15130 NULL values, <br>
Transactionid: 15125 NULL values, <br>
Pagetitle: 1 NULL values, <br>
Ecommerceaction_option: 15103 NULL values
	
** drop columns with all NULL values
```<language-sql>
ALTER TABLE all_sessions
DROP COLUMN productrefundamt;
```

```<language-sql>
ALTER TABLE all_sessions
DROP COLUMN itemquantity;
```

```<language-sql>
ALTER TABLE all_sessions
DROP COLUMN itemrevenue;
```
```<language-sql>
ALTER TABLE all_sessions
DROP COLUMN searchkeyword;
```
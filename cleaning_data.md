What issues will you address by cleaning the data?

  - NULL values
  - missing information
  - incorrect data types
  - incorrect column format
  - incorrect pricing values
  - duplicate columns


Queries:
Below, provide the SQL queries you used to clean your data.


--------------------------------------------------
** looked for null values and drop NULL columns **
--------------------------------------------------

** in SALES_REPORT
SELECT 
	COUNT(*) AS total_rows,
	COUNT(CASE WHEN productsku IS NULL THEN 1 END) AS productsku,
	COUNT(CASE WHEN total_ordered IS NULL THEN 1 END) AS total_ordered
FROM sales_by_sku;

** RESULt: Total rows: 462, no NULL values


** in SALES_REPORT
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
	
** RESULt: Total rows: 454, Ratio: 78 NULL values
	
	
** in PRODUCT
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

** RESULt: Total rows: 1092, Sentimentscore: 1 NULL values, Sentimentmagnitude: 1 NULL values
	
	
** in ANALYTICS
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
	
** RESULt: Total rows: 4301122, Units_sold: 4205975 NULL values, Pageviews: 72 NULL values,
	Timeonsite: 477465 NULL values, Bounces: 477465 NULL values, Revenue: 4285767 NULL values

** drop columns with all NULL values
ALTER TABLE analytics
DROP COLUMN userid;

	
** in ALL_SESSIONS
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

** RESULt: Total rows: 15134, Totaltransactionrevenue: 15053 NULL values, Transactions: 15053 NULL values,
	Timeonsite: 3300 NULL values, Sessioinqualitydim: 13906 NULL values, Productquantity: 15081 NULL values, 
	Productrevenue: 15130 NULL values, Currencycode: 272 NULL values, Transactionrevenue: 15130 NULL values, 
	Transactionid: 15125 NULL values, Pagetitle: 1 NULL values, Ecommerceaction_option: 15103 NULL values
	
** drop columns with all NULL values
ALTER TABLE all_sessions
DROP COLUMN productrefundamt;

ALTER TABLE all_sessions
DROP COLUMN itemquantity;

ALTER TABLE all_sessions
DROP COLUMN itemrevenue;

ALTER TABLE all_sessions
DROP COLUMN searchkeyword;

-------------------------------------------------------------------------------
** Compared columns with the same or like names, check for duplicate columns **
-------------------------------------------------------------------------------

** compare NAME/v2PRODUCTNAME columns in TABLES: sales_report, products and all_sessions
SELECT
	sr.name AS sr_name,
	p.name AS p_name,
	al.v2productname AS al_v2productname
FROM
	sales_report sr
FULL JOIN products p
	ON sr.name = p.name
FULL JOIN all_sessions al
	USING(productsku)
	
** Result: sr.name and p.name are the same, but al.v2productname includes a brand name
	
	
** compare PRODUCTSKU/SKU columns in sales_report, all_sessions and products
SELECT
	sr.productsku AS sr_productsku,
	al.productsku AS al_productsku,
	sbs.productsku AS sbs_productsku,
	p.sku AS p_sku	
FROM sales_report sr
FULL JOIN products p
	USING(name)
FULL JOIN all_sessions al
	USING(productsku)
FULL JOIN sales_by_sku sbs
	USING(productsku)
	
** Result: p.sku has some matching skus to productsku, however most are different skus. 
	sr.productsku, sbs.productsku and al.productsku are the same, however al.productsku has 
	more distinct values
	
	
** compare VISITID/VISITSTARTTIME columns in all_sessions and analytics
SELECT
	al.visitid AS al_visitid,
	ac.visitid AS ac_visitid,
	ac.visitstarttime AS visitstarttime
FROM
	analytics ac
FULL JOIN all_sessions al
	USING(date)
	
** Result: ac.visitid and ac.visitstarttime have duplicate date, will drop ac.visitid. 

** drop duplicate column
ALTER TABLE analytics
DROP COLUMN visitid;
	

** compare TOTAL_ORDER/ORDEREDQUANTITY columns in sales_by_sku, sales_report and products
SELECT
	p.orderedquantity AS p_orderedquantity,
	sr.total_ordered AS sr_total_ordered,
	sbs.total_ordered AS sbs_total_ordered 
FROM sales_report sr
FULL JOIN products p
	ON p.name = sr.name
FULL JOIN sales_by_sku sbs
	USING(productsku)

** Result: p.orderedquantity quantites do not match sr.total_ordered and sbs.total_ordered


** compare PRODUCTSKU/TOTAL_ORDERED columns in sales_by_sku and sales_report
SELECT 
	sbs.productsku,
	sbs.total_ordered,
	sr.productsku, 
	sr.total_ordered
FROM sales_by_sku sbs
FULL JOIN sales_report sr
	USING(productsku)
where sbs.productsku != sr.productsku 

** Result: sbs.productsku/sbs.total_ordered have the same data in both sales_by_sku and sales_report tables; drop sales_by_sku table

** drop table
DROP TABLE sales_by_sku


--------------------------------
** CREATED TRANSACTIONS TABLE **
--------------------------------
** created table to focus on important infomation requirred to provide insights

CREATE TABLE transactions AS
SELECT 
	productsku,
	v2productname,
	v2productcategory,
	productquantity,
	productprice,
	currencycode,
	city,
	country,
	productrevenue,
	totaltransactionrevenue, 
	transactions, 
	transactionrevenue, 
	transactionid 
FROM 
	all_sessions;

------------------------------
** CLEAN TRANSACTIONS TABLE ** 
------------------------------

** convert productquantity data type
ALTER TABLE transactions
ALTER COLUMN productquantity TYPE integer 
USING productquantity::integer;

UPDATE transactions
SET productquantity = CASE
                                WHEN productquantity IS NULL THEN 0
                                ELSE productquantity
                              END;

** updated productprice, covert data type to numeric; when NULL = 0
ALTER TABLE transactions
ALTER COLUMN productprice TYPE numeric (20,2)
USING productprice::numeric (20,2);

UPDATE transactions
SET productprice = CASE
                                WHEN productprice IS NULL THEN 0
                                ELSE productprice
                              END;

UPDATE transactions
SET productprice = productprice / 1000000;

** updated currencycode when NULL = USD
UPDATE transactions
SET CURRENCYCODE = 'USD'
WHERE CURRENCYCODE IS NULL;


** updated productrevenue, covert data type to numeric; when NULL = 0
ALTER TABLE transactions
ALTER COLUMN productrevenue TYPE numeric (20,2)
USING productrevenue::numeric (20,2);

UPDATE transactions
SET productrevenue = CASE
					WHEN productrevenue IS NULL THEN 0
					ELSE productrevenue
				  END;

UPDATE transactions
SET productrevenue = productrevenue / 1000000;

** updated transactions when NULL = 0; 
UPDATE transactions
SET transactions = CASE
					WHEN transactions IS NULL THEN 0
					ELSE transactions
				END;
				
** updated transactions, if there is a productquantity then there is 1 transation
UPDATE all_sessions
SET transactions = CASE
					WHEN productquantity > 0 THEN 1
					ELSE transactions
				END;

** updated transactionrevenue, covert data type to numeric; when NULL = 0; transactionrevenue/1000000
ALTER TABLE transactions
ALTER COLUMN transactionrevenue TYPE numeric (20,2)
USING transactionrevenue::numeric (20,2);

UPDATE transactions
SET transactionrevenue = CASE
						WHEN transactionrevenue IS NULL THEN 0
						ELSE transactionrevenue
					  END;

UPDATE transactions
SET transactionrevenue = transactionrevenue / 1000000;

** updated totaltransactionrevenue, covert data type to numeric; when NULL = 0; totaltransactionrevenue/1000000
ALTER TABLE transactions
ALTER COLUMN totaltransactionrevenue TYPE numeric (20,2)
USING totaltransactionrevenue::numeric (20,2);

UPDATE transactions
SET totaltransactionrevenue = CASE
                                WHEN totaltransactionrevenue IS NULL THEN 0
                                ELSE totaltransactionrevenue
                              END;

UPDATE transactions
SET totaltransactionrevenue = totaltransactionrevenue / 1000000;

** updated transactionid when NULL = 0
UPDATE transactions
SET transactionid = '-'
WHERE transactionid IS NULL;

** missing city informaiton = (not available in demo dataset) and (not set),converted to country
UPDATE transactions
SET CITY = CASE
    WHEN CITY = '(not set)' THEN COUNTRY
    ELSE CITY
    END;
	
UPDATE transactions
SET CITY = CASE
    WHEN CITY = 'not available in demo dataset' THEN COUNTRY
    ELSE CITY
    END;

------------------------------
** CLEAN SALES_REPORT TABLE **
------------------------------

** convert NULL to 0 - ratio
UPDATE sales_report
SET ratio = CASE
			WHEN ratio IS NULL THEN 0
			ELSE ratio
		  END;

--------------------------
** CLEAN PRODUCTS TABLE ** 
--------------------------

** convert NULL to 0 - sentimentscore
UPDATE products
SET sentimentscore = CASE
					WHEN sentimentscore IS NULL THEN 0
					ELSE sentimentscore
				  END;

** convert NULL to 0 - sentimentmagnitude
UPDATE products
SET sentimentmagnitude = CASE
						WHEN sentimentmagnitude IS NULL THEN 0
						ELSE sentimentmagnitude
					  END;

---------------------------
** CLEAN ANALYTICS TABLE **
---------------------------

** convert visitstarttime to epoch time format
ALTER TABLE analytics
ALTER visitstarttime TYPE TIMESTAMPTZ
USING timezone('UTC', TO_TIMESTAMP(visitstarttime))


** convert NULL to 0 - units_sold
UPDATE analytics
SET units_sold = CASE
					WHEN units_sold IS NULL THEN 0
					ELSE units_sold
				  END;

** convert NULL to 0 - pageviews
UPDATE analytics
SET pageviews = CASE
					WHEN pageviews IS NULL THEN 0
					ELSE pageviews
				  END;
				  
** convert NULL to 0 - timeonsite
UPDATE analytics
SET timeonsite = CASE
					WHEN timeonsite IS NULL THEN 0
					ELSE timeonsite
				  END;
				  
** convert to relavent time format - timeonsite
ALTER TABLE analytics
ALTER COLUMN timeonsite
TYPE VARCHAR
USING LPAD(timeonsite::VARCHAR, 6, '0');

UPDATE analytics
SET timeonsite = CONCAT(
    SUBSTRING(timeonsite, 1, 2),
    ':',
    SUBSTRING(timeonsite, 3, 2),
    ':',
    SUBSTRING(timeonsite, 5, 2)
);

UPDATE analytics
SET timeonsite = TIME '00:00:00' + 
           INTERVAL '1 hour' * CAST(SUBSTR(timeonsite, 1, 2) AS INTEGER) +
           INTERVAL '1 minute' * CAST(SUBSTR(timeonsite, 4, 2) AS INTEGER) +
           INTERVAL '1 second' * CAST(SUBSTR(timeonsite, 7, 2) AS INTEGER);

ALTER TABLE analytics
ALTER COLUMN timeonsite TYPE TIME USING timeonsite::TIME;

** convert NULL to 0 - bounces
UPDATE analytics
SET bounces = CASE
				WHEN bounces IS NULL THEN 0
				ELSE bounces
			  END;

** convert NULL to 0 - revenue
UPDATE analytics
SET revenue = CASE
				WHEN revenue IS NULL THEN 0
				ELSE revenue
			  END;

** correct revenue
ALTER TABLE analytics
ALTER COLUMN revenue TYPE numeric (20,2);

UPDATE analytics
SET revenue = revenue / 1000000;

** correct unitprice
ALTER TABLE analytics
ALTER COLUMN unitprice TYPE numeric (20,2);

UPDATE analytics
SET unitprice = unitprice / 1000000;

------------------------------
** CLEAN ALL_SESSIONS TABLE **
------------------------------

** convert NULL to 0 - time
UPDATE all_sessions
SET time = 0
WHERE time IS NULL;

** convert to relavent time format - time
ALTER TABLE all_sessions
ALTER COLUMN time
TYPE VARCHAR
USING LPAD(time::VARCHAR, 6, '0');

UPDATE all_sessions
SET time = CONCAT(
    SUBSTRING(time, 1, 2),
    ':',
    SUBSTRING(time, 3, 2),
    ':',
    SUBSTRING(time, 5, 2)
);

UPDATE all_sessions
SET time = TIME '00:00:00' + 
           INTERVAL '1 hour' * CAST(SUBSTR(time, 1, 2) AS INTEGER) +
           INTERVAL '1 minute' * CAST(SUBSTR(time, 4, 2) AS INTEGER) +
           INTERVAL '1 second' * CAST(SUBSTR(time, 7, 2) AS INTEGER);

ALTER TABLE all_sessions
ALTER COLUMN time TYPE TIME USING time::TIME;

** updated productvariant, replace (not set) with -
UPDATE all_sessions
SET productvariant = '-'
WHERE productvariant = '(not set);

** missing city informaiton = (not available in demo dataset) and (not set),converted to country
UPDATE all_sessions
SET CITY = CASE
    WHEN CITY = '(not set)' THEN COUNTRY
    ELSE CITY
    END;
	
UPDATE all_sessions
SET CITY = CASE
    WHEN CITY = 'not available in demo dataset' THEN COUNTRY
    ELSE CITY
    END;

** updated totaltransactionrevenue, covert data type to numeric; when NULL = 0; totaltransactionrevenue/1000000
ALTER TABLE all_sessions
ALTER COLUMN totaltransactionrevenue TYPE numeric (20,2)
USING totaltransactionrevenue::numeric (20,2);

UPDATE all_sessions
SET totaltransactionrevenue = CASE
                                WHEN totaltransactionrevenue IS NULL THEN 0
                                ELSE totaltransactionrevenue
                              END;

UPDATE all_sessions
SET totaltransactionrevenue = totaltransactionrevenue / 1000000;

** updated transactions when NULL = 0; 
UPDATE transactions
SET transactions = CASE
					WHEN transactions IS NULL THEN 0
					ELSE transactions
				END;
				
** updated transactions, if there is a productquantity then there is 1 transation
UPDATE all_sessions
SET transactions = CASE
					WHEN productquantity > 0 THEN 1
					ELSE transactions
				END;
				
** convert NULL to 0 - timeonsite
UPDATE all_sessions
SET timeonsite = 0
WHERE timeonsite IS NULL;

** convert to relavent time format - timeonsite
ALTER TABLE all_sessions
ALTER COLUMN timeonsite
TYPE VARCHAR
USING LPAD(timeonsite::VARCHAR, 6, '0');

UPDATE all_sessions
SET timeonsite = CONCAT(
    SUBSTRING(timeonsite, 1, 2),
    ':',
    SUBSTRING(timeonsite, 3, 2),
    ':',
    SUBSTRING(timeonsite, 5, 2)
);

UPDATE all_sessions
SET timeonsite = TIME '00:00:00' + 
           INTERVAL '1 hour' * CAST(SUBSTR(timeonsite, 1, 2) AS INTEGER) +
           INTERVAL '1 minute' * CAST(SUBSTR(timeonsite, 4, 2) AS INTEGER) +
           INTERVAL '1 second' * CAST(SUBSTR(timeonsite, 7, 2) AS INTEGER);

ALTER TABLE all_sessions
ALTER COLUMN timeonsite TYPE TIME USING timeonsite::TIME;

** convert sessionqualitydim
UPDATE all_sessions
SET sessionqualitydim = CASE
						WHEN sessionqualitydim IS NULL THEN 0
						ELSE sessionqualitydim
					  END;

** convert productquantity data type
ALTER TABLE all_sessions
ALTER COLUMN productquantity TYPE integer 
USING productquantity::integer ;

UPDATE all_sessions
SET productquantity = CASE
                                WHEN productquantity IS NULL THEN 0
                                ELSE productquantity
                              END;

** updated productprice, covert data type to numeric; when NULL = 0
ALTER TABLE all_sessions
ALTER COLUMN productprice TYPE numeric (20,2)
USING productprice::numeric (20,2);

UPDATE all_sessions
SET productprice = CASE
                                WHEN productprice IS NULL THEN 0
                                ELSE productprice
                              END;

UPDATE all_sessions
SET productprice = productprice / 1000000;


** updated productrevenue, covert data type to numeric; when NULL = 0
ALTER TABLE all_sessions
ALTER COLUMN productrevenue TYPE numeric (20,2)
USING productrevenue::numeric (20,2);

UPDATE all_sessions
SET productrevenue = CASE
					WHEN productrevenue IS NULL THEN 0
					ELSE productrevenue
				  END;

UPDATE all_sessions
SET productrevenue = productrevenue / 1000000;

** updated currencycode when NULL = USD
UPDATE all_sessions
SET CURRENCYCODE = 'USD'
WHERE CURRENCYCODE IS NULL;

** updated transactionrevenue, covert data type to numeric; when NULL = 0; transactionrevenue/1000000
ALTER TABLE all_sessions
ALTER COLUMN transactionrevenue TYPE numeric (20,2)
USING transactionrevenue::numeric (20,2);

UPDATE all_sessions
SET transactionrevenue = CASE
						WHEN transactionrevenue IS NULL THEN 0
						ELSE transactionrevenue
					  END;

UPDATE all_sessions
SET transactionrevenue = transactionrevenue / 1000000;

** updated transactionid when NULL = -
UPDATE all_sessions
SET transactionid = '-'
WHERE transactionid IS NULL;

** convert pagetitle when NULL = -
UPDATE all_sessions
SET pagetitle = '-'
WHERE pagetitle IS NULL;

** ecommerceaction_option when NULL = -
UPDATE all_sessions
SET ecommerceaction_option = '-'
WHERE ecommerceaction_option IS NULL;

-------------------------
** ADDITIONAL CLEANING ** 
-------------------------

** calculate productrevenue ** 
UPDATE transactions
SET productrevenue = productquantity * productprice;

** calculate transactionrevenue ** 
UPDATE transactions
SET transactionrevenue = productquantity * productprice;

** calculate totaltransactionrevenue ** 
UPDATE transactions
SET totaltransactionrevenue = productquantity * productprice;

** calculate revenue ** 
UPDATE analytics
SET revenue = units_sold * unitprice;

** calculate productrevenue ** 
UPDATE all_sessions
SET productrevenue = productquantity * productprice;

** calculate transactionrevenue ** 
UPDATE all_sessions
SET transactionrevenue = productquantity * productprice;

** calculate totaltransactionrevenue ** 
UPDATE all_sessions
SET totaltransactionrevenue = productquantity * productprice;



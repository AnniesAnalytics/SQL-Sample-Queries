# SQL-Sample-Queries
Here is where I will keep logs of what I am learning!

# AVERAGE TEMPERATURE
SELECT AVG(temperature) <br/>
FROM `skillful-coast-340323.demos.weather_nyc` <br/>
WHERE date BETWEEN '2020-06-01' AND '2020-06-30' <br/><br/>
 
# ALIAS 
Basic format for an AS query: <br/>
SELECT column_name(s) <br/>
FROM table_name AS alias_name; <br/><br/>
&emsp; Notice that AS is preceded by the table name and followed by the new nickname. It is a similar approach to aliasing a column:<br/><br/>
SELECT column_name AS alias_name <br/>
FROM table_name; <br/><br/>

If using AS results in an error when running a query because the SQL database you are working with doesn't support it, you can leave it out. In the previous examples, the alternate syntax for aliasing a table or column would be: <br/>

FROM table_name alias_name <br/>

SELECT column_name alias_name <br/>

# BETWEEN
SELECT
	Date, purchase_price
FROM customer_data.purchases
WHERE
	Date BETWEEN ‘2020-12-01’ AND ‘2020-12-20’

# CAST
SELECT <br/>
CAST(purchase_price AS FLOAT64) <br/>
FROM customer.data_purchase <br/>
ORDER BY purchase_price DESC

SELECT
CAST(date AS date) AS date_only <br/>
FROM customer_data.purchases  <br/>
The above statement changes SQL from recognizing the dates as datetime (2020-12-12T0:00:00) to only date (2020-12-12)

# CAST 
<br/>(expression AS typename)    Where expression is the data to be converted and typename is the data type to be returned.

## Converting a number to a string: 
SELECT CAST(MyCount AS String) FROM MyTable <br/>
In the above SQL statement, the following occurs: SELECT indicates that you will be selecting data from a table. CAST indicates that you will be converting the data you select to a different data type. AS comes before and identifies the data type which you are casting to. STRING indicates that you are converting the data to a string. FROM indicates which table you are selecting the data from <br/>
## Converting String to a number:
SELECT CAST(MyVarcharCol AS INT) FROM MyTable <br/>
CAST indicates that you will be converting the data you select to a different data type. AS comes before and identifies the data type which you are casting to. INT indicates that you are converting the data to an integer<br/>
## Convert date to a string:
SELECT CAST(MyDate AS STRING) FROM MyTable <br/>
## Converting a date to a datetime: Datetime values have the format of YYYY-MM-DD hh: mm: ss format
SELECT CAST (MyDate AS DATETIME) FROM MyTable
## The SAFE_CAST function: Using the CAST function in a query that fails returns an error in BigQuery. It returns null instead of error. 
SELECT SAFE_CAST (MyDate AS STRING) FROM MyTable
 
# CONCAT
SELECT <br/>
	CONCAT(product_code, product_color) AS new_product_code <br/>
FROM customer_purchase.data <br/>
WHERE <br/>
	Product = ‘couch’ <br/> <br/> <br/>
	
SELECT usertype <br/>
	CONCAT(start_station_name, “ to “, end_station_name) AS route, <br/>
	COUNT (*) as num_trips, <br/>
ROUND(AVG(cast(tripduration as int64)/60,2) AS duration <br/>
FROM big-query-public-data.ny <br/>
GROUP BY start_station_name, end_station_name, usertype <br/>
ORDER BY num_trips DESC <br/>
LIMIT 10 <br/>
Reminder: Make sure to use a backtick (`) instead of an apostrophe (') in the FROM statement. <br/>
About: ROUND(AVG(cast(tripduration as int64)/60,2) AS duration <br/>
Big query stores numbers in a 64-bit memory system, which is why there's a 64 after integer in this case. we'll divide it by the number seconds in a minute (60) and tell it how far we want it to round, two decimal places(2).<br/>
# COALESCE
SELECT <br/>
	COALESCE(product, product_code) AS product_info <br/>
FROM customer_data.purchase <br/>
Return non-null values in a list <br/>

# CASE
The CASE statement goes through one or more conditions and returns a value as soon as a condition is met <br/>
SELECT <br/>
	Customer_id <br/>
	CASE  <br/>
		WHEN first_name = ‘Tnoy’ THEN ‘TONY’ <br/>
		ELSE first_name <br/>
		END AS cleaned_name <br/>
FROM customer.data
 
# DISTINCT
SELECT  DISTINCT fuel_type <br/>
FROM cars.car_info; <br/>
SELECT DISTINCT name <br/>
FROM playlist <br/>
ORDER BY playlist_id <br/>

# JOIN
General join syntax: <br/>
SELECT <br/>
--table columns are inserted here <br/>
Table_name1.column_name <br/>
Table_name2.column_name <br/>
FROM <br/>
&emsp;	Table_name1 <br/>
JOIN <br/>
&emsp;	Table_name2 <br/>
ON table_name1.column_name=table_name2.column_name <br/> 
(the column name is the key, be it primary key or foreign key that they share in common) <br/> <br/> 
SELECT <br/>
&emsp;	Customers.customer_name, <br/>
&emsp;	Orders.product_id, <br/> 
&emsp;	Orders.ship_date <br/>
FROM <br/>
&emsp;	Customers <br/>
INNER JOIN <br/>
&emsp;	Orders <br/>
ON customers.customer_id = orders.customer_id <br/>


SELECT <br/>
&emsp; employees.name AS employee_name, <br/>
    &emsp; employees.role AS employee_role, <br/>
    &emsp; departments.name AS department_name <br/>
FROM employee_data.employees <br/>
INNER JOIN  <br/>
   &emsp; employee_data.departments ON  <br/>
   &emsp; employees.department_id = departments.department_id <br/>
   
SELECT <br/>
&emsp; employees.name AS employee_name, <br/>
    &emsp; employees.role AS employee_role, <br/>
    &emsp; departments.name AS department_name <br/>
FROM employee_data.employees <br/>
FULL OUTER JOIN  <br/>
   &emsp; employee_data.departments ON  <br/>
   &emsp; employees.department_id = departments.department_id <br/> <br/> 
   
  SELECT <br/> 
  &emsp;`bigquery-public-data.world_bank_intl_education.international_education`.country_name, <br/>  
    &emsp;  `bigquery-public-data.world_bank_intl_education.country_summary`.country_code,  <br/> 
   &emsp;   `bigquery-public-data.world_bank_intl_education.international_education`.value, <br/> 
   &emsp;   `bigquery-public-data.world_bank_intl_education.country_summary`.short_name, <br/> 
FROM  <br/> 
  &emsp;    `bigquery-public-data.world_bank_intl_education.international_education` <br/> 
INNER JOIN  <br/> 
   &emsp;   `bigquery-public-data.world_bank_intl_education.country_summary`  <br/> 
ON `bigquery-public-data.world_bank_intl_education.country_summary`.country_code = `bigquery-public-data.world_bank_intl_education.international_education`.country_code <br/><br/> 
To use the SAME query but with alias' to clean it up: <br/><br/>

SELECT <br/>
  &emsp;   edu.country_name, <br/>
   &emsp;  summary.country_code, <br/>
    &emsp; edu.value <br/>
FROM  <br/>
   &emsp;  `bigquery-public-data.world_bank_intl_education.international_education` AS edu <br/>
INNER JOIN  <br/>
   &emsp;  `bigquery-public-data.world_bank_intl_education.country_summary` AS summary  <br/>
ON edu.country_code = summary.country_code  <br/> <br/>

SELECT <br/>
&emsp; seasons.market AS university, <br/>
&emsp; seasons.name AS team_name, <br/>
&emsp; seasons.wins, <br/>
&emsp; seasons.losses, <br/>
&emsp; seasons.ties, <br/>
&emsp; mascots.mascot AS team_mascot <br/>
FROM <br/>
&emsp; `bigquery-public-data.ncaa_basketball.mbb_historical_teams_seasons` AS seasons <br/>
LEFT JOIN <br/>
&emsp; `bigquery-public-data.ncaa_basketball.mascots` AS mascots <br/>
ON <br/>
&emsp; seasons.team_id = mascots.id <br/>
 WHERE  <br/>
&emsp; seasons.season = 1984 <br/>
 AND seasons.division = 1 <br/>
 ORDER BY  <br/>
&emsp; seasons.market <br/>

# LENGTH
SELECT length (title) AS letters_in_title, album_id <br/>
FROM album <br/>
WHERE letters_in_title < 4 <br/>
The function LENGTH(title) < 4 will return any album names that are less than 4 characters long. The complete query is SELECT * FROM album WHERE LENGTH(title) < 4. The LENGTH function counts the number of characters a string contains. <br/>
TRIM

# MIN/MAX
SELECT <br/>
    MIN(length) AS min_length, <br/>
    MAX(length) AS max_length <br/>
FROM cars.car_info; <br/>



# Order By
SELECT * <br/>
FROM movie_data.movies <br/>
ORDER BY Release_date DESC <br/> <br/><br/>

SELECT * 
FROM movies.data <br/>
WHERE Genre = ‘Comedy’ <br/>
AND Revenue >  30000000 <br/>
ORDER BY Release_date DESC <br/> <br/><br/>

SELECT total <br/>
FROM invoice <br/>
WHERE billing_city = "Chicago" <br/>
ORDER BY total ASC <br/> <br/><br/>


SELECT County_of_Residence  <br/>
FROM `bigquery-public-data.sdoh_cdc_wonder_natality.county_natality` <br/>
ORDER BY Births ASC <br/>
LIMIT 10 <br/><br/><br/>
 
SELECT County_of_Residence <br/>
FROM `bigquery-public-data.sdoh_cdc_wonder_natality.county_natality` <br/>
WHERE year = '2018-01-01' <br/>
ORDER BY Births DESC <br/>
LIMIT 10 <br/>
The year had to be in ‘ ‘ for it to work, and since it is in date formate, it would not work as simply 2018. <br/><br/><br/>
 

SELECT<br/>
The meteorologists who you’re working with have asked you to get the temperature, wind speed, and precipitation for stations La Guardia and JFK, for every day in 2020, in descending order by date, and ascending order by Station ID. Use the following query to request this information: <br/>
SELECT stn, date, <br/>
	IF(temp=9999.9, NULL, temp) AS temperature, <br/>
	IF(wdsp="999.9", NULL, CAST(wdsp AS Float64)) AS wind_speed, <br/>
	IF(prcp=99.99, 0, prcp) AS precipitation <br/>
FROM  `bigquery-public-data.noaa_gsod.gsod2020` <br/>
WHERE stn="725030" -- La Guardia <br/>
	OR stn="744860" -- JFK <br/>
ORDER BY  date DESC, stn ASC <br/>
-- Use the IF function to replace 9999.9 values, which the dataset description explains is the default value when temperature is missing, with NULLs instead. <br/>
-- Use the IF function to replace 999.9 values, which the dataset description explains is the default value when wind speed is missing, with NULLs instead. -- Use the IF function to replace 99.99 values, which the dataset description explains is the default value when precipitation is missing, with NULLs instead. <br/>
 
# SUBSTR
SELECT  customer_id, <br/>
    SUBSTR(country,1,3) AS new_country <br/>
FROM customer <br/>
ORDER BY country <br/>
The statement SUBSTR(country, 1, 3) AS new_country will retrieve the first 3 letters of each state name and store the result in a new column as new_country. The complete query is SELECT customer_id, SUBSTR(country, 1, 3) AS new_country FROM customer ORDER BY country. The SUBSTR function extracts a substring from a string. This function instructs the database to return 3 characters of each country, starting with the first character. <br/><br/>
SELECT Invoice_id, <br/>
	SUBSTR(billing_city,1,4) AS new_city <br/>
FROM invoice <br/>
ORDER BY billing_city <br/>
Billing city= city, 1=starting position in string, 4=how many you return <br/>

# UPDATE
UPDATE  cars.car_info <br/>
     SET num_of_doors = "four" <br/>
WHERE  make = "dodge" AND fuel_type = "gas" AND body_style = "sedan"; <br/>

# WHERE
SELECT   * <br/>
FROM   cars.car_info <br/> 
WHERE  num_of_doors IS NULL; <br/>

SELECT * 
FROM movies.data <br/>
WHERE Genre = ‘Comedy’ <br/>
Because the genre is a string, you need to put the ‘ ‘ around the string name. Capitalizations matter <br/><br/>

SELECT CustomerId <br/>
FROM invoices <br/>
WHERE BillingCountry = 'Germany' AND Total > 5




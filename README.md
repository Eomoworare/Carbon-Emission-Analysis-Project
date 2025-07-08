# Carbon-Emission-Analysis
Understanding carbon emissions across various industries is vital in tackling global climate change. With SQL, I will uncover which sectors are the biggest polluters and track how these emissions have changed over time to aid in sustainable decision-making.

Dataset: The dataset includes emission data by industry, country, and year, along with greenhouse gas types like CO2, CH4, and N2O.

SQL Project Idea: Create a carbon tracking database in SQL.

A carbon tracking database was created using Microsoft SQL Server Management Studio. Data cleaning processes were applied such as blank spaces replaced with Zero's (0) and changed the data types to float, varchar, int and text. The table Cargo Emissions was imported as a CSV file into the database.

The following questions were answered using SQL. They are highlighted below:

1. Which industry had the highest CO2 emissions in the most recent year?


**SQL QUERY FOR Q1.**

--Query to produce the highest emission in the latest year
--Question 1:
Select MAX(Value)
 FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v2]
where year = 
(Select MAX (Year)
 FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v2])


Result: 201.957992553711

![image](https://github.com/user-attachments/assets/e066af91-c148-4abb-84ac-c0d0013ecafc)



2. What has been the trend of total emissions across sectors over the last decade?


**SQL QUERY FOR Q2.**

 --Query to show the values of emissions over the last 10 years for each sector
--Question 2:
select MSN, sum(value) as [Total Emissions], Year
 FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v2]
where YEAR>=(SELECT MAX (YEAR)-10
 FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v2])
Group by MSN, Year 
Order by MSN


Result: Nearly all sectors showed a reduction in the last 10 years with further significant reduction in CO2 emissions in 2016.



![image](https://github.com/user-attachments/assets/576ed0fb-fb80-4c18-863a-6048505a0fd8)





3. Which industries showed a decline in emissions over the years?


**SQL QUERY FOR Q3**

--Query to show the values of emissions over the last 10 years for each sector
--Question 3:
select MSN, round(sum(value),2) as [Total Emissions], Year
FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v.2]
where YEAR>=
(SELECT MAX (YEAR)-10
 FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v.2])
Group by MSN, Year 
Order by MSN

Result: Trend chart from SQL Q2 result was used to get the result for SQL Q3

![Carbon Emissions Industry Decade Trend Q3 Result v](https://github.com/user-attachments/assets/93f66223-03ca-4e72-a9b8-2cee97413c03)

Three major industries showed a decline over the years being as seen from chart above

1.	PAEIEUS
2.	RFEIEUS
3.	PCEIEUS


4. How does the emission share differ across continents or economic zones?


**SQL QUERY FOR Q4**

--Query to show How the emission share differ across economic zones
--Question 4:
SELECT DISTINCT MSN, 
       sum(value) as [Total Emissions], 
       ROUND(sum(value)* 100.0 / (SELECT DISTINCT sum(value) FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v.2]),2) as [% Emissions]
FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v.2]
Group by MSN
With Rollup
Order by [Total Emissions]


Result: 


![image](https://github.com/user-attachments/assets/d13d9e90-8776-4253-b87b-03daa06959a5)



 5. Identify the top three emitting industries and their year-wise emission pattern.


**SQL QUERY FOR Q5**

--Q51-Query to Identify the top three emitting industries and their year-wise emission pattern.
--Question 5:

--To identify the top 3 industries by Description
Select top 3 [Description],
	   Round(sum(value),2) as [Total Emissions]
FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v.2]
Group by [Description]
Order by [Total Emissions] Desc


![image](https://github.com/user-attachments/assets/3e2f9529-3c06-4c22-9493-11d89b5b57ee)





--Q52-To identify the top 3 industries by column order
Select top 3 column_order,
	   Round(sum(value),2) as [Total Emissions]
FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v.2]
Group by column_order
Order by [Total Emissions] Desc

 
![image](https://github.com/user-attachments/assets/a1fc97da-a2f1-463b-a98a-1482283171ed)





Q5 Identify the top three emitting industries and their year-wise emission pattern.
Select [Description],
	   round(sum(value),2) as [Total Emissions], 
       Year
FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v.2]
where [Column_Order] = 9
OR
[Column_Order] = 1
OR
[Column_Order] = 2
Group by [Description], Year 
Order by [Description]



![image](https://github.com/user-attachments/assets/3a625242-a44b-469d-b361-6fc2173f0f72)


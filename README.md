# Carbon-Emission-Analysis-Project
Understanding carbon emissions across various industries is vital in tackling global climate change. With SQL, I will uncover which sectors are the biggest polluters and track how these emissions have changed over time to aid in sustainable decision-making.

Dataset: The dataset includes emission data by industry, country, and year, along with greenhouse gas types like CO2, CH4, and N2O.

SQL Project Idea: Create a carbon tracking database in SQL.

A carbon tracking database was created using Microsoft SQL Server Management Studio. Data claning processes were applied such as blank spaces replaced with Zero's (0) and changed the data types to float, varchar, int and text. The table Cargo Emissions was imported as a CSV file into the database.

The following questions were answered using SQL. They are highlighted below:

1. Which industry had the highest CO2 emissions in the most recent year?

SQL QUERY FOR Q1. 

--Query to produce the highest emission in the latest year
--Question 1:
Select MAX(Value)
 FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v2]
where year = 
(Select MAX (Year)
 FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v2])


Result: 201.957992553711

![image](https://github.com/user-attachments/assets/aae18258-b931-4ffc-9c86-c2662b4f1bc8)





2. What has been the trend of total emissions across sectors over the last decade?

SQL QUERY FOR Q2. 

 --Query to show the values of emissions over the last 10 years for each sector
--Question 2:
select MSN, sum(value) as [Total Emissions], Year
 FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v2]
where YEAR>=(SELECT MAX (YEAR)-10
 FROM [Carbon Emissions].[dbo].[Cargo Emissions Data v2])
Group by MSN, Year 
Order by MSN


Result: Nearly all sectors showed a reduction in the last 10 years with further reduction in CO2 emissions in 2016 being the latest year.


![Carbon Emissons Industry Decade Trend](https://github.com/user-attachments/assets/b7a1972c-ec42-4690-aa75-94be19ca7805)



3. Which industries showed a decline in emissions over the years?

4. How does the emission share differ across continents or economic zones?

5. Identify the top three emitting industries and their year-wise emission pattern.

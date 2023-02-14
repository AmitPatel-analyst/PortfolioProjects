# International-Debt-Statistics-Analysis-
In this project, we are going to analyze international debt data collected by The World Bank. The dataset contains information about the amount of debt (in USD) owed by developing countries across several categories. We are going to find the answers to questions like:

What is the total amount of debt that is owed by the countries listed in the dataset? Which country owns the maximum amount of debt and what does that amount look like? What is the average amount of debt owed by countries across different debt indicators?
In this project, we are going to use DISTINCT, COUNT, SUM, ROUND, MAX, MIN, GROUPBY 

--The first line of code connects us to the international_debt database where the table international_debt is residing. 
use international_debt
go

-- Let's first SELECT all of the columns from the international_debt table. Also, we'll limit the output to the first ten rows to keep the output clean.
```sql
select top 10 * from international_debt;
```
--1.Finding the number of distinct countries
```sql
select count(distinct(country_name)) as Total_Countries_Names
from international_debt;
```
--2.Finding out the distinct debt indicators

We can see there are a total of 124 countries present on the table. As we saw in the first section, there is a column called indicator_name that briefly specifies 
the purpose of taking the debt. Just beside that column, there is another column called indicator_code which symbolizes the category of these debts. Knowing about 
these various debt indicators will help us to understand the areas in which a country can possibly be indebted to.
```sql
SELECT DISTINCT indicator_code AS distinct_debt_indicators
FROM international_debt
ORDER BY distinct_debt_indicators;  "there are total 25 distinct_debt_indicators"
```

--3.Totaling the amount of debt owed by the countries

As mentioned earlier, the financial debt of a particular country represents its economic state. But if we were to project this on an overall global scale, how will we approach it?

Let's switch gears from the debt indicators now and find out the total amount of debt (in USD) that is owed by the different countries. 
This will give us a sense of how the overall economy of the entire world is holding up.

```sql
SELECT 
    ROUND(SUM(debt)/1000000, 2) AS total_debt
FROM international_debt;                                there are total_debt is 3079734.49(in USD)
```
-- 4.Country with the highest debt 

Now that we have the exact total of the amounts of debt owed by several countries, let's now find out the country that owns the highest amount of debt along with the amount. 
Note that this debt is the sum of different debts owed by a country across several categories. 
This will help to understand more about the country in terms of its socio-economic scenarios.
```sql
SELECT  top 1 country_name,FORMAT(SUM(debt)/1000000,'#,##0.00')+' millions' AS [HIGHEST DEBT]
FROM international_debt
GROUP BY country_name
ORDER BY SUM(debt) DESC;                 -- China	285,793.49 millions(in USD) highest debt
```
--5.Average amount of debt across indicators

We now have a brief overview of the dataset and a few of its summary statistics. 
We already have an idea of the different debt indicators in which the countries owe their debts. We can dig even further to find out on an average how much debt a country owes? 
This will give us a better sense of the distribution of the amount of debt across different indicators.
```sql
SELECT 
    indicator_code AS debt_indicator,
    indicator_name,
    AVG (debt) AS average_debt
FROM international_debt
GROUP BY indicator_code,indicator_name
ORDER BY 3 DESC;
```
--6.The highest amount of principal repayments

We can see that the indicator DT.AMT.DLXF.CD tops the chart of average debt. This category includes repayment of long term debts. Countries take on long-term debt to acquire immediate capital.

An interesting insight to be drawn from the above findings is the significant gap between the values of the indicators after the second one. This suggests that the first two indicators are likely to be the most critical categories in terms of the debt liabilities of the countries.
We can investigate this a bit more so as to find out which country owes the highest amount of debt in the category of long term debts (DT.AMT.DLXF.CD). Since not all the countries suffer from the same kind of economic disturbances, this finding will allow us to understand that particular country's economic condition a bit more specifically.
```sql
SELECT 
    country_name, 
    indicator_name
FROM international_debt
WHERE debt= (SELECT 
                 MAX(debt)
             FROM international_debt
             WHERE indicator_code ='DT.AMT.DLXF.CD');   --China has the highest amount of debt in the long-term debt (DT.AMT.DLXF.CD) category.
```
--7.The most common debt indicator
China has the highest amount of debt in the long-term debt (DT.AMT.DLXF.CD) category. This is verified by [The World Bank](https://data.worldbank.org/indicator/DT.AMT.DLXF.CD?end=2018&most_recent_value_desc=true). It is often a good idea to verify our analyses like this since it validates that our investigations are correct.

We saw that long-term debt is the topmost category when it comes to the average amount of debt. But is it the most common indicator in which the countries owe their debt? Let's find that out.

```sql
SELECT 
    indicator_code,
    COUNT (indicator_code) AS indicator_count
FROM international_debt
GROUP BY indicator_code
ORDER BY indicator_count DESC, indicator_code DESC;
```
--8.Other viable debt issues and conclusion
There are a total of six debt indicators in which all the countries listed in our dataset have taken debt. The indicator DT.AMT.DLXF.CD is also there in the list. So, this gives us a clue that all these countries are suffering from a common economic issue.
Let's change tracks from debt_indicators now and focus on the amount of debt again. Let's find out the maximum amount of debt across the indicators along with the respective country names. With this, we will be in a position to identify the other plausible economic issues a country might be going through. By the end of this section, we will have found out the debt indicators in which a country owes its highest debt.
```sql
SELECT top 10
    country_name, 
    indicator_code, 
    MAX(debt) AS maximum_debt
FROM international_debt
GROUP BY country_name,indicator_code
ORDER BY 3 DESC;
```

In this Project,we took a look at debt owed by countries across the globe. We extracted a few summary statistics from the data and unraveled some interesting facts and figures. We also validated our findings to make sure the investigations are correct.

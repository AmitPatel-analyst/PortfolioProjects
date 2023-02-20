### Incredible 120 Years of Olympic Games
Introduction

The modern Olympics represents an evolution of all games from 1986 to 2016. Because the Olympics is an international sports event. It is affected by global issues such as the COVID-19 pandemic, and world wars. Nevertheless, there are positive movements such as women's empowerment and the development of the game itself.

In this project, I used a 120-year-old dataset containing a massive collection of data. I downloaded the data from Kaggle Website.  https://www.kaggle.com/datasets/heesoo37/120-years-of-olympic-history-athletes-and-results
There are total 2 Csv files "athlete_events.csv" and "noc_regions.csv" and I imported the table into MS-SQL Server and created a database in my local machine and saved these 2 tables in the following names.
1) olympics_history
2) Olympics_history_noc_regions

I performed intermediate to advanced SQL queries (Subqueries, CTE, Joins) for better analysis.
First and foremost, I wanted to study the dataset to get answers to the following questions: How many columns and rows are in the dataset? Ans:- ~271K Rows and 15 Columns
How many datasets are there? Ans:- 2 datasets
```sql
select count(1) as Total_rows from  olympics_history;
```
![image](https://user-images.githubusercontent.com/120770473/220054252-f442e35a-c2ff-4c3f-b073-429ee015c327.png)
```sql
select COUNT(*) as Total_Columns
from sys.all_columns
where object_id = (
		select object_id
				from sys.tables
				where name = 'olympics_history');
```
![image](https://user-images.githubusercontent.com/120770473/220054633-fc379b63-483b-4aa1-b0aa-96821aabac74.png)
--------------------------------------------------------------------------------------------------
Derived answers of some 20 questions by writing sql queries.
### Ques-1 How many olympics games have been held?
```sql
select count(distinct games) as total_olympics_games 
from olympics_history
```
![image](https://user-images.githubusercontent.com/120770473/220057463-efee6918-e4c8-4ca5-a756-5af0542cfc43.png)
### Ques-2 Mention the total no of nations who participated in each olympics game
```sql
WITH ALL_COUNTRIES AS 
(
	SELECT		GAMES,NR.REGION AS COUNTRY
	FROM		OLYMPICS_HISTORY AS OH
	JOIN		OLYMPICS_HISTORY_NOC_REGIONS NR ON OH.NOC=NR.NOC
	GROUP BY	GAMES,NR.REGION
)
	SELECT		GAMES,COUNT(1) AS TOTAL_NATIONS_PARTICIPATED
	FROM		ALL_COUNTRIES
	GROUP BY	GAMES
	ORDER BY	GAMES	
```
![image](https://user-images.githubusercontent.com/120770473/220058410-39520caa-ba15-4cdc-b392-a041728ef93c.png)
![image](https://user-images.githubusercontent.com/120770473/220058581-06ba4173-30aa-4ac8-aa12-66ca6178bf22.png)
### Ques-3 Which year saw the highest and lowest no of countries participating in olympics?
```sql
with all_countries as (
select Games,nr.region
from olympics_history as oh
join Olympics_history_noc_regions nr on oh.NOC=nr.NOC
group by games,nr.region
),
tot_countries as(
select Games,count(1) as total_nations_participated
from all_countries
group by Games
)	
select distinct
      concat(first_value(games) over(order by total_nations_participated)
      , ' - '
      , first_value(total_nations_participated) over(order by total_nations_participated)) as Lowest_Countries,
      concat(first_value(games) over(order by total_nations_participated desc)
      , ' - '
      , first_value(total_nations_participated) over(order by total_nations_participated desc)) as Highest_Countries
      from tot_countries
      order by 1;
```   
![image](https://user-images.githubusercontent.com/120770473/220059898-a315859a-269d-4315-8f97-709f1863b373.png)
### Ques-4 Which nation has participated in all of the olympic games?
 ```sql
with tot_games as 
    (
    select count(distinct games) as total_olympics_games 
    from olympics_history),
all_countries as 
    (
    select Games,nr.region as country
    from olympics_history as oh
    join Olympics_history_noc_regions nr on oh.NOC=nr.NOC
    group by games,nr.region
    ),
countries_participated as
    (select country,count(1) as total_participated_games
    from all_countries
    group by country
    )
					
select cp.* 
from countries_participated as cp 
join tot_games as tg
on cp.total_participated_games=tg.total_olympics_games
```
![image](https://user-images.githubusercontent.com/120770473/220060557-33acc892-0c5b-4edb-90ce-a8e81fdbc129.png)

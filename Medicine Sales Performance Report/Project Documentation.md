# Medicine Sales Performance Report
This report provides comprehensive insights and analysis of the sales performance of medicine sold across all 6 countries worldwide from Jan 2020 to Feb 2024. 

### Created and Analyzed by: Amit Patel @Data Analyst [LinkedIn](https://www.linkedin.com/in/amit-patel999/)
### Live Dashboard [Link]()

## Project Objective:    
The objective of this project is to provide the higher management of the pharmaceutical company with comprehensive insights into Medicine sales performance over the specified reporting period.

By analyzing this dataset, the management aims to gain valuable insights into overall sales performance, identify key trends and patterns, and make strategic decisions to optimize future sales strategies. This includes assessing the effectiveness of marketing campaigns, understanding customer purchasing behaviour, and identifying high-demand products to enhance overall profitability and customer satisfaction.

## About Dataset:   
The dataset comprises 3 spreadsheet files in CSV format. Each file represents a different aspect of the dataset: customers, drugs, and sales transactions.       
**1. Sales Table:** Contains detailed records of each sale from **200 individual customers**, including the drug sold, the customer, and the transaction specifics total records are **16314**.    
**2. Drugs Lookup Table:** Contains details about each drug, including pricing and regulatory information.    
**3. Customer Table:** Provides demographic and additional information about each customer.   

## Data Dictionary

### Lookup_Drug Table
| S no. | Column                    | Description                                  | Data Type |
|-------|---------------------------|----------------------------------------------|-----------|
| 1     | DrugID                    | Unique identifier for each drug              | Integer   |
| 2     | CostOfProduction          | Cost incurred to produce the drug            | Decimal   |
| 3     | DrugName                  | Name of the drug                             | String    |
| 4     | RegulatoryComplianceID    | Compliance identifier for regulatory bodies  | Integer   |
| 5     | Treats                    | Conditions treated by the drug               | String    |
| 6     | UnitSalesPrice            | Sale price per unit of the drug              | Decimal   |

### Lookup_Customer Table
| S no. | Column        | Description                           | Data Type |
|-------|---------------|---------------------------------------|-----------|
| 1     | CustomerID    | Unique identifier for each customer   | Integer   |
| 2     | Age           | Age of the customer                   | Integer   |
| 3     | Age Group     | Age group classification of the customer | String    |
| 4     | Country       | Country of the customer               | String    |
| 5     | Country - Copy| Duplicate column for Country          | String    |
| 6     | Full Name     | Full name of the customer             | String    |
| 7     | Gender        | Gender of the customer                | String    |

### Fct_Sales Table
| S no. | Column      | Description                         | Data Type |
|-------|-------------|-------------------------------------|-----------|
| 1     | CustomerID  | Unique identifier for each customer | Integer   |
| 2     | DrugID      | Unique identifier for each drug     | Integer   |
| 3     | SaleDate    | Date of the sale                    | Date      |
| 4     | BuyerType   | Type of buyer (e.g., retail, wholesale) | String    |
| 5     | SaleID      | Unique identifier for each sale     | Integer   |
| 6     | UnitsSold   | Number of units sold                | Integer   |

### Lookup_Date Table (Created new calculated table using DAX language)
| S no. | Column         | Description                                         | Data Type |
|-------|----------------|-----------------------------------------------------|-----------|
| 1     | Date           | Specific date                                       | Date      |
| 2     | Month Year     | Month and Year                                      | String    |
| 3     | MonthName      | Name of the month                                   | String    |
| 4     | MonthNo        | Month number                                        | Integer   |
| 5     | Quarter        | Quarter of the year                                 | Integer   |
| 6     | Weekdayname    | Name of the weekday                                 | String    |
| 7     | Weekdayno      | Number of the weekday                               | Integer   |
| 8     | WeekNum        | Week number of the year                             | Integer   |
| 9     | Year           | Year                                                | Integer   |
| 10    | Date Hierarchy | Hierarchical structure of the date (Year, Quarter, MonthName) | Hierarchy |

## Lookup_Date Table Creation

This DAX code snippet generates a date table (`Lookup_Date`) with various attributes derived from the `SaleDate` column in the `Fct_Sales` table. The date range is dynamically determined based on the minimum and maximum dates in the `Fct_Sales` table.

```DAX
Lookup_Date = 
VAR _StartDate = MIN(Fct_Sales[SaleDate])
VAR _EndDate = MAX(Fct_Sales[SaleDate])
RETURN
ADDCOLUMNS(
    CALENDAR(_StartDate, _EndDate),
    "Year", YEAR([Date]),
    "Quarter", FORMAT([Date], "\Qq"),
    "MonthName", FORMAT([Date], "mmm"),
    "MonthNo", MONTH([Date]),
    "Weekdayno", WEEKDAY([Date], 2),
    "Weekdayname", FORMAT([Date], "ddd"),
    "dayMonth-Num", DAY([Date]), 
    "WeekNum", WEEKNUM([Date], 2)
)
```
## Manage Relationship Details

### Relationships Between Tables
| S no. | From Table | From Column | To Table       | To Column  | Relationship Type |
|-------|------------|-------------|----------------|------------|-------------------|
| 1     | Fct_Sales  | CustomerID  | Lookup_Customer| CustomerID | One-to-Many       |
| 2     | Fct_Sales  | DrugID      | Lookup_Drug    | DrugID     | One-to-Many       |
| 3     | Fct_Sales  | SaleDate    | Lookup_Date    | Date       | One-to-Many       |

### Description of Relationship Types

**One-to-Many Relationship**: Indicates that one record in the "From Table" can relate to multiple records in the "To Table." This is the case for CustomerID, DrugID, and SaleDate, where each can appear multiple times in the Fct_Sales table but only once in their respective lookup tables.

This structure allows for a normalized database design, enabling efficient queries and data integrity across the tables.

## Data Preparation: 
###  1. Column Profiling 
  - Given meaningful names to all columns
  - Removed columns that are not needed in my analysis
  - Merged Firstname & Lastname to make one column named Fullname
  - Created an Age Group Bucket Based on Age value e.g. 20s, 30s, 40s, 50s, 60s, 70s

## Data Model:
![image](https://raw.githubusercontent.com/AmitPatel-analyst/PortfolioProjects/main/Medicine%20Sales%20Performance%20Report/Data%20modeling.jpg)

A simple Star Schema format was used to model the data in Power BI. This model contains a central fact table titled "Fct_Sales" in addition to "Lookup_Customer", "Lookup_Drug", "Lookup_Date" as dimensions.

## Dashboard Overview:
 
I have developed a comprehensive Power BI dashboard report consisting of three pages, each serving a distinct purpose to provide valuable insights from the medicine sales data.  

![Drug PBI report Page 1](https://github.com/user-attachments/assets/09d20d3b-9f94-4eaf-88dd-da0b7b5b0651)     

**Page 1:- Top/Bottom Analysis**     
    The first report page provides a comprehensive overview of Medicine's sales performance with key performance indicators to monitor the following metrics: sales, profit, cogs and quantity sold. Custom KPI card visuals reflect the nominal and percent differences between the Last years and months. The date slicer enables dynamic filtering of the KPI. The field parameter allows the user to toggle between each sales metric to monitor metric performance more closely across the entire date selection period. Another field parameter allows the user to toggle between top and bottom selections based on the number of highlighted bars.      
 
### **Key Performance Indicators (KPIs):**

**- Revenue:** Total income generated from sales. The current value is $4M for February 2021, showing a 21.1% decrease from the previous month. This KPI indicates overall business performance and growth.
**- COGS:** Total money spent on producing medicines. The current value is $753K for February 2021, showing a 23.5% decrease from the previous month. This KPI indicates overall production efficiency.       
**- Quantity:** Total orders processed. The current value is 16K for February 2021, showing a 16.3% decrease from the previous month. This KPI reflects customer demand and operational volume.    
**- Profit** Revenue minus costs. The current value is $3M for February 2021, showing a 20.6% decrease from the previous month. This KPI indicates overall financial health and sustainability.    


![Drug PBI report Page 2](https://github.com/user-attachments/assets/cfbb67fb-a991-494a-bd1f-fe8a3dfac574)

    
**Page 2:- Customer Analysis**      
    The second report page presents customer-related insights and demographic analysis, providing detailed information about customer segments and demographic distribution. The key elements of this page are:    

### **Key Performance Indicators (KPIs):**    
    
Important KPIs are displayed at the top, offering a quick overview of customer-related metrics:    

**- Total Customers:** The total number of unique customers.   
**- Total Medicines:** The total number of unique medicines.     
**- Total Transactions:** The total number of transactions that happened to buy a medicine.     
**- Total Countries:** The total number of unique Countries.   
**- Male Customers & Female Customers:** The total number of Male & Female customers.    
**- Average Revenue per Customer:** The average revenue generated per customer.    
**- Total Revenue:** The total revenue generated.   

#### **Sales by Country (Map Chart):**     
A map chart is provided to display sales distribution by country. Users can interact with this chart to view the top two major contributions to revenue.
    
#### **Revenue by Gender (Doughnut Chart):**     
This chart shows the percentage of revenue contributed by each gender. It helps in understanding gender-wise revenue distribution and identifying key customer segments.    

#### **Revenue by Day (Column Chart):**     
This chart shows the revenue contributed by each day of the week. It helps in understanding Day-wise revenue distribution and identifying Peak Sales Days. 

#### **Revenue Distribution (Bubble Chart):**   
The bubble chart illustrates the daily and weekly revenue distribution. Each bubble represents a day's revenue, with its size indicating the magnitude of the revenue generated.   

**Page 3:- Medicine Details**      
    The third report page displays the details of the medicine, presenting each metric and comparing it against the previous year and Profit margin %. Users can also search for the name using a custom visual( Text filter visual) from the list.   With the help of Drill-through functionality users can further see the performance of each medicine.        
    
![Drug PBI report Page 3](https://github.com/user-attachments/assets/15055603-e3c8-4946-9002-663555495dfe)

![Drug PBI report Page 4](https://github.com/user-attachments/assets/dac11f0f-b6d9-4be1-97d3-4e98b6f2ed66)

       
## Conclusion:        
The detailed analysis of the Medicine Sales Performance Report provides valuable insights into revenue distribution, customer demographics, and geographical contributions. By leveraging these insights, the company can make informed strategic decisions to optimize sales performance, enhance customer satisfaction, and drive future growth.    


## Recommendations for Improving Sales Performance

### Market Analysis

Conduct a detailed market analysis to understand the factors contributing to the sales peak in 2021 and the subsequent decline. Identifying these factors will help in strategizing future sales and marketing efforts.

### Targeted Marketing

Implement targeted marketing campaigns in Canada and Australia to further strengthen these markets. Additionally, explore new marketing strategies to increase penetration in the United States and other countries.

### Sales Stability

Develop strategies to stabilize sales and reduce the extreme fluctuations observed in the yearly sales summary. This could involve diversifying the product range, optimizing pricing strategies, and enhancing customer engagement.

### Continuous Monitoring

Regularly monitor sales performance and market trends to quickly adapt to changes and mitigate any adverse impacts on sales.

    


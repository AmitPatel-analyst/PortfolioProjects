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
  - Merged Firstname & lastname to make one column named Fullname
  - Created an Age Group Bucket Based on Age value e.g. 20s, 30s, 40s, 50s, 60s, 70s

## Data Model:
![image]()

A simple Star Schema format was used to model the data in Power BI. This model contains a central fact table titled "Customer" in addition to "Agegroup", "Creditscoregroup", "Tenuregroup" as dimensions.

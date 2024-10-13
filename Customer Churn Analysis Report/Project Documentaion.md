# Customer-churn-analysis-report
The objective of this report is to analyze customer churn rates across different demographics and regions to identify key areas for improvement. By understanding the factors contributing to churn, the company can develop targeted strategies to enhance customer retention and reduce churn rates.
### Created and Analyzed by: Amit Patel @Data Analyst [LinkedIn](https://www.linkedin.com/in/amit-patel999/)
### Live Dashboard [Link](https://app.powerbi.com/view?r=eyJrIjoiOGI0ZjliMGUtMzdlYi00NDNhLWIwZWEtMDc1ZWQ4ZGJiMGRjIiwidCI6IjA3ZjAxN2QwLWJiNzEtNDliYS1iMTMxLTJkZDkyZWQ3MWE3MiJ9)

## Project Objective:    
The objective of this report is to analyze customer churn rates across different demographics and regions to identify key areas for improvement. By understanding the factors contributing to churn, the company can develop targeted strategies to enhance customer retention and reduce churn rates.    

## About Dataset:   
The dataset comprises customer data, encompassing detailed records of visits from **10000 individual customers**. Each entry in the dataset stores unique information regarding the credit score, salary, country, gender, age and churn status.  

# Customer Table Data Dictionary

## Table: Customer

| **Sno.** | **Column**        | **Description**                                    | **Data Type** |
|----------|--------------------|----------------------------------------------------|---------------|
| 1        | customer_id        | Unique identifier for each customer.               | Integer       |
| 2        | credit_score       | Credit score of the customer.                      | Integer       |
| 3        | country            | Country of residence of the customer.              | String        |
| 4        | gender             | Gender of the customer.                            | String        |
| 5        | age                | Age of the customer.                               | Integer       |
| 6        | tenure             | Number of years the customer has been with the bank.| Integer      |
| 7        | balance            | Balance of the customer's account.                 | Float         |
| 8        | products_number    | Number of products the customer has with the bank. | Integer       |
| 9        | credit_card        | Indicates whether the customer has a credit card.  | Integer       |
| 10       | active_member      | Indicates whether the customer is an active member.| Integer       |
| 11       | estimated_salary   | Estimated salary of the customer.                  | Float         |
| 12       | churn              | Indicates whether the customer has churned.        | Integer       |

### Column Value Definitions

- **gender**: 
  - Male
  - Female

- **credit_card**:
  - 0: No
  - 1: Yes

- **active_member**:
  - 0: No
  - 1: Yes

- **churn**:
  - 0: No
  - 1: Yes

## Data Preparation: 
###  1. Column Profiling 
  - Given meaningful names to all columns
  - Removed columns that are not needed in my analysis
  - Replaced value from 1 to Holding & from 0 to Unholding to Credit card status column
  - Replaced value from 1 to Active & from 0 to Inactive to Activity status column
  - Replaced value from 1 to churned & from 0 to Not churned to Churn status column
  - Created meaningful groups (Agegroup, Creditscoregroup,Tenuregroup)
  - Created queries to organise data for analysis and reporting ( Create a Index column to sort order of Groups )
 
## Data Model:
![image](https://github.com/AmitPatel-analyst/Customer-churn-analysis-report/assets/120770473/ac333e91-df24-4e32-9cdc-b3c43c68e1d0)

A simple Star Schema format was used to model the data in Power BI. This model contains a central fact table titled "Customer" in addition to "Agegroup", "Creditscoregroup", "Tenuregroup" as dimensions.

## Dashborad Overview:
![image](https://github.com/AmitPatel-analyst/Customer-churn-analysis-report/blob/main/Customer%20churn%20analysis%20report.jpg)

## Detailed Insights Explanation:         
### Some Important KPIs       
![image](https://github.com/AmitPatel-analyst/Customer-churn-analysis-report/assets/120770473/0fbe48c2-d657-4bcd-a7d1-329813aeef89)

- **Total Number of Customers**: 
  This KPI represents the total number of customers in the dataset, which is 10,000. It serves as the base for calculating other important metrics such as churn rate and retention rate.

- **Currently Active Customers**: 
  This KPI indicates the number of customers who are currently active, totalling 5,151. This metric helps in understanding the active customer base and planning customer retention strategies.

- **Retained Customers**: 
  This KPI represents the number of customers who have been retained, which is 7,963. Retention is a crucial aspect of customer relationship management, highlighting the effectiveness of retention strategies.

- **Customer Churn Rate**: 
  The churn rate is 20.4%, which shows the percentage of customers who have stopped using the service. This metric is critical for assessing the company's customer retention performance.

### Breakdown of Churn by Country

![image](https://github.com/AmitPatel-analyst/Customer-churn-analysis-report/assets/120770473/c6e19532-32c2-4153-a72d-8fed237f3c01)

The dashboard provides a clear visualization of the churn rate by country:

- **France**: 16.2%
- **Germany**: 32.4%
- **Spain**: 16.7%

This breakdown helps in identifying which countries have higher churn rates, allowing for targeted interventions to reduce churn in specific regions.

### Churn by Age Groups

![image](https://github.com/AmitPatel-analyst/Customer-churn-analysis-report/assets/120770473/f46b2216-9f61-4b55-a4ca-fa21c06120a0)

The bar chart reveals the churn rates across different age groups:

- **18-25**: 7.5%
- **26-35**: 8.5%
- **36-45**: 19.6%
- **46-55**: 50.6%
- **56-65**: 48.3%
- **66+**: 13.3%

Notably, the highest churn rates are observed in the 46-55 and 56-65 age groups, indicating a need for focused retention efforts for these demographics.

### Churn by Tenure Groups   

![image](https://github.com/AmitPatel-analyst/Customer-churn-analysis-report/assets/120770473/597a839c-d230-4d32-b7c7-0a0c9368b1a5)

The bar chart also illustrates churn rates based on customer tenure:

- **0-2 years**: 21.2%
- **3-5 years**: 20.8%
- **6-8 years**: 18.9%
- **9-11 years**: 21.3%

The churn rate is relatively high for customers in their first two years and those with 9-11 years of tenure, suggesting that the company might need to enhance its engagement strategies for these tenure groups.

### Customer List Insights   

![image](https://github.com/AmitPatel-analyst/Customer-churn-analysis-report/assets/120770473/128ac157-369e-4638-9e2e-4c72471ca2ad)

The customer list table provides detailed information about individual customers, including gender, country, age, tenure, credit score, credit rating, and estimated salary. This granular data can be used to perform more specific analyses and identify patterns or correlations that could help in reducing churn.

## Top Recommendations

Based on the insights from the dashboard and the objective of reducing customer churn, here are some top recommendations:

### 1. Targeted Retention Programs for High Churn Age Groups
Implement specialized retention programs aimed at the 46-55 and 56-65 age groups. These could include loyalty rewards, personalized communication, and tailored offers to enhance customer satisfaction and reduce churn.

### 2. Enhanced Onboarding for New Customers
Given the high churn rate among customers in their first two years, improving the onboarding process can help retain these customers. This could involve providing comprehensive onboarding materials, regular check-ins, and early engagement initiatives.

### 3. Country-Specific Interventions
With Germany exhibiting the highest churn rate, country-specific retention strategies should be developed. These could include localized marketing campaigns, better customer support in the local language, and culturally relevant engagement activities.

### 4. Re-engagement Strategies for Long-Tenure Customers
For customers with 9-11 years of tenure, re-engagement strategies such as anniversary rewards, exclusive events, and recognition programs can help retain them.

### 5. Data-Driven Personalization
Utilize the detailed customer data to create personalized experiences. This could involve using predictive analytics to identify at-risk customers and offering them targeted promotions or support to prevent churn.

By implementing these recommendations, the company can effectively reduce churn, improve customer satisfaction, and enhance overall business performance while aligning with its strategic goals.

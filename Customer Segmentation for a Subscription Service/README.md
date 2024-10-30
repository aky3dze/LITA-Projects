# Customer Segmentation for a Subscription Service
<p align="center">
<img src="https://github.com/user-attachments/assets/e8e96962-dabb-4771-ac6d-124b05ed68ed" width="600" height="400">


	
## Table of Contents 

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Data Source and Overview](#data-source-and-overview)
- [Tools and concepts applied](#tools-and-concepts-applied)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data visualization](#data-visualization)
- [Findings](#findings)
- [Conclusions and Recommendations](#conclusions-and-recommendations)
- [Limitations](#limitations)


## Project Overview
This project analyses customer data for a subscription service to identify segments and trends. The report outlines key insights from customer subscription data using Microsoft Excel, SQL queries, and PowerBi. The analysis focuses on various aspects of customer behaviour, such as subscription retention, cancellations, revenue generation, and regional differences.


## Objectives
The analysis aims to:
- Understand customer behaviour
- Track different subscription types
- Identify key trends in cancellations and renewals
- Calculate key business metrics such as customer retention, churn, and revenue
- Provide actionable insights that could help optimise customer engagement strategies
The final deliverable will be a Power BI dashboard visually presenting these insights. 


## Data Source and Overview
This data was obtained from the Ladies in Tech Africa (LITA) capstone project. The data is structured in a single table with the following attributes:

- `CustomerID` – Unique identifier for each customer.
- `CustomerName` – Name of the customer.
- `Region` – The region where the customer is located.
- `SubscriptionType` – Type of subscription (e.g., Basic, Premium, Standard).
- `SubscriptionStart` – Date when the subscription started. m 
- `SubscriptionEnd` – Date when the subscription ended.
- `Canceled` – Whether the subscription was cancelled (True/False).
- `Revenue` – Revenue generated from the customer.


## Tools and concepts applied
The following tools and concepts were used for data processing, analysis and visualization: 
- Microsoft Excel [Download Here](https://www.microsoft.com/es-es/) - Used for initial data cleaning and analysis.
     
- SQL Server - For querying and extracting key insights from the data
  	- The following SQL techniques were used: 
  	 1. Aggregate functions
  	 2. `Case` expression
  	     
- Power BI - For further data analysis, visualization and dashboard creation
	- The following PowerBi features were incorporated:
   	 1. Measures
   	 2. Calculated columns
   	 3. DAX
   	    
- Github - To showcase this project as part of a portfolio 

## Data Cleaning and Preparation
- Data loading and inspection: The raw data was initially loaded in Excel, and checked for missing values, duplicates and consistency in data format.
- Data cleaning and formatting: This involved removing duplicates.
- Calculation of subscription duration (in days) using the Excel formula `= SubscriptionEnd - SubscriptionStart`
- Loading data into SQL server and Power BI; data types were reviewed accordingly.


## Exploratory Data Analysis
````sql
---retrieves all subscription data
select *
from sub
````

**1. Total number of customers from each region**
````sql
select Region, count(distinct CustomerID) as TotalCustomers
from sub
group by Region
````
**Output** 
| Region | TotalCustomers |
| --- | --- |
| East	| 5 | 
| South | 5 |
| North	| 5 |
| West	| 5 |


**2. Most popular subscription type by the number of customers**
````sql
select top 1 SubscriptionType, count(distinct CustomerID) as CustomerCount
from sub
group by SubscriptionType
````
**Output** 
| SubscriptionType | CustomerCount |
| --- | --- |
| Basic	| 10 |
	

**3. Customers who cancelled their subscription within 6 months**
````sql 
select distinct CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd 
from sub
where Canceled = 1 and DATEDIFF(month, SubscriptionStart, SubscriptionEnd)  <=6
````
**Output** 
No customer cancelled their subscription within 6 months.


**4. Calculate the average subscription duration for all customers**
````sql
--in days
select Avg(DATEDIFF(day, SubscriptionStart, SubscriptionEnd)) as AvgSubscriptionDurationDays
from sub

--in months
select Avg(DATEDIFF(month, SubscriptionStart, SubscriptionEnd)) as AvgSubscriptionDurationMonths
from sub
````
**Output** 
| AvgSubscriptionDurationDays |
| --- |
| 365	|

| AvgSubscriptionDurationMonths |
| --- |
| 12	|


**5. Customers with subscriptions longer than 12 months**
````sql 
select distinct CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd 
from sub
where DATEDIFF(month, SubscriptionStart, SubscriptionEnd) >12
````
**Output** 
No customer had their subscription longer than 12 months.


**6. Total revenue by subscription type**
````sql
select SubscriptionType, sum(Revenue) as TotalRevenue 
from sub
group by SubscriptionType
````
**Output** 
| SubscriptionType | TotalRevenue  |
| --- | --- |
| Basic	| 33776735 |
| Premium	| 16899064 |
| Standard	| 16864376 |
	

**7. Top 3 regions by subscription cancellations** 
````sql
select top 3 Region, count(CustomerID) as CanceledSubscriptions 
from Sub
where Canceled = 1
group by Region 
order by CanceledSubscriptions desc
````
**Output** 
| Region | CanceledSubscriptions |
| --- | --- |
| North	| 5067 |
| South | 5064 |
| West	| 5044 |


**8. Total number of active and canceled subscriptions** 
````sql
-- Active subscriptions are those where Canceled = 0 (False).
-- Canceled subscriptions are those where Canceled = 1 (True).

Select 
    sum(case when Canceled = 0 then 1 else 0 end) as ActiveSubscriptions,
    sum(case when Canceled = 1 then 1 else 0 end) as CanceledSubscriptions
from sub
````
**Output** 
| ActiveSubscriptions | CanceledSubscriptions |
| --- | --- |
| 18612	| 15175 |


**9. Number of cancellations in each region by subscription type**
````sql
Select Region, SubscriptionType,
       count(CustomerID) as TotalSubscriptions, 
       sum(case when Canceled = 1 then 1 else 0 end) as  CanceledSubscriptions
from sub
group by Region, SubscriptionType
order by TotalSubscriptions desc
````
**Output** 
| Region | SubscriptionType | TotalSubscriptions | CanceledSubscriptions |
| --- | --- | --- | --- |
| East | Basic | 8488 | 0 | 
| South | Premium | 8446 | 5064 |
| North	| Basic | 8433 | 5067 | 
| West | Standard | 8420 | 5044 | 	



**10. Churn rate by subscription type**
````sql
Select SubscriptionType, 
       count(CustomerID) as TotalSubscriptions, 
       sum(case when Canceled = 1 then 1 else 0 end) as  CanceledSubscriptions,
       (sum(case when Canceled = 1 then 1 else 0 end) * 100.0 / count(CustomerID)) as ChurnRate
from sub
group by SubscriptionType
````
**Output** 
| SubscriptionType | TotalSubscriptions | CanceledSubscriptions | ChurnRate |
| --- | --- | --- | --- |
| Basic	| 16921 | 5067 | 29.945038709296 |
| Premium | 8446 | 5064 | 59.957376272791 |
| Standard | 8420 | 5044 | 59.904988123515 |	


**11. Revenue generated from each customer**
````
select distinct CustomerID, sum(Revenue) as TotalRevenuePerCustomer
from sub
group by CustomerID
order by TotalRevenuePerCustomer desc
````
**Output** 
| CustomerID | TotalRevenuePerCustomer |
| --- | --- |
| 211	| 3437444 |
| 207	| 3427436 |
| 218	| 3414995 |
| 220	| 3399895 |
| 212	| 3398288 |
| 202	| 3395374 |
| 216	| 3385349 | 
| 210	| 3384539 |
| 201	| 3378897 |
| 203	| 3377675 |
| 217	| 3376796 |
| 209	| 3365221 |
| 215	| 3361350 |
| 214	| 3357269 |
| 219	| 3354858 |
| 208	| 3354682 |
| 213	| 3351225 |
| 206	| 3346887 |
| 205	| 3345833 |
| 204	| 3326162 |


**12. Number of subscriptions per customer**
````sql
select distinct CustomerID, count(CustomerID) as NumberofSubscriptions
from sub
group by CustomerID
order by NumberofSubscriptions desc
````
**Output** 
| CustomerID | NumberofSubscriptions |
| --- | --- |
| 211	| 1718 |
| 207	| 1714 |
| 212	| 1700 |
| 218	| 1699 |
| 220	| 1695 |
| 202	| 1693 |
| 201	| 1693 |
| 213	| 1692 |
| 210	| 1692 |
| 217	| 1690 |
| 203	| 1690 |
| 216	| 1687 |
| 215	| 1686 |
| 209	| 1685 |
| 214	| 1683 |
| 219	| 1680 |
| 206	| 1679 |
| 208	| 1676 |
| 205	| 1673 |
| 204	| 1662 |


**13. Average number of subscriptions per customer**
````sql
select count(CustomerID)/count(distinct CustomerID) as AvgNumberofSubscriptions
from sub
````
**Output** 
| AvgNumberofSubscriptions | 
| --- | 
| 1689	|


## Data visualization
The PowerBi dashboard provides an interactive interface, allowing for filtering (Figure 1) based on whether or not a subscription was cancelled (Figures 2 and 3) and viewing trends by customer segments, thus region and subscription type.

![Screenshot 2024-10-29 000243](https://github.com/user-attachments/assets/4277160a-1231-406f-bc06-f2baf8e25ac5)
**Figure 1**
<br>

![Screenshot 2024-10-29 000449](https://github.com/user-attachments/assets/a464c939-127b-4355-9f61-74c4b08c6941)
**Figure 2**
<br>

![Screenshot 2024-10-29 000514](https://github.com/user-attachments/assets/c1d2e8a3-7f4e-4d4a-8d28-9f7f0b0ad1b1)
**Figure 3**
<br>


## Findings
**1. Customers from each region**
The customer distribution is equal across the different regions, suggesting a balanced market reach.


**2. Popularity and total revenue generated based on subscription type**
Basic subscription is the most popular, with 10 customers choosing it over Premium and Standard.  This higher preference suggests that many customers are more inclined towards cost-effective plans which meet their basic needs.

Additionally, Basic subscription generates the most revenue, **33,776,735**, followed by Premium and Standard. 


**3. Customers who cancelled their subscription within 6 months**
No customer cancelled their subscriptions within the first 6 months. This may indicate a satisfactory initial onboarding experience among customers, hence the absence of early churn.


**4.Average subscription duration**
The average subscription duration is approximately 365 days (12 months), which indicates that customers completed an annual subscription cycle before deciding to cancel or renew. This indicates a somewhat stable customer base as most customers within the period.


**5. Customers with subscriptions longer than 12 months**
No customer had their subscription longer than 12 months.
The lack of customer subscriptions beyond 12 months, may suggest that:
- The data was gathered at the end of the annual subscription period
- There is a need for long-term subscriptions, 2 or 5 years, apart from annual subscriptions. These long-term plans could come with incentives and discounts.


**7. Top 3 regions by subscription cancellations** 
The North has the highest number of cancelled subscriptions, followed by the South region. 

**8. Total number of active and canceled subscriptions**
Active subscriptions are higher than the cancelled subscriptions, reflecting a relatively higher retention rate. The higher number of cancellations is a cause for concern and so measures should be put in place to improve the value of services offered as well as customer engagement.

**9. Churn rate in each region**
High churn rate in the North, South and West regions may indicate a need for targeted retention strategies and efforts.


**10. Churn rate by subscription**
Premium and Standard subscription plans experienced a higher churn rate, implying that customer expectations were unmet. Thus, there was a misalignment between their perceived expectations of these higher-tier subscriptions and what they received.

**11. Revenue generated from each customer**
Customers contributing significantly to the overall revenue could be introduced to a loyalty program or exclusive offers to retain them.

**12. Customer by number of subscriptions**



**13. Average number of subscriptions per customer**
The average number of subscriptions per customer gives a general overview of customer engagement.


## Conclusions and Recommendations 
- Implement targeted customer retention strategies in regions North, South, and West
- Incentives or strategies to encourage customers on basic subscriptions to go for higher-tier plans
- Implement long-term plans
- Introduce loyalty programs



## Limitations
- The dataset is limited to one table with a single subscription period, and no demographic data. Thus, customer behaviour across different seasons may not be fully captured in the analysis. Additionally, the effects of demographic patterns could enhance our understanding of churn and retention rates.







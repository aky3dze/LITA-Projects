# Customer-Segmentation-for-a-Subscription-Service
<p align="center">
<img src="https://github.com/user-attachments/assets/e8e96962-dabb-4771-ac6d-124b05ed68ed" width="600" height="400">


	
## Table of Contents 

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Data Source and Overview](#data-source-and-overview)
- [Tools](#tools)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data visualization](#data-visualization)
- [Findings](#findings)
- [Conclusions and Recommendations](#conclusions-and-recommendations)
- [Limitations](#limitations)


## Project Overview
For this project, I will analyse customer data for a subscription service to identify segments and trends. The report outlines key insights derived from customer subscription data using Microsoft Excel, SQL queries, and PowerBi. The analysis focuses on various aspects of customer behaviour, such as subscription retention, cancellations, revenue generation, and regional differences.


## Objectives
The analysis aims to:
- Understand customer behaviour
- Track different subscription types
- Identify key trends in cancellations and renewals
- Calculate key business metrics such as customer retention, churn, and revenue
- Provide actionable insights that could help optimise customer engagement strategies
- The final deliverable will be a Power BI dashboard that presents my analysis. 


## Data Source and Overview
This data was obtained from the Ladies in Tech Africa (LITA) capstone project file. The data is structured in a single table with the following attributes:

- `CustomerID` – Unique identifier for each customer.
- `CustomerName` – Name of the customer.
- `Region` – The region where the customer is located.
- `SubscriptionType` – Type of subscription (e.g., Basic, Premium, Standard).
- `SubscriptionStart` – Date when the subscription started.
- `SubscriptionEnd` – Date when the subscription ended.
- `Canceled` – Whether the subscription was canceled (True/False).
- `Revenue` – Revenue generated from the customer.


## Tools and concepts applied
the following tools and concepts were used for data processing, analysis and visualization: 
- Microsoft Excel [Download Here](https://www.microsoft.com/es-es/) - for data cleaning and initial analysis
     
- SQL server - for querying and extracting key insights
  	- The following SQL 
  	 1. Aggregate functions
  	 2. Case expression
  	     
- PowerBi - for data visualization and dashboard creation
	- The following PowerBi features were incorporated:
   	 1. Measures
   	 2. Calculated columns
   	 3. DAX
   	    
- Github - to showcase this project as part of a portfolio 

## Data Cleaning and Preparation
data loading and inspection: the raw data was loaded first in excel 
data cleaning and formatting


## Exploratory Data Analysis
````sql
---retrieves all subscription data
select *
from sub
````

**1. total number of customers from each region**
````sql
select Region, count(distinct CustomerID) as TotalCustomers
from sub
group by Region
````
**Results** 
| Region | TotalCustomers |
| --- | --- |
| East	| 5 | 
| South | 5 |
| North	| 5 |
| West	| 5 |

The customer distribution is equal across the different regions. 


**2. most popular subscription type by the number of customers**
````sql
select top 1 SubscriptionType, count(distinct CustomerID) as CustomerCount
from sub
group by SubscriptionType
````
**Results** 
| SubscriptionType | CustomerCount |
| --- | --- |
| Basic	| 10 |

The basic subscription is the most popular among customers with 10 subscribers, indicating a higher preference for basic subscription services.
	

**3. customers who cancelled their subscription within 6 months**
````sql 
select distinct CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd 
from sub
where Canceled = 1 and DATEDIFF(month, SubscriptionStart, SubscriptionEnd)  <=6
````
**Results** 
*No customer cancelled their subscription within 6 months.*


**4. calculate the average subscription duration for all customers**
````sql
--in days
select Avg(DATEDIFF(day, SubscriptionStart, SubscriptionEnd)) as AvgSubscriptionDurationDays
from sub

--in months
select Avg(DATEDIFF(month, SubscriptionStart, SubscriptionEnd)) as AvgSubscriptionDurationMonths
from sub
````
**Results** 
| AvgSubscriptionDurationDays |
| --- |
| 365	|

| AvgSubscriptionDurationMonths |
| --- |
| 12	|

The average subscription duration is approximately 365 days (12 months), which indicates a healthy duration as most customers stayed as subscribers for at least one year.

**5. customers with subscriptions longer than 12 months**
````sql 
select distinct CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd 
from sub
where DATEDIFF(month, SubscriptionStart, SubscriptionEnd) >12
````
**Results** 
*No customer had their subscription longer than 12 months.*


**6. total revenue by subscription type**
````sql
select SubscriptionType, sum(Revenue) as TotalRevenue 
from sub
group by SubscriptionType
````
**Results** 
| SubscriptionType | TotalRevenue  |
| --- | --- |
| Basic	| 33776735 |
| Premium	| 16899064 |
| Standard	| 16864376 |
	
Basic subscription which is the most popular amongst customers also generated the most revenue. 

**7. top 3 regions by subscription cancellations** 
````sql
select top 3 Region, count(CustomerID) as CanceledSubscriptions 
from Sub
where Canceled = 1
group by Region 
order by CanceledSubscriptions desc
````
**Results** 
| Region | CanceledSubscriptions |
| --- | --- |
| North	| 5067 |
| South | 5064 |
| West	| 5044 |

The North has the highest number of cancelled subscriptions, followed by the South region. 

**8. total number of active and canceled subscriptions** 
````sql
-- Active subscriptions are those where Canceled = 0 (False).
-- Canceled subscriptions are those where Canceled = 1 (True).

Select 
    sum(case when Canceled = 0 then 1 else 0 end) as ActiveSubscriptions,
    sum(case when Canceled = 1 then 1 else 0 end) as CanceledSubscriptions
from sub
````
**Results** 
| ActiveSubscriptions | CanceledSubscriptions |
| --- | --- |
| 18612	| 15175 |

## Data visualization


## Findings


## Conclusions and Recommendations 



## Limitations







# Customer-Segmentation-for-a-Subscription-Service
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
**Output** 
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
**Output** 
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
**Output** 
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
**Output** 
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
**Output** 
*No customer had their subscription longer than 12 months.*


**6. total revenue by subscription type**
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
	
Basic subscription which is the most popular amongst customers also generated the most revenue. 

**7. top 3 regions by subscription cancellations** 
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
**Output** 
| ActiveSubscriptions | CanceledSubscriptions |
| --- | --- |
| 18612	| 15175 |

--churn rate in each region
````sql
Select Region, 
       count(CustomerID) as TotalCustomers, 
       sum(case when Canceled = 1 then 1 else 0 end) as  CanceledCustomers,
       (sum(case when Canceled = 1 then 1 else 0 end) * 100.0 / count(CustomerID)) as ChurnRate
from sub
group by Region
````
**Output** 
| ActiveSubscriptions | CanceledSubscriptions |
| --- | --- |
| 18612	| 15175 |
Region	TotalCustomers	CanceledCustomers	ChurnRate
North	8433	5067	60.085378868729
East	8488	0	0.000000000000
South	8446	5064	59.957376272791
West	8420	5044	59.904988123515


--churn rate by subscription
````sql
Select SubscriptionType, 
       count(CustomerID) as TotalCustomers, 
       sum(case when Canceled = 1 then 1 else 0 end) as  CanceledCustomers,
       (sum(case when Canceled = 1 then 1 else 0 end) * 100.0 / count(CustomerID)) as ChurnRate
from sub
group by SubscriptionType
````
**Output** 
| ActiveSubscriptions | CanceledSubscriptions |
| --- | --- |
| 18612	| 15175 |
SubscriptionType	TotalCustomers	CanceledCustomers	ChurnRate
Basic	16921	5067	29.945038709296
Premium	8446	5064	59.957376272791
Standard	8420	5044	59.904988123515

--Revenue generated from each customer
````
select distinct CustomerID, sum(Revenue) as TotalRevenuePerCustomer
from sub
group by CustomerID
order by TotalRevenuePerCustomer desc
````
**Output** 
| CustomerID | TotalRevenuePerCustomer |
| --- | --- |
| 18612	| 15175 |
211	3437444
207	3427436
218	3414995
220	3399895
212	3398288
202	3395374
216	3385349
210	3384539
201	3378897
203	3377675
217	3376796
209	3365221
215	3361350
214	3357269
219	3354858
208	3354682
213	3351225
206	3346887
205	3345833
204	3326162

--customer by number of subscription
````sql
select distinct CustomerName, count(CustomerID) as NumberofSubscriptions
from sub
group by CustomerName
order by NumberofSubscriptions desc
````
**Output** 
| CustomerName | NumberofSubscriptions |
| --- | --- |
| Liam	| 1718 |
| Mike	| 1714 |
| Anna	| 1700 |
| Sophia| 1699 |
| Nina	| 1695 |
| Jane	| 1693 |
| John	| 1693 |
| Eva	| 1692 |
| Chris	| 1692 |
| Rob	| 1690 |
| Alex	| 1690 |
| Grace	| 1687 |
| Paul	| 1686 |
| Tom	| 1685 |
| Zoe	| 1683 |
| Dan	| 1680 |
| Ella	| 1679 |
| Sara	| 1676 |
| James	| 1673 |
| Maria	| 1662 |

211	1718
207	1714
212	1700
218	1699
220	1695
202	1693
201	1693
213	1692
210	1692
217	1690
203	1690
216	1687
215	1686
209	1685
214	1683
219	1680
206	1679
208	1676
205	1673
204	1662

--avg number of subscription
````sql
select count(CustomerID)/count(distinct CustomerID) as AvgNumberofSubscriptions
from sub
````
**Output** 
| AvgNumberofSubscriptions | 
| --- | 
| 1689	|

## Data visualization
![Screenshot 2024-10-28 004111](https://github.com/user-attachments/assets/91f9ad7c-e8e4-4195-ad07-26e290130c56)


## Findings


## Conclusions and Recommendations 



## Limitations







# Human Resources (HR) Attrition Analysis
<p align="center">

<img src="https://github.com/user-attachments/assets/6c163380-696d-4b70-a55e-e3429c70b4e6" width="800" height="400">

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Data Source and Overview](#data-source-and-overview)
- [Tools and concepts applied](#tools-and-concepts-applied)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Data visualization](#data-visualization)
- [Findings](#findings)
- [Conclusions and Recommendations](#conclusions-and-recommendations)

## Project Overview 
This project analyses an HR attrition dataset to identify key factors contributing to employee turnover. High attrition rates can lead to increased costs and loss of valuable knowledge within an organization, making it crucial for HR teams to understand and address the drivers behind employee departures.


## Objectives
- Identify key factors influencing employee attrition, such as job satisfaction, work environment, and compensation.
- Provide actionable insights to help the HR department create targeted strategies for improving employee retention.


## Data Source and Overview
This data was obtained from the Ladies in Tech Africa (LITA) course. The dataset includes attributes such as employee demographics, performance ratings, and attrition status. It is available in the file list above.


## Tools and concepts applied
- **Power BI** - for data analysis, visualization and dashboard creation
	- Concepts applied:
   	 1. Measures
   	 2. Calculated columns
   	 3. DAX functions (e.g. `SUM`, `AVERAGE`), etc.
   	    

## Data Cleaning and Preparation
Data was efficiently cleaned and transformed with the PowerQuery editor in Power BI. Some of the applied steps include:
- Making first rows as headers
- Adding conditional columns to
   - assign labels to numeric responses such as job satisfaction, work-life balance, etc.
   - define age and salary brackets
   - assign numeric values to the YES and NO responses of attrition.
- Crosschecking datatypes and changing them when there is a need


## Data visualization
The Power BI dashboard provides an interactive interface, allowing for filtering (Figures 1 - 5) based on job role and education field.

- 🔗[Power BI link](https://app.powerbi.com/links/fRqM2Pc3UJ?ctid=3f227dba-f3f4-4544-b314-c6efd30e0d00&pbi_source=linkShare&bookmarkGuid=4fc449eb-c7d0-42a1-b57f-c70f72ea32be)

  
![Screenshot 2024-11-04 160059](https://github.com/user-attachments/assets/f6ed2cc0-58f4-4780-9255-b1b19ee18dca)
**Figure 1**

![Screenshot 2024-11-04 160123](https://github.com/user-attachments/assets/ed867c8e-b627-41e8-b59f-07403bc7d71d)
**Figure 2**

![Screenshot 2024-11-04 160142](https://github.com/user-attachments/assets/aed06b9e-d211-4c65-9367-529d76ba61af)
**Figure 3**

![Screenshot 2024-11-04 160241](https://github.com/user-attachments/assets/5280a0aa-5a87-439d-bbc1-b1ffb3c825d4)
**Figure 4**

![Screenshot 2024-11-04 160946](https://github.com/user-attachments/assets/b8a20914-a814-4917-9fbb-3066c31c56a9)
**Figure 5**


## Findings
_**Summary: 1470 total employees, 237 exited, attrition rate: 16.12%**_

1. **Demographics:**
   - Sex and Age: Of the 237 employees who left, 150 were males, and 112 fell within the 25 - 34 age bracket. why???
   - Marital status: The majority of employees who left were single (120) and 84 were married. This may suggest that single employees who may have fewer commitments are more open to exploring or seeking more opportunities, unlike their married colleagues who may seek some sort of stability.


2. **Departmental Trends:**
   - Research and development experienced the highest attrition, with 133 employees leaving. This may be indicative of an internal problem such as role-specific challenges, poor work conditions and environment, low salary, etc that may need to be addressed
   - High turnover was observed among Lab Technicians (62), Sales Executives (57), and Research Scientists (47).

3. **Educational background:**
   - Degree level: Employees with a Bachelor's degree (BSc) formed the largest part of those who exited (99), followed by 58 who had a Master's (MSc). Only a few with PhD left. This may suggest that employees with BSc. exited to pursue higher degrees or in pursuit of career advancement opportunities.
   - Field of study: The life sciences and medical fields saw the highest attrition, 89 and 63 respectively, suggesting that the expectations of employees were not being met.

4. **Work-Life Balance and Job Satisfaction:**
   - Although 127 departing employees reported being 'satisfied' with their work-life balance,  58 were dissatisfied and 25 were very dissatisfied. This iterates that a healthy work-life balance alone might not be sufficient for retention. Other factors should be considered.
   - Interestingly, 73 of them were generally satisfied with the job. However, the majority were either dissatisfied or very dissatisfied (66 and 46 respectively). Implying that the majority were not pleased with their jobs.

5. **Work environment satisfaction:**
   - A considerable number of departing employees were very dissatisfied (72) or dissatisfied (43) with the work environment. Even though the other half were either satisfied or very satisfied, there is still the need  to address a poor work environment due to interpersonal conflicts between employees, limited resources and the lack of career progression. 

6. **Tenure and role tenure:**
   - Surprisingly, 102 employees left within their first two years of working at the company and 152 left within two years in their specific role, implying that roles may not have been clearly defined for new employees.
   - More than half of those who left were in entry-level roles. This may suggest that mentorship and training for early career employees should be reviewed and may need greater focus. 

7. **Overtime and workload:**
   - Another contributor to attrition was working overtime as 127 ex-employees regularly worked overtime. This suggests that there may be lots of work to be done by a few employees, which may eventually lead to stress and burnout.

8. **Salary:** 
   - Monthly income played a role in attrition since 137 of those who left earned between 1,000 and 4,000. This raises the concern of not receiving their role's worth and should therefore be reviewed accordingly.

9. **Distance to the workplace:**
   - Distance is not a major factor in attrition since 144 employees who left lived near the workplace.

10. **Business travel:** 
    - Travel frequency does not appear to be a factor in attrition since the majority who left rarely travelled for work. Although business travel may come with some bonuses, it may not directly influence retention in the workplace.



## Conclusions and Recommendations
The following conclusions can be drawn from these findings:
- Younger employees, particularly males and singles, show higher rates of attrition.
- High turnover in R&D and specific roles like Lab Techs, Sales executives and Research scientists.
- Monthly income, work environment, and working overtime greatly impact attrition.
- Entry-level employees are more likely to leave.
- Attrition is high within the first two years of employment.
  
Based on the findings, these recommendations can be made:
- Increase salaries to reduce attrition.
- Review workload and overtime practices.
- Address concerns with the work environment.
- Targeted retention strategies for specific roles and departments should be implemented.
- Thorough orientation and training programs for new hires as well as entry-level employees.
- Introduce career development programs for younger employees.

By implementing these recommendations the company can reduce attrition, foster a healthy work environment and improve job satisfaction.

😊
💻
👩‍💼

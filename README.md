# Jay-Kalantar-Capstone Project: Final Report



## Objective:   
Unanticipated overtime (OT) costs are a common problem for many service sector businesses, as they can erode their profit margins and affect their employees' well-being. To help them address this problem, I applied various machine learning methods to determine the main factors that can forecast the risk of overtime occurrence. This study can offer our clients valuable insights and suggestions on how to improve their workforce management and reduce overtime costs.




## Data Understanding:
### Our system collects time entries by the users and converts them to calculated pay data.  The following datasets describe most of the transactional activities in the system: 
**Timecards**– Employee’s Time IN/OUT with all associated fields (e.g., Emp No, Location, Position, ….)  
**Audits** – Archive of timecard adjustments (e.g., Original Time IN, Current Time IN, …)  
**Timesheets** – Employee’s calculated pay (e.g., REG Pay, Overtime Pay, Expenses, … )  
**Budgets / Schedules** – Planned Budget or attendance for the upcoming timecards.  


These datasets provide the underlying data that form the basis of the feature engineering for analysis:  
**OPEN punches** - List of punches with IN and/or OUT added by a manager  
**Time Changed punches** - List of punches with time change (in minutes)  
**Miss Punches** - List of punches with missed FP, IVR, Face or GPS, Schedule, …  
**Correction Lags** - list of punch correction lag times in hours for any modified punch  


### Output variable (desired target):  
**OT Hours** – Employee’s OT Occurance (0/1)


## Data Preparation
First, data cleanups were performed to remove irrelevant or inaccurate data, such as data added after the pay period, PTO data, and rows without time entries.  Next, feature engineering is done to create new variables and metrics from the existing data, such as the number of punches per day, total REG and OT hours per day, the budget by day-of-week, the correction counts and lag hours, and the combination of punches and correction lags. Finally, all the data sources are consolidated into a single dataframe for further analysis and modeling.

Our analysis does not consider the particularities of each client, but rather the common factors that affect their performance. This way, I can draw findings that are applicable to all of them.



## Models
A comparative analysis of different machine learning models for predicting overtime occurrence was performed. The dataset was highly unbalanced, with only 3% of the cases having overtime occurrence. Therefore, high Precision and Recall scores were needed to accurately identify overtime cases and reduce false positives and negatives. After tuning, Decision Tree and Logistic Regression models showed good performance on this task. The most important features for predicting overtime occurrence were also identified based on the feature importance scores of the models.


## Summary of the Findings

Our analysis of different machine learning models shows that tuned Decision Tree or Logistic Regression models can perform well in predicting overtime occurrence. Both models showed high Precision and Recall scores, meaning they can correctly classify overtime occurrence cases and minimize false positives and negatives. I also identified the most influential features that affect overtime occurrence, based on the feature importance scores of the models. The features that have a positive correlation with overtime are:

**High percentage of incomplete or open punches**: This feature measures the percentage of punches that are not properly recorded or closed by the employees. A high value of this feature indicates a lack of compliance or awareness of the punching compliance, which may lead to overtime occurrence.

**Higher number of daily punches by the same employee**: This feature measures the number of punches per day by each employee. A high value of this feature indicates a high frequency or intensity of work, which may increase the likelihood of overtime occurrence.

**High percentage of time changes**: This feature measures the percentage of punches modified or corrected by the supervisors. A high value of this feature indicates a high variability or uncertainty in the working hours, which can result in overtime occurrence.

**High correction lag**: This feature measures the average number of days between the date of a punch exception and the date of its correction. A high value of this feature indicates a delay or inefficiency in resolving the punch exceptions, which may cause overtime occurrence.

**Higher number of supervisors per employee**: I determined the number of supervisors based on who made the daily corrections for each employee.  A higher number may indicate lack of direct supervision that may lead to higher overtime occurrence.

The factors that have a negative correlation with overtime are:

**Number of employees**: This feature measures the number of employees who perform the same task or belong to the same group. A low value of this feature indicates a low availability or redundancy of resources, which may increase the demand or pressure on the existing employees, leading to overtime occurrence.

These findings can help managers and supervisors monitor and control these factors and reduce the risk of overtime occurrence.



## Next steps and Model Impovements:
We need a data-driven approach to help our clients minimize the expenses associated with paying overtime to their employees. We can use time-series analysis methods such as ARMA or LSTM to model the patterns and trends of overtime over time and predict future overtime levels. This can provide our clients with actionable insights and recommendations on how to optimize their workforce management and reduce overtime costs.

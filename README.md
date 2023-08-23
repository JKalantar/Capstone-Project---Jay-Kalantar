# Jay-Kalantar-Capstone Project: Initial Report and Exploratory Data Analysis (EDA)



## Objective:   
### My objective is to leverage Machine Learning Models to improve payroll processes and reduce costs for our clients.  My initial focus is to identify the leading indicators for Overtime work and then attempt to predict Overtime occurrences. 


## Data Understanding:
### Our system collects time entries by the users and converts them to calculated pay data.  The following datasets describe most of the transactional activities in the system: 
**Timecards**– Employee’s Time IN/OUT with all associated fields (e.g., Emp No, Location, Position, ….)  
**Audits** – Archive of timecard adjustments (e.g., Original Time IN, Current Time IN, …)  
**Timesheets** – Employee’s calculated pay (e.g., REG Pay, Overtime Pay, Expenses, … )  
**Budgets / Schedules** – Planned Budget or attendance for the upcoming timecards.  
**Employees** – Employee demographics such as the hire dates, base salary, and positions  
**Managers** – Manager details such as title, number of employees, and locations they manage  

These datasets provide the underlying data that form the basis of the feature engineering for analysis:  
**OPEN punches** - List of punches with IN and/or OUT added by a manager  
**Time Changed punches** - List of punches with time change (in minutes)  
**Miss Punches** - List of punches with missed FP, IVR, Face or GPS, Schedule, …  
**Correction Lags** - list of punch correction lag times in hours for any modified punch  


### Output variable (desired target):  
**%OT** – Employee’s calculated Percent Overtime [ $OT/($REG + $OT) ]


## Data Preparation:
1) Count Punches from from Timecards
2) Create %OT KPI calculation from Timesheets
3) Calculate Correction Counts and Lag Hours from Correction Lags
4) Combine Punches and Correction lags
5) Combine with Timesheet Data
6) Select specific features
7) Replaced unknown with NaN values with zero
8) One-Hot encodes all object features
9) Split Train / Test (30%)
10) Scaled numerical fields


## Summary of the Findings

### Regression Models
* Random Forest followed by Gradient Boost provide the best scores but they also run much slower than other models

### Classification Models
* There is only around 3% overtime, so our data is imbalanced.  We are using Precision and Recall to score and optimize our models
* Random Forest and Gradient Boost provide the best Precision but the Decision Tree provides the best Recall

### Both Regression and classification models show the following Feature importance:
1. REG_Hours:  As more hours are associated with a Position the probability of %OT goes up.  These active positions approch 40 hrs/wk more quickly resulting in higher OT incidence.
2. DayOfWeek:  This is expected. As employees approach the 40 hrs/wk later in the week, they are more prone to result in OT
3. Miss_Punch Corr Lag: Employees whose Timecards are unapproved for a long time will prevent the manager from noticing their hours are approaching 40 hours.
4. Open_Punch Corr Lag: Employees whose Timecards are incomplete for a long time will prevent managers from noticing their hours are approaching 40 hours.
5. Specific Positions -  This seems to be due to colinearity the Feature


## Next steps and Model Improvements:
1. Feature engineering.  Add more features such as hire date, pay rate, state, employment statistics, and employee demographic (age, gender, ...) to see if they have any impact on Overtime.
2. Add more data from different clients to confirm the finding
3. Remove features with strong colinearity
4. Try other modeling techniques such as Ensemble models that combine multiple algorithms to improve performance.
5. Tune the hyperparameters of the best-performing classifier

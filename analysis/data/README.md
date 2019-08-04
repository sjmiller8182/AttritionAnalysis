# Data

This folder contains the data used for the analysis.

## Data Files

 * [`CaseStudy2-data_train.csv`](https://github.com/sjmiller8182/AttritionAnalysis/blob/master/analysis/data/CaseStudy2-data_train.csv): A complete set of data. The analysis is performed on this dataset.
 * [`CaseStudy2CompSetNoAttrition_test.csv`](https://github.com/sjmiller8182/AttritionAnalysis/blob/master/analysis/data/CaseStudy2CompSetNoAttrition_test.csv): A set of data with the response (attrition) removed. This set will be used by an external pary to access the provided model for predicting attrition.
 * [`CaseStudy2CompSetNoSalary_test.csv`](https://github.com/sjmiller8182/AttritionAnalysis/blob/master/analysis/data/CaseStudy2CompSetNoSalary_test.csv): A set of data with the response (salary) removed. This set will be used by an external pary to access the provided model for predicting attrition.

## Features

### Summary

There are three types of variables in this data set: factor, continuous, and stationary. The types of variables are listed below.

#### Factor Variables

* Attrition  (response variable)
* BusinessTravel
* Department
* Education
* EducationField
* EmployeeNumber
* EnvironmentSatisfaction
* Gender
* JobInvolvement
* JobLevel
* JobRole
* JobSatisfaction
* MaritalStatus
* Overtime
* PerformanceRating
* RelationshipSatisfaction
* StockOptionLevel
* WorkLifeBalance

#### Continuous Variables

* DailyRate
* DistanceFromHome
* Age
* HourlyRate
* MonthlyIncome (response variable)
* MonthlyRate
* NumCompaniesWorked
* PercentSalaryHike
* TotalWorkingYears
* TrainingTimesLastYear
* YearsAtCompany
* YearsInCurrentRole
* YearsSinceLastPromotion
* YearsWithCurrManager

#### Stationary Variables (Single Valued)

* EmployeeCount
* Over18
* StandardHours

### Details

**ID**: Row ID (integer)

**Age**: Employee age (integer)

**Attrition**: If employee left company; response variable (factor)

**BusinessTravel**: Frequeny of travel associated with employee's job (factor)

* Travel_Rarely
* Travel_Frequently
* Non-Travel

**DailyRate**: Unknown numeric value (integer)

**Department**: Department where employee works (factor)

**DistanceFromHome**: Some measurement of distance employee commutes from home (integer)

**Education**: Unknown measurement of education, likely a level (factor)

* 5
* 4
* 3
* 2
* 1

**EducationField**: Field of education (factor)

* Life Sciences
* Medical
* Marketing
* Technical Degree
* Other
* Human Resources

**EmployeeCount**: Number of employees in observation; always 1 (integer)

**EmployeeNumber**: Employee ID number (factor)

**EnvironmentSatisfaction**: Employee's satisfaction with environment (factor)

* 4
* 3
* 2
* 1

**Gender**: Employee gender (factor)

* Male
* Female

**HourlyRate**: Unknown numeric value (integer)

**JobInvolvement**: Measurement of employee job involvement (factor)

* 4
* 3
* 2
* 1

**JobLevel**: Seniority of employee's position (factor)

* 5
* 4
* 3
* 2
* 1

**JobRole**: Role of position (factor)

* Sales Executive	
* Research Director	
* Manufacturing Director	
* Research Scientist	
* Sales Representative	
* Healthcare Representative
* Manager
* Human Resources
* Laboratory Technician

**JobSatisfaction**: Measurement of job satisfaction (factor)

* 4
* 3
* 2
* 1

**MaritalStatus**: Employee marital status (factor)

* Divorced				
* Single				
* Married

**MonthlyIncome**: Employee's monthly income (integer)

**MonthlyRate**: Unknown numeric value (integer)

**NumCompaniesWorked**: Number of companies employee previously worked for (integer)

**Over18**: If employee is over 18; always 'Yes'

**OverTime**: Indicator of whether employee works overtime (factor)

* No				
* Yes

**PercentSalaryHike**: Percent increase in salary (integer)

**PerformanceRating**: Measurement of employee performance (factor)

* 3
* 4

**RelationshipSatisfaction**: Measurement of employee relationship satisfaction (factor)

* 4
* 3
* 2
* 1

**StandardHours**: Standard working hours; always 80

**StockOptionLevel**: Level of stock options granted to employees (factor)

* 3
* 2
* 1
* 0 

**TotalWorkingYears**: Employee's number of working years (integer)

**TrainingTimesLastYear**: Measurement of employee's training times in the previous year (integer)

**WorkLifeBalance**: Measurement of employee's work-life balance (factor)

* 4
* 3
* 2
* 1

**YearsAtCompany**: Years of experience at this company (integer)

**YearsInCurrentRole**: Year of experience in current role (integer)

**YearsSinceLastPromotion**: Number of years since last promotion (integer)

**YearsWithCurrManager**: Number of years working for current manager (integer)




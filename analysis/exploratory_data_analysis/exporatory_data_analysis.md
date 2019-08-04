Exploratory Data Analysis
================
Stuart Miller
August 4, 2019

# Setup Environment

``` r
library(knitr)
library(tidyverse)
library(naniar)
library(Hmisc)
library(GGally)

train <- read_csv('../data/CaseStudy2-data_train.csv')
```

# Data Exploration

A data dictionary was not given. So start by exploring the variables to
get a sense of what is included. A simple data dictionary will be built.
See ‘./analysis/data/README.md’ for more details.

``` r
names(train)
```

    ##  [1] "ID"                       "Age"                     
    ##  [3] "Attrition"                "BusinessTravel"          
    ##  [5] "DailyRate"                "Department"              
    ##  [7] "DistanceFromHome"         "Education"               
    ##  [9] "EducationField"           "EmployeeCount"           
    ## [11] "EmployeeNumber"           "EnvironmentSatisfaction" 
    ## [13] "Gender"                   "HourlyRate"              
    ## [15] "JobInvolvement"           "JobLevel"                
    ## [17] "JobRole"                  "JobSatisfaction"         
    ## [19] "MaritalStatus"            "MonthlyIncome"           
    ## [21] "MonthlyRate"              "NumCompaniesWorked"      
    ## [23] "Over18"                   "OverTime"                
    ## [25] "PercentSalaryHike"        "PerformanceRating"       
    ## [27] "RelationshipSatisfaction" "StandardHours"           
    ## [29] "StockOptionLevel"         "TotalWorkingYears"       
    ## [31] "TrainingTimesLastYear"    "WorkLifeBalance"         
    ## [33] "YearsAtCompany"           "YearsInCurrentRole"      
    ## [35] "YearsSinceLastPromotion"  "YearsWithCurrManager"

# Continuous Variables

Exploration of the continuous variables.

``` r
# create a vector of numeric features
features.numeric <- c('DailyRate', 'DistanceFromHome', 'Age', 'HourlyRate', 'MonthlyIncome', 'MonthlyRate',
           'NumCompaniesWorked','PercentSalaryHike', 'TotalWorkingYears', 'TrainingTimesLastYear',
           'YearsAtCompany','YearsInCurrentRole','YearsSinceLastPromotion', 'YearsWithCurrManager')
```

## Univariate Analysis

Explore features in isolation and the relationship between features and
the response variables.

**Variance of Features**

The following table ranks features in order of descending standard
deviation.

``` r
# get varaince table
temp.table <- train %>%
  select(features.numeric) %>%
  summarise_all(funs(sd(., na.rm=TRUE))) %>%
  rownames_to_column %>%
  gather(var, value, -rowname) %>%
  arrange(-value) %>%
  select(-one_of(c('rowname')))
# rename columns for clairity and print markdown table
names(temp.table) <- c('Feature','Standard Deviation')
kable(temp.table)
```

| Feature                 | Standard Deviation |
| :---------------------- | -----------------: |
| MonthlyRate             |        7108.381928 |
| MonthlyIncome           |        4597.695974 |
| DailyRate               |         401.116280 |
| HourlyRate              |          20.127163 |
| Age                     |           8.925950 |
| DistanceFromHome        |           8.136704 |
| TotalWorkingYears       |           7.513668 |
| YearsAtCompany          |           6.021036 |
| PercentSalaryHike       |           3.675440 |
| YearsInCurrentRole      |           3.639317 |
| YearsWithCurrManager    |           3.574441 |
| YearsSinceLastPromotion |           3.185872 |
| NumCompaniesWorked      |           2.520443 |
| TrainingTimesLastYear   |           1.272665 |

**`Age` exploration**

There appears to be a relationship between `Age` and `MonthlyIncome`. A
relationship between `Age` and `Attrition` is not clear.

``` r
train %>% ggplot(aes(x = Age)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = Age)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-4-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = Age, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-4-3.png)<!-- -->

**`DailyRate` exploration**

There does not appear to be a correlation between `DailyRate` and either
outcome variable.

``` r
train %>% ggplot(aes(x = DailyRate)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = DailyRate)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = DailyRate, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-5-3.png)<!-- -->

**`DistanceFromHome` exploration**

There does not appear to be a correlation between `DistanceFromHome` and
either outcome variable.

``` r
train %>% ggplot(aes(x = DistanceFromHome)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = DistanceFromHome)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = DistanceFromHome, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-6-3.png)<!-- -->

**`MonthlyRate` exploration**

There does not appear to be a correlation between `MonthlyRate` and
either outcome variable.

``` r
train %>% ggplot(aes(x = MonthlyRate)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = MonthlyRate)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = MonthlyRate, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-7-3.png)<!-- -->

**`PercentSalaryHike` exploration**

There does not appear to be a correlation between `PercentSalaryHike`
and either outcome variable.

``` r
train %>% ggplot(aes(x = PercentSalaryHike)) + 
  geom_histogram()
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = PercentSalaryHike)) + 
  geom_histogram() + 
  facet_wrap(~ Attrition)
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-8-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = PercentSalaryHike, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-8-3.png)<!-- -->

**`TotalWorkingYears` exploration**

There does appear to be a correlation between `TotalWorkingYears` and
`MonthlyIncome`.

``` r
train %>% ggplot(aes(x = TotalWorkingYears)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = TotalWorkingYears)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-9-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = TotalWorkingYears, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-9-3.png)<!-- -->

**`TrainingTimesLastYear` exploration**

There does not appear to be a correlation between
`TrainingTimesLastYear` and either outcome variable.

``` r
train %>% ggplot(aes(x = TrainingTimesLastYear)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = TrainingTimesLastYear)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-10-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = TrainingTimesLastYear, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-10-3.png)<!-- -->

**`YearsAtCompany` exploration**

There does appear to be a correlation between `YearsAtCompany` and
`MonthlyIncome`.

``` r
train %>% ggplot(aes(x = YearsAtCompany)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = YearsAtCompany)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-11-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = YearsAtCompany, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-11-3.png)<!-- -->

**`YearsInCurrentRole` exploration**

There does appear to be a correlation between `YearsInCurrentRole` and
`MonthlyIncome`.

``` r
train %>% ggplot(aes(x = YearsInCurrentRole)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = YearsInCurrentRole)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-12-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = YearsInCurrentRole, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-12-3.png)<!-- -->

**`YearsSinceLastPromotion` exploration**

There does appear to be a correlation between `YearsSinceLastPromotion`
and `MonthlyIncome`.

``` r
train %>% ggplot(aes(x = YearsSinceLastPromotion)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = YearsSinceLastPromotion)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-13-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = YearsSinceLastPromotion, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-13-3.png)<!-- -->

**`YearsWithCurrManager` exploration**

There does not appear to be a correlation between `YearsWithCurrManager`
and either outcome variable.

``` r
train %>% ggplot(aes(x = YearsWithCurrManager)) + 
  geom_histogram(bins = 15)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

``` r
train %>% ggplot(aes(x = YearsWithCurrManager)) + 
  geom_histogram(bins = 15) + 
  facet_wrap(~ Attrition)
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-14-2.png)<!-- -->

``` r
train %>% ggplot(aes(x = YearsWithCurrManager, y = MonthlyIncome)) + 
  geom_point() + geom_smooth(method = 'lm')
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-14-3.png)<!-- -->

## Multivariate Exploration

Scatter plot and correlation matrix gives a board overview of
correlations between continuous variables.

  - `MonthlyIncome` appears to be correlated with `Age` and
    `TotalWorkingYears`
  - `YearsAtCompany`,`YearsInCurrentRole`,`YearsSinceLastPromotion`,
    `YearsWithCurrManager`, `TotalWorkingYears`, and `Age` appear to be
    correlated.

<!-- end list -->

``` r
train %>%
  select(features.numeric) %>%
  ggpairs()
```

![](exporatory_data_analysis_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

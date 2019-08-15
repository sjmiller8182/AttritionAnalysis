Modeling Attrition
================
Stuart Miller
August 14, 2019

``` r
## Computation Setup

# import libraries
library(knitr)
library(tidyverse)
library(GGally)
library(gridExtra)
library(RColorBrewer)
library(gplots)
library(corrplot)
library(ggthemes)
library(caret)

set.seed(3456)

# import helper functions
source('../helper/data_munging.R')
source('../helper/visual.R')

# read in data
train <- read_csv('../data/CaseStudy2-data_train.csv')

# create a vector of numeric features
features.numeric <- c('DailyRate', 'DistanceFromHome', 'Age', 'HourlyRate', 'MonthlyIncome', 'MonthlyRate',
           'NumCompaniesWorked','PercentSalaryHike', 'TotalWorkingYears', 'TrainingTimesLastYear',
           'YearsAtCompany','YearsInCurrentRole','YearsSinceLastPromotion', 'YearsWithCurrManager')

# create a vector of numeric features
features.factor <- c('BusinessTravel', 'Department', 'Education', 'EducationField', 'EnvironmentSatisfaction', 'Gender', 'JobInvolvement', 'JobLevel', 'JobRole', 'JobSatisfaction', 'MaritalStatus', 'OverTime', 'PerformanceRating', 'RelationshipSatisfaction', 'StockOptionLevel', 'WorkLifeBalance')
```

## Variable Munging

Based on EDA several categorical levels will be releveled. Levels of
variables that appear to have similar rates of attrition will be
combined.

**Groupings**

  - JobInvolvement
      - Level 3 is similar to level 2
      - Level 4 is similar to level 2
  - EnvironmentSatisfaction
      - Level 3 is similar to level 2
      - Level 4 is similar to level 2
  - WorkLifeBalance
      - Level 3 is similar to level 2
      - Level 4 is similar to level 2
  - StockOptionLevel
      - Level 0 is similar to level 3
      - Level 1 is similar to level 2
  - Education
      - Level 2 is similar to level 1
      - Level 3 is similar to level 1
      - Level 4 is similar to level 1
  - JobLevel
      - Level 2 is similar to level 5
      - Level 3 is similar to level 5
  - JobRole
      - Sales Executive, Human Resources, Laboratory Technician, and
        Research Scientist are similar
      - Manufacturing Director, Research Director, Manager, and
        Healthcare Representative are similar
  - BusinessTravel
      - Non-Travel and Travel\_Rarely are similar
  - EducationField
      - Technical Degree and Human Resources are similar
      - Life Sciences and Medical are similar
      - Marketing and Other are similar
  - JobSatisfaction
      - Level 3 is similar to level 1
      - Level 4 is similar to level 1

<!-- end list -->

``` r
# drop variables that are not useful - static or unique
train <- select(train, -c('EmployeeCount', 'EmployeeNumber','StandardHours', 'Over18'))

# factor categorical variables
train[, features.factor] <- lapply(train[, features.factor], as.factor)

train$Attrition <- as.factor(train$Attrition)

train$JobInvolvement <- recode(train$JobInvolvement, '3' = '2', '4' = '2')
train$EnvironmentSatisfaction <- recode(train$EnvironmentSatisfaction, '3' = '2', '4' = '2')
train$WorkLifeBalance <- recode(train$WorkLifeBalance, '3' = '2', '4' = '2')
train$StockOptionLevel <- recode(train$StockOptionLevel, '0' = '3', '1' = '2')
train$Education <- recode(train$Education, '2' = '1', '3' = '1', '4' = '1')
train$JobLevel <- recode(train$JobLevel,  '2' = '5', '3' = '5')
train$JobRole <- as.factor(recode(train$JobRole, "Sales Representative" = 3,
                                        "Research Scientist" = 2,
                                        "Sales Executive" = 2,
                                        "Human Resources" = 2,
                                        "Laboratory Technician" = 2,
                                        "Manufacturing Director" = 1,
                                        "Research Director" = 1,
                                        "Manager" = 1,
                                        "Healthcare Representative" = 1))
train$BusinessTravel <- recode(train$BusinessTravel, "Non-Travel" = "Travel_Rarely" )
train$EducationField <- recode(train$EducationField,
                              "Technical Degree" = '1',
                              "Human Resources"  = '1',
                              "Life Sciences"    = '2',
                              "Marketing"        = '3',
                              "Medical"          = '2',
                              "Other"            = '3')
train$JobSatisfaction <- recode(train$JobSatisfaction,
                                '3' = '1',
                                '2' = '1')
```

## Data Partitioning

The training dataset will be split into a training set and a test set.
The training set `dfTrain` will be used for model cross validation. The
test set, `dfTest` will be used for final model selection.

``` r
# split off a test set
trainIndex <- createDataPartition(train$Attrition , p = .75, 
                                  list = FALSE, 
                                  times = 1)
dfTrain <- train[trainIndex,]
dfTest <-  train[-trainIndex,]
```

## Model Training

With a small data set for training, the model will be initially trained
with repeated 5-fold CV. Because there are a large number of categorical
that appear to be useful for predicting attrition (based on EDA), a
naive bayes model will be used.

``` r
# Set up repeated k-fold cross-validation
train.control <-trainControl(method = "repeatedcv",
                             number = 5,
                             repeats = 5,
                             summaryFunction = twoClassSummary,
                             classProbs = TRUE)
# Train the model
model.cv <-train(y = dfTrain$Attrition,
                 x = dfTrain[, c('OverTime' ,
                                 'JobInvolvement' ,
                                 'EnvironmentSatisfaction',
                                 'WorkLifeBalance' ,
                                 'StockOptionLevel' ,
                                 'Age',
                                 'YearsInCurrentRole', 
                                 'YearsAtCompany',
                                 'JobLevel',
                                 'JobRole',
                                 'TotalWorkingYears',
                                 'MonthlyIncome',
                                 'DistanceFromHome',
                                 'YearsWithCurrManager',
                                 'BusinessTravel',
                                 'EducationField')],
                 method = 'nb',
                 metric = 'Spec',
                 trControl = train.control)
# print model summary
model.cv
```

    ## Naive Bayes 
    ## 
    ## 653 samples
    ##  16 predictor
    ##   2 classes: 'No', 'Yes' 
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (5 fold, repeated 5 times) 
    ## Summary of sample sizes: 522, 522, 522, 523, 523, 522, ... 
    ## Resampling results across tuning parameters:
    ## 
    ##   usekernel  ROC        Sens       Spec     
    ##   FALSE      0.7868869  0.8606038  0.5657143
    ##    TRUE      0.7802677  0.9032761  0.4952381
    ## 
    ## Tuning parameter 'fL' was held constant at a value of 0
    ## Tuning
    ##  parameter 'adjust' was held constant at a value of 1
    ## Spec was used to select the optimal model using the largest value.
    ## The final values used for the model were fL = 0, usekernel = FALSE
    ##  and adjust = 1.

## Model Validation

A previously unseen dataset will be used to verify that model is not
overfit to the training data.

The current model provides a specificity of 0.66 on the validation data.

``` r
preds <- predict(model.cv, dfTest[, !names(dfTest) %in% ('Attrition')])

confusionMatrix(table(preds, dfTest$Attrition))
```

    ## Confusion Matrix and Statistics
    ## 
    ##      
    ## preds  No Yes
    ##   No  157  12
    ##   Yes  25  23
    ##                                          
    ##                Accuracy : 0.8295         
    ##                  95% CI : (0.7727, 0.877)
    ##     No Information Rate : 0.8387         
    ##     P-Value [Acc > NIR] : 0.68356        
    ##                                          
    ##                   Kappa : 0.452          
    ##  Mcnemar's Test P-Value : 0.04852        
    ##                                          
    ##             Sensitivity : 0.8626         
    ##             Specificity : 0.6571         
    ##          Pos Pred Value : 0.9290         
    ##          Neg Pred Value : 0.4792         
    ##              Prevalence : 0.8387         
    ##          Detection Rate : 0.7235         
    ##    Detection Prevalence : 0.7788         
    ##       Balanced Accuracy : 0.7599         
    ##                                          
    ##        'Positive' Class : No             
    ##

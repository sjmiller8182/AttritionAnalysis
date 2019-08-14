# Attrition Analysis

Created by [Stuart Miller](https://github.com/sjmiller8182).

## Purpose

In an effort to reduce employee attrition, data has been provided on employees. The objective is to analyze the data to determine what factors (if any) correlate to attrition. The following will be reported:

 * Top 3 factors assocatied with employee turnover
 * A model for predicting employee attrition
 * A model for predicting monthly salary
 * Job role specific trend
 * Any other interesting trends in the data

## Analysis 

### Analysis Files

## Data

Three files were provided. The first is a complete set that will be used for modeling. The other two will be used by a independent party to verify model quality.

 * [`CaseStudy2-data_train.csv`](https://github.com/sjmiller8182/AttritionAnalysis/blob/master/analysis/data/CaseStudy2-data_train.csv): A complete set of data. The analysis is performed on this dataset.
 * [`CaseStudy2CompSetNoAttrition_test.csv`](https://github.com/sjmiller8182/AttritionAnalysis/blob/master/analysis/data/CaseStudy2CompSetNoAttrition_test.csv): A set of data with the response (attrition) removed. This set will be used by an external pary to access the provided model for predicting attrition.
 * [`CaseStudy2CompSetNoSalary_test.csv`](https://github.com/sjmiller8182/AttritionAnalysis/blob/master/analysis/data/CaseStudy2CompSetNoSalary_test.csv): A set of data with the response (salary) removed. This set will be used by an external pary to access the provided model for predicting attrition.

## Codebook

The [Codebook](https://github.com/sjmiller8182/AttritionAnalysis/blob/master/CodeBook.md) provides additional details on the regarding the computational environment, code, and data.

## Repo Structure
    .
    ├── analysis                            # Primary analysis files
    |    ├── exploratory_data_analysis      # Rmarkdown files for EDA
    |    ├── modeling                       # Rmarkdown files for the modeling
    │    ├── data                           # Raw data and merge automation files
    │    └── helper			                # Files containing helper functions
    ├── reports                             # Reports from the analysis
    ├── CodeBook.md                         # Information regarding the computational environment, code, and data
    ├── LICENSE                             # All code and analysis is licensed under the MIT license
    └── README.md

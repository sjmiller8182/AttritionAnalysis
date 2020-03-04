
Created by [Stuart Miller](https://github.com/sjmiller8182).

**Contents**
* [Purpose](#Purpose)
* [Reports](#Reports)
* [Analysis](#Analysis)
  * [Exploratory Data Analysis](#EDA)
  * [Modeling](#Modeling)
* [Data](#Data)
* [Codebook](#Codebook)

## Purpose <a name="Purpose"></a>

In an effort to reduce employee attrition, data has been provided on employees. The objective is to analyze the data to determine what factors (if any) correlate to attrition. The following will be reported:

 * Top 3 factors assocatied with employee turnover
 * A model for predicting employee attrition
 * A model for predicting monthly salary
 * Job role specific trend
 * Any other interesting trends in the data

## Reports <a name="Reports"></a>

Reports generated from the analysis

* [HTML Report](./reports/CaseStudy2DDS.html)
* [Powerpoint Presentation](./reports/AttritionAnalysis.pdf)  
* [Presentation Video](https://www.youtube.com/watch?v=QXD0BcmQ6LU) (directs to youtube)

## Analysis  <a name="Analysis"></a>

The files in this folder contain the original analysis files for EDA and modeling.

### Exploratory Data Analysis <a name="EDA"></a>

* [`exploratory_data_analysis.Rmd`](./analysis/exploratory_data_analysis/exporatory_data_analysis.Rmd): contains the primary EDA work.
* [`exploratory_data_analysis.md`](./analysis/exploratory_data_analysis/exporatory_data_analysis.md): markdown file containing the EDA work generated from the `Rmd` file.
* [`deep_dive_on_attrition.Rmd`](./analysis/exploratory_data_analysis/deep_dive_on_attrition.Rmd): contains the deeper EDA work on attrition.
* [`deep_dive_on_attrition.md`](./analysis/exploratory_data_analysis/deep_dive_on_attrition.md): markdown file containing the EDA work generated from the `Rmd` file.

### Modeling <a name="Modeling"></a>

* [`modeling_attrition.Rmd`](./analysis/modeling/modeling_attrition.Rmd): file containing modeling of attrition.
* [`modeling_attrition.md`](./analysis/modeling/modeling_attrition.md): a markdown file generated from `modeling_attrition.Rmd`.
* [`Cas2PredictionsMiller Attrition.csv`](./Cas2PredictionsMiller%20Attrition.csv): predictions from the attrition model index by ID for 3rd party model assessment.
* [`modeling_income.Rmd`](./analysis/modeling/modeling_income.Rmd): file containing modeling of income.
* [`modeling_income.md`](./analysis/modeling/modeling_income.md): a markdown file generated from `modeling_income.Rmd`.
* [`Cas2PredictionsMiller Salary.csv`](./Cas2PredictionsMiller%20Salary.csv): predictions from the income model index by ID for 3rd party model assessment.

## Data <a name="Data"></a>

More information is included in the [data README](./analysis/data/README.md).

### Analysis Data

Three files were provided. The first is a complete set that will be used for modeling. The other two will be used by a independent party to verify model quality.

 * [`CaseStudy2-data_train.csv`](./analysis/data/CaseStudy2-data_train.csv): A complete set of data. The analysis is performed on this dataset.
 * [`CaseStudy2CompSetNoAttrition_test.csv`](./analysis/data/CaseStudy2CompSetNoAttrition_test.csv): A set of data with the response (attrition) removed. This set will be used by an external pary to access the provided model for predicting attrition.
 * [`CaseStudy2CompSetNoSalary_test.csv`](./analysis/data/CaseStudy2CompSetNoSalary_test.csv): A set of data with the response (salary) removed. This set will be used by an external pary to access the provided model for predicting attrition.

### Predictions

The following files contain predictions created with the models created based on the training data. These predictions are provided for assessment by a 3rd party.

* [`Cas2PredictionsMiller Attrition.csv`](./Cas2PredictionsMiller%20Attrition.csv): predictions for employee attrition.
* [`Cas2PredictionsMiller Salary.csv`](./Cas2PredictionsMiller%20Salary.csv): preditions for employee salary.

## Codebook <a name="Codebook"></a>

The [Codebook](./CodeBook.md) provides additional details on the regarding the computational environment, code, and data.

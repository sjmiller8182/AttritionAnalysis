# CodeBook

This code book describes the data and the computational environment.

## Data

TODO: Add description

Data is included in git repo because it is light-weight and in git-friendly format.

## R Variables (Main)

### Variables in `/analysis/exploratory_data_analysis/`

* 

### Variables in `/analysis/modeling/`

#### Data

* `train`: The whole training set; raw import from csv. 870 observations of 32 variables.
* `dfTrain`: A 75% parition of `train` used for model training and cross validation.
* `dfTest`: A 25% parition of `train` used for model selection and final validation.
* `preds`: The predictions based on the models

#### Functional

* `model.cv`: Trained model produced by `caret`.
* `lin.model.cv`: A linear regression model `lm` produced by `caret`.
* `knn.model.cv`: A k-nearest neighbors regression model produced by `caret`.
* `train.control`: List of model training options.
* `model.formula`: A regression model expression.

## Code

All analysis code files are located at `./analysis/`

### Variables in `/analysis/exploratory_data_analysis/`



### Variables in `/analysis/modeling/`



## Libraries

The following R packages are required for running the code or paper generation.

* `bookdown`
* `tidyverse`
  * `ggplot2`
  * `dplyr`
* `knitr`
* `GGally`
* `gridExtra`
* `RColorBrewer`
* `gplots`
* `corrplot`
* `ggthemes`
* `caret`
* `Hmisc`

## R Session Info

Provides an example of the environment used to generate the analysis.

```R
R version 3.5.1 (2018-07-02)
Platform: x86_64-pc-linux-gnu (64-bit)
Running under: Ubuntu 18.04.3 LTS

Matrix products: default
BLAS: /home/stuart/anaconda3/lib/R/lib/libRblas.so
LAPACK: /home/stuart/anaconda3/lib/R/lib/libRlapack.so

locale:
 [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
 [3] LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8    
 [5] LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
 [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                 
 [9] LC_ADDRESS=C               LC_TELEPHONE=C            
[11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
[1] RevoUtils_11.0.1     RevoUtilsMath_11.0.0

loaded via a namespace (and not attached):
[1] compiler_3.5.1
```

## Other Dependencies

Paper was generated with TeX (requires MiKTeX on Windows, MacTeX 2013+ on OS X, or Tex Live 2013+ on Linux)

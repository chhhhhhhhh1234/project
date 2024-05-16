
# Project: Self-Reported Health Analysis

## Purpose

The project aims to conduct survival analysis on public health data about whether the self-reported health status is a significant indicator for motality.

## Data

+ Survey Data from 1999-2000 National Health and Nutrition Examination Survey (NHANES)
  ```stata
  import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
  ```

+ Mortality Follow-up Data from National Center for Health Statistics (NCHS)
  Click [link](https://ftp.cdc.gov/pub/) as follows:
  - Health Statistics
    - NCHS
      - Datalinkage
        - Linked Mortality
          - ```NHANES_1999_2000_MORT_2019_PUBLIC.dat```    
                        
   ```stata
   global mort_1999_2000 https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/NHANES_1999_2000_MORT_2019_PUBLIC.dat  
   ```

## Code Development
+ Access to the .do file from NHANES website
  ```stata
  cat  https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/Stata_ReadInProgramAllSurveys.do
  ```

+ Edit the `SURVEY` to `NHANES_1999_2000`

+ Edit the directory path and rename it to `followup.do`

+ Create `followup.dta` dataset using `followup.do` file 

  ```stata
  //use your own username/project repo instead of the class repo below
  global repo "https://github.com/jhustata/intermediate/raw/main/"
  do ${repo}followup.do
  save followup, replace
  ```

+ Merge datasets
  ```stata
  import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
  merge 1:1 seqn using followup
  lookfor follow
  ```

## Get ready for Next Weeks!

+ Exploratory analaysis on the data (variables of interest) following the [information page](https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/HUQ.htm)
+ Inference and Analysis
  ```stata
  merge 1:1 seqn using demo_mortality, nogen
  sts graph, by(huq010) fail
  stcox i.huq010
  ```
  ```stata
  import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/HUQ.XPT", clear 
  huq010 
  desc huq010
  codebook huq010
  ```
## Week 7
click [here][dyndoc.html] to view nonparametric and semiparametric risk estimates from Stata

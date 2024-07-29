# Child-Care Needs According to CCDF Assistance

Child care is a critical factor in the multi-pronged implementation of poverty reduction within the United States (https://www.povertycenter.columbia.edu/child-care-and-paid-family-leave).

To understand the child-care needs in the context of workforce development of the Greater Austin area, I performed an exploratory analysis through publically available demographic data of children receiving Child Care and Development Fund (CCDF) assistance. 

My findings include the following notable patterns:

* The CPI-adjusted average monthly income of families across ZIP Codes receiving CCDF has moderately decreased from Q1 2021 to Q1 2024.

* The number of homeless individuals in families receiving CCDF has increased from Q1 2021 to Q1 2024. 

* The number of children receiving CCDF assistance is **trending upwards** from Q1 2021 to Q1 2024.  
  * The demographics experiencing the most significant increases (across ethnicity, gender, and age) are `ChildEthnicityHispLatino`, `ChildFemale`, and `ChildAgeSchAge`.

* However, a notable decrease occurred from Q3 2023 to Q1 2024.  
  * The demographics experiencing the most significant decreases (across ethnicity, gender, and age) are `ChildRaceBlackAfriAmer`, `ChildMale`, and `ChildInfantToddler`.

* Initial time series models signal a **decrease** in children receiving assistance in 2024.

* Pre-kindergarten-aged children account for most families receiving assistance from 2021 to 2024.

* Most ZIP codes in Austin have experienced an **increase** in children receiving assistance, with 78748, 78724, and 78728 experiencing the largest increases.

## Methodology

1. Collected open source data from https://data.texas.gov/ (Monthly Child Care Services Data Report - Children Served by ZIP Code Q1 2021 to Q1 2024)
2. Filtered data town to Greater Austin Area (by ZIP Code)
3. Checked for data quality (missing values according to time, ZIP code, and column, as well as general outliers)
4. Performed exploratory analysis 

## Data Quality Findings

1. 2021 Q3 & 2022 Q4 are duplicates of 2021 Q2 & 2022 Q2 respectively (i.e. these quarters are missing).
2. To protect privacy, `*` symbol is placed to left-censor data where ZIP codes contain < 5 children.
3. ZIP codes have not all been consistently recorded throughout all years (only 33 out of 60 ZIP codes have been recorded each year)
4. Demographic columns (`ChildRaceAsian`, `ChildDisability`, `ChildRaceAmIndAlaNat`) contain >80% censored data.

## Risks

1. Duplicate data inflates values for Q3 2021 & Q4 2022. 
2. Each month entails at least 50% censored data, 
3. Inconsistent data recording introduces the possibility of invalid findings.
4. A low sample size in columns is insufficient to generalize findings for those particular columns.

## Solutions

1. Removed duplicated data. Furthermore, I reached out to the dataset owner (https://data.texas.gov/) on this concern and linearly imputed missing data.
2. Replaced censored data with a constant of `2.5`. 
3. Removed all but 33 consistent ZIP codes from data.
4. Remove demographic columns (`ChildRaceAsian,` `ChildDisability,` `ChildRaceAmIndAlaNat`) containing > 80% of imputed data.

## Exploratory Trends

As demographics overlap (multiple demographic labels can apply to the same child), I strictly use the age demographics (`ChildInfantToddler`, `ChildAgePrek`, `ChildAgeSchAge`) when calculating the average count of children.

### Negative Trend in Consumer Price Index-Adjusted Income

![trend](images/income.png)  

From January 2021 to March 2024, the average income in the Austin area of families receiving CCDF has increased from 2315.18 to 2663.58 (15.05%)

![trend](images/cpi.png) 

However, when considering the consumer price index, we see that the purchasing power of families has decreased from 2780.67 to 2679.29 (-3.65%) when considering the June 2024 CPI. 

### Increase in Average Count of Homeless Individuals 

![trend](images/homeless.png)

The average number of homeless individuals in families has increased from 2021 to 2024. In January 2021, there was an average of 2.94 homeless individuals, and by March 2024 this number increased to 5.35 (81.96%).

### Positive Overall Trend in Average Count of Children

![trend](images/trend.png)  

The number of children receiving CCDF assistance is trending upwards, with the beginning of Q1 2021 showing an average of 19.97 children per ZIP code and the end of Q1 2024 concluding with an average of 25.29 children per ZIP code (26.62% change).

All demographics experienced an increase in average quantity from January 2021 to March 2024, with children in the `ChildEthnicityHispanicLatino` demographic experiencing the **largest** rise between January 2021 and March 2024. In January 2021, there were an average of 28.80 children across all ZIP codes in the `ChildEthnicityHispanicLatino` demographic. By March 2024, this amount had increased to 38.20 (32.61%). 

### Negative Overall Trend from Q3 2023 to Q1 2024

![trend](images/childtrend.png)  

There has also been a notable decline in children receiving CCDF assistance from August 2023 to March 2024, which does not follow a seasonal trend. In August 2023, an average of 29.39 children per ZIP code were receiving assistance, which decreased to 25.29 by March 2024 (-13.95%).

Limiting our scope to the age demographic, `ChildInfantToddler` experienced the most notable decrease in the age category. In August 2023, an average of 27.6 children were in the `ChildInfantToddler` category. By March 2024, this number decreased to 22.2 (-19.7%). 

A demographic shift could explain this value drop during this period. However, an increase in the `ChildAgePreK` demographic should likewise be expected. This is not the case, as both the `ChildAgePreK` and `ChildAgeSchAge` demographics decreased by 12.17% and 10.09% respectively. 

### Modeling Future Outcomes

![trend](images/predicted.png)  

To model the future trend in this dataset, I chose an ARIMA model to account for the dataset's non-stationarity. Using this model, we can observe that the trend for average children receiving CCDF assistance is predicted to decrease to an average of 22.47 by December 2024. 

### Pre-Kindergarten Aged Children Account for Largest Share of Age Demographics

![trend](images/child.png)  

Year over year, the average number of children across all ZIP codes in the `ChildAgePreK` demographic is larger than the other 2 age demographics (`ChildInfantToddler`, `ChildAgeSchAge`)

### Notable ZIP Codes with Positive Trend

![trend](images/zips.png)  

When only considering the number of children across age demographics, 72% of Austin ZIP codes have experienced an increase in children receiving CCDF assistance from January 2021 to March 2024, and 16% of ZIP codes have experienced no change. Finally, 12% of ZIP codes have experienced a decrease. The most notable changes in ZIP codes include:

* 78748 (Manchaca): 32.33 in 2021 to 53 in 2024  
* 78724 (Daffin): 47.33 in 2021 to 66.33 in 2024  
* 78728 (Wells Branch): 50.33 in 2021 to 65 in 2024  

## Prescriptions 

* Enhance Spanish language assistance within child-care centers in support of families with children in the increasing `ChildEthnicityHispanicLatino` demographic.
* Target outreach to families with children that are within the `ChildRaceBlackAfriAmer` and `ChildInfantToddler` demographics to identify the cause of the decrease.
* Anticipate the consistent need for child care from 2023 into 2024 for children in the `ChildAgeSchAge` category, with a potential reduced need for the `ChildInfantToddler` category.
* Enhance Pre-K child-care programs for 2024, as children in the `ChildAgePreK` demographic consistently make up the largest share of those receiving assistance according to age. 
* Investigate and tailor outreach for child-care needs in crucial ZIP codes of 78748, 78724, and 78728. Analyze which demographic shifts account for the largest changes in these ZIP codes.

## Next Steps

* Investigate the underlying causes of the decrease in children receiving CCDF from 2023 to 2024 through statistical methods, policy, economic, and demographic research.
* Receive data from missing quarters.
* Investigate demographic distributions to better model censored data.
* Investigate individual ZIP Code demographics to understand trends and target outreach better.
* Monitor additional data to compare predicted trends with reality.
* Combine child data with family data to understand the workforce and educational needs of the family.
* Create a data dashboard to communicate findings.
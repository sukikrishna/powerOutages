## Introduction

Understanding the causes of power outages and who they affect can be an important analysis for ensuring the efficiency and reliability of current infrastructure to prevent or be prepared for future occurrences.

The "Major Power Outage Risks in the U.S." dataset comes from the Laboratory for Advancing Sustainable Critical Infrastructure at Purdue University.

This dataset has information about every major power outage in the United States between January 2000 and July 2016. There are 55 variables containing information that might explain how these power outages happened and how they were fixed. This dataset obtained its information from (i) OE-417 form Schedule 1 published by DOE׳s Office of Electricity Delivery and Energy Reliability; (ii) U.S. Energy Information Administration (EIA) [form EIA-826 and EIA-861]; (iii) National Oceanic and Atmospheric Administration (NOAA); (iv) National Climatic Data Center (NCDC); (v) U.S. Department of Labor; Bureau of Labor Statistics; and, (vi) U.S. Census Bureau [1].

This dataset contains 1534 observations and 56 features. The features include the time and date of power outage occurrences, location, duration, causes of the events, electricity consumption, and regional and economic characteristics. In analyzing this comprehensive dataset, one of our goals is to provide insights into power outage patterns to help create informed decisions on preparing for future power outage disasters.

It's important to understand why power outages are happening, so we'd be better prepared for them. There are many questions that we may strive to answer. With the increase of climate change, has there been more severe weather over the years? Are electricity companies keeping up and updating the protection of their facilities from severe weather? Are there more power outages now than in the past (climate change) (grouped 2000-2008 and 2009-2016)? Is there an upward trend? By ratio, are there more power outages now due to severe weather compared to the past? Are industries using more electricity than residents? These questions are important if we want to minimize power outages and their disastrous effects on daily lives and the economy.

We strive to answer the question: What causes power outages and who do they affect?

For our analysis, we will answer aim to analyze the following hypothesis:

*Null hypothesis*: The ratio of power outages due to severe weather from 2000-2008 is the same as the ratio of power outages overall.

*Alternative hypothesis*: The ratio of power outages due to severe weather from 2000-2008 is less than the ratio of power outages overall.

Relevant columns for this test are `YEAR` and `CAUSE.CATEGORY`. `YEAR` states the year of the particular power outage. `CAUSE.CATEGORY` states the cause as one of seven: equipment failure, fuel supply emergency, intentional attack, islanding, public appeal, severe weather, and system operability disruption.

The relevant columns for the people affected by power outages are `TOTAL.PRICE`, `COM.PERCEN`, `POPPCT_UC`, and `IND.PERCEN`. Detailed descriptions of the relevant features we included are listed in the following table [1]. More detailed descriptions of other features included in the raw dataset can be found in this [article](https://www.sciencedirect.com/science/article/pii/S2352340918307182) under "Table 1: Variable descriptions".

|Column	                 |Description|
|---                     |---        |
|`'YEAR'	`              |Indicates the year when the outage event occurred|
|`'MONTH'`	             |Indicates the month when the outage event occurred|
|`'CUSTOMERS.AFFECTED'`	 |Number of customers affected by the power outage event|
|`'CAUSE.CATEGORY'`	     |Categories of all the events causing the major power outages|
|`'CAUSE.CATEGORY.DETAIL'`	 |Detailed description of the event categories causing the major power outages|
|`'TOTAL.PRICE'`	       |Average monthly electricity price in the U.S. state (cents/kilowatt-hour)|
|`'COM.PERCEN'`	         |Percentage of commercial electricity consumption compared to the total electricity consumption in the state (in %)|
|`'IND.PERCEN'`	         |Percentage of industrial electricity consumption compared to the total electricity consumption in the state (in %)|
|`'POPPCT_UC'`	         |Percentage of the total population of the U.S. state represented by the population of the urban clusters (in %)|
|`'OUTAGE.DURATION'`	       |Duration of outage events (in minutes)|
|`'TOTAL.CUSTOMERS'`	       |Annual number of total customers served in the U.S. state|
|`'CLIMATE.REGION'`	       |U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)|
|`'HURRICANE.NAMES'`	       |If the outage is due to a hurricane, then the hurricane name is given by this variable|

## Data Cleaning and Exploratory Data Analysis

Before analyzing our power outage dataset, we would first conduct data cleaning to make the data more convenient for analysis.

We deleted the rows and columns that didn't have data on the Excel file containing the raw data, then we converted the Excel file into a CSV file.

The first 5 rows of the raw DataFrame is shown in the following table:

<iframe 
  src="assets/df.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The data frame was filtered to include only the columns that would be analyzed or included in an analysis. The data types for all of the features we were analyzing were of an appropriate data type. The `MONTH` column was typecasted from floats to ints since this column only contained integer values. For the `CUSTOMERS.AFFECTED` feature, the NaN values were filled in with 0. This is because we could assume that if `CUSTOMERS.AFFECTED` was so insignificant that it wasn't recorded, there probably wasn't anyone affected.

For the purposes of our hypothesis test, we converted the `CAUSE.CATEGORY` column into a binary column of values "severe weather" and "other" for any other cause. The `YEARS` column was converted to a binary `year_range` column to specify if the power outage occurred in the first half or second half of our data time range (2000-2008 and 2009-2016 respectively). We don't have any missing data in either of these categories.

After data cleaning, the first 5 rows of the resulting DataFrame are shown below in the following table:

***INCLUDE CLEANED HEAD DF***


**Distribution of Columns and Aggregates**

<iframe 
  src="assets/Number_of_Power_Outages_over_Time.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot shows the number of power outages each year. We see that there was a spike in 2011 and it has been relatively decreasing ever since.

<iframe 
  src="assets/Causes_of_Power_Outages.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Here is displayed a bar plot representing the number of power outages in the dataset due to each cause. Severe weather is the most common cause followed by intentional attack.

<iframe 
  src="assets/pivot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe 
  src="assets/Ratio_of_Power_Outages_due_to_Severe_Weather_over_Time.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Here we have the yearly trend of the proportion of power outages due to severe weather shown in both pivot table form and bar graph form. It seems like it decreased over time. We will therefore test an alternate hypothesis: The ratio of power outages due to severe weather from 2000-2008 is more than the overall ratio of power outages due to severe weather.

<iframe 
  src="assets/Spread_of_Power_Outages_due_to_Causes.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Here, we see the spread of power outages over the years, separated by causes. From these visualizations, we see that the ratio of power outages due to severe weather actually decreases over time rather than increases. This plot seems to imply that there were relatively more power outages due to other causes in later years and more power outages overall.

## Assessment of Missingness

In the data set, the major outages are described in terms of the duration of the outage event and the total number of customers affected during that event.

NMAR: Missing power outages likely have a smaller `OUTAGE.DURATION` and fewer `TOTAL.CUSTOMERS` since the data was only collected for major power outages.

We believe `CUSTOMERS.AFFECTED` is NMAR because the dataset would be less likely to record the number if there are few customers affected.

MAR: `CLIMATE.REGION` is MAR because it's only missing for states that aren't part of the mainland US -- Alaska and Hawaii.

MD: `HURRICANE.NAMES` is missing by design. It only has a value if `CAUSE.CATEGORY.DETAIL` is hurricanes

The test statistic is the TVD between the distribution of causes when the cause details are missing or not missing

We perform a permutation test to check if the `CAUSE.CATEGORY.DETAIL` missingness depends on `CAUSE.CATEGORY` with Total Variation Distance (TVD) as the test statistic.

*Null hypothesis*: The missingness of `CAUSE.CATEGORY.DETAIL` does not depend on `CAUSE.CATEGORY`.

*Alternative hypothesis*: The missingness of `CAUSE.CATEGORY.DETAIL` does depend on `CAUSE.CATEGORY`.

<iframe 
  src="assets/Empirical_Distribution_of_the_TVD.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

As observed from the graph above, the p-value is close to 0, which is within the significance level of 0.05 (5%). If the p-value were within the threshold that would suggest that the data is missing completely at random (MCAR). We reject the null hypothesis in favor of the alternative hypothesis that `CAUSE.CATEGORY.DETAIL` missingness <u>does</u> depend on `CAUSE.CATEGORY`.


**NEED MISSINGNESS OF COLUMN DEPENDENT AND NOT DEPENDENT ON SELECTED COLUMN**


As observed from the graph above, the p-value is close to 1 far greater than our significance level of 0.05 (5%). If the p-value were within the threshold that would suggest that the data is missing completely at random (MCAR). We fail to reject the null hypothesis that `CAUSE.CATEGORY.DETAIL` missingness <u>does not</u> depend on `CAUSE.CATEGORY`.

## Hypothesis Testing

*Null hypothesis*: The ratio of power outages due to severe weather from 2000-2008 is equal to the ratio of power outages due to severe weather overall.

*Alternative hypothesis*: The ratio of power outages due to severe weather from 2000-2008 is more than the ratio of power outages due to severe weather overall.

The test statistic is the proportion of power outages that have `CAUSE.CATEGORY` of severe weather.

<iframe 
  src="assets/Empirical_Distribution_of_the_Observed_Statistic.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The p-value is 0.0. We reject the null hypothesis that the proportion of power outages due to severe weather is similar between 2000-2008 and an overall number of power outages in favor of the alternative hypothesis that the ratio of power outages due to severe weather from 2000-2008 is more than the ratio of power outages due to severe weather overall.

## Framing a Prediction Problem

Relevant covariates/predictors: `TOTAL.PRICE`, `COM.PERCEN`, `POPPCT_UC`

Target variable: `IND.PERCEN`

Using the correlation matrix below, we wanted to find a column prediction that had some correlation but wasn't too easy to predict. For example, predicting TOTAL.SALES would be too easy as it's just the sum of `RES.SALES`, `COM.SALES`, and `IND.SALES`. We found that, using regression, `IND.PERCEN` would be a good variable with an okay correlation. It would also be good to predict how much of the total electricity consumption in a state comes from industry rather than residents because so many state policies try to limit electricity consumption by residents while ignoring just how much is consumed by industry.

We will use accuracy in predicting because we want our model to predict as closely as possible to the actual `IND.PERCEN`. It doesn't matter if it's over or under.

<iframe 
  src="assets/Correlation.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The remaining features in the dataset are either derived from the predictors that we have chosen or are features that may not be as relevant to the causes of power outages.

## Baseline Model

The baseline model consists of a pipeline that includes a K-Nearest Neighbors (KNN) regression model to predict the 'IND.PERCEN' variable based on features `TOTAL.PRICE`, `COM.PERCEN`, and `POPPCT_UC`. We chose our predictors by checking which features correlated the most with `IND.PERCEN`.

The K-Nearest Neighbors (KNN) regression model is being tested because this algorithm is a common approach for predicting the value of a target variable by finding the k closest data points in the feature space to the input data point and averaging their target values to form the final prediction.

All three features in the model (`TOTAL.PRICE`, `COM.PERCEN`, and `POPPCT_UC`) are quantitative, and there are no ordinal or nominal features.

For the baseline model, no explicit encoding was performed.

The model's performance is evaluated using the R-squared metric, which measures the proportion of the variance in the target variable that is predictable from the input features. Generally, higher R-squared values closer to 1 indicate better predictive performance.

The `KNeighborsRegressor` was initialized with a parameter of 20 neighbors. The accuracy score ended up being around 0.786.

It works okay, but we want a more accurate predictor.

## Final Model

The same features and modeling algorithm were utilized for our improved model, however, we engineered all our relevant columns to have a standard distribution with the StandardScaler transformer to normalize the data. Standardizing the features using StandardScaler means each feature will have a mean of 0 and a standard deviation of 1. This doesn't change anything for most regressors, but it does make a difference for our KNeighborsRegressor because the distance isn't being heavily over-influenced by the larger numbers in the `COM.PERCEN` column.

Afterward, we used `QuantileTransformer` to turn every column into quantiles because we believed that the small differences in each number didn't make too much of a difference in the values of `IND.PERCEN`. Transforming the data into quantiles using QuantileTransformer can help mitigate the influence of outliers.

For hyperparameter tuning, we found the best hyperparameters n_quantiles for the `QuantileTransformer` and n_neighbors for the `KNeighborsRegressor` through `GridSearchCV`. Grid Search performs an exhaustive search across specified hyperparameter ranges to find the best combination of parameters that maximizes model performance.

Testing 'n_quantiles' of `range(20, 1001, 20)` and 'n_neighbors' of `range(1, 31)`, the best 'n_quantiles' was 500, and the best 'n_neighbors' was 2. We believe the best 'n_neighbors' are so low because each city is very different from one another in their industries, geography, and population.

The final model achieved an accuracy of 0.896, which is a 12% improvement over the baseline model's performance. This improvement indicates that applying the feature engineering techniques, along with hyperparameter tuning, effectively enhanced the model's predictive capability.

## Fairness Analysis

We'll test this model for fairness among earlier years (2000-2008) and later years (2009-2016) defined in the `year_range` column.

Null Hypothesis: The model performs the same for earlier years (2000-2008) and later years (2009-2016).

Alternative Hypothesis: The model performs worse in earlier years (2000-2008) than in later years (2009-2016).

<iframe 
  src="assets/Empirical_Distribution_of_the_Observed_Fairness_Statistic.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We used TVD with a significance level of 0.05. The resulting p-value was 0.8, which is greater than 0.05, so there is no significant evidence that the model performs differently in earlier years and later years.

## References
[1] Sayanti Mukherjee, Roshanak Nateghi, Makarand Hastak, Data on major power outage events in the continental U.S., Data in Brief, Volume 19, 2018, Pages 2079-2083, ISSN 2352-3409, https://doi.org/10.1016/j.dib.2018.06.067. (https://www.sciencedirect.com/science/article/pii/S2352340918307182)

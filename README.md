## Introduction

The "Major Power Outage Risks in the U.S." dataset comes from the Laboratory for Advancing Sustainable Critical Infrastructure at Purdue University.

This dataset has information about every major power outage in the United States between January 2000 and July 2016. There are 55 variables containing information that might explain how these power outages happened and how they were fixed. This dataset obtained its information from (i) OE-417 form Schedule 1 published by DOE׳s Office of Electricity Delivery and Energy Reliability; (ii) U.S. Energy Information Administration (EIA) [form EIA-826 and EIA-861]; (iii) National Oceanic and Atmospheric Administration (NOAA); (iv) National Climatic Data Center (NCDC); (v) U.S. Department of Labor; Bureau of Labor Statistics; and, (vi) U.S. Census Bureau [1]. 

This dataset contains 1534 observations and 56 features. The features include the time and date of power outage occurrences, location, duration, causes of the events, electricity consumption, and regional and economic characteristics.

It's important to understand why power outages are happening, so we'd be better prepared for them. There are many questions that we may strive to answer: With the increase of climate change, has there been more severe weather over the years? Are electricity companies keeping up and updating the protection of their facilities from severe weather? Are there more power outages now than in the past (climate change) (grouped 2000-2008 and 2009-2016)? Is there an upward trend? By ratio, are there more power outages now due to severe weather compared to the past?

For our analysis, we will answer aim to analyze the following hypothesis:

*Null hypothesis*: The ratio of power outages due to severe weather from 2000-2008 is the same as the ratio of power outages overall.

*Alternative hypothesis*: The ratio of power outages due to severe weather from 2000-2008 is less than the ratio of power outages overall.

## Data Cleaning and Exploratory Data Analysis

We deleted rows and a column that didn't have data. Then we converted the Excel file into a CSV.

The MONTH column was changed from floats to ints since they are all whole numbers. For both MONTHS and CUSTOMERS.AFFECTED, we filled NaN values with 0. We could assume that if CUSTOMERS.AFFECTED was so insignificant that it wasn't recorded, there probably wasn't anyone affected.

For the purposes of our hypothesis test, we converted the CAUSE.CATEGORY column into a binary column of values "severe weather" and "other" for any other cause. The YEARS column was converted to a binary "year_range" column to specify if the power outage occurred in the first half or second half of our data time range (2000-2008 and 2009-2016 respectively). We don't have any missing data in either of these categories.

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
  src="assets/Ratio_of_Power_Outages_due_to_Severe_Weather_over_Time.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Here we have the yearly trend of the proportion of power outages due to severe weather. It seems like it decreased over time. We will therefore also test an alternate hypothesis: The ratio of power outages due to severe weather from 2000-2008 is more than the overall ratio of power outages due to severe weather.

<iframe 
  src="assets/Spread_of_Power_Outages_due_to_Causes.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Here, we see the spread of power outages over the years, separated by causes. From these visualizations, we see that the ratio of power outages due to severe weather actually decreases over time rather than increases. This plot seems to imply that there were relatively more power outages due to other causes in later years and more power outages overall.

## Assessment of Missingness

The data set describes: The major outages are described in terms of the duration of the outage event and the total number of customers affected during that event.

NMAR: Missing power outages likely have a smaller OUTAGE.DURATION and fewer TOTAL.CUSTOMERS since the data was only collected for major power outages.

We believe CUSTOMERS.AFFECTED is NMAR because the dataset would be less likely to record the number if there are few customers affected.

MAR: CLIMATE.REGION is MAR because it's only missing for states that aren't part of the mainland US: Alaska and Hawaii.

MD: HURRICANE.NAMES is missing by design. It only has a value if CAUSE.CATEGORY.DETAIL is hurricanes

The test statistic is the TVD between the distribution of causes when the cause details are missing or not missing

We perform a permutation test to check if CAUSE.CATEGORY.DETAIL missingness depends on CAUSE.CATEGORY

<iframe 
  src="assets/Empirical_Distribution_of_the_TVD.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe 
  src="assets/Empirical_Distribution_of_the_Observed_Statistic.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

As the pvalue is close to 1 that suggests the data is missing completely at random (MCAR). CAUSE.CATEGORY.DETAIL missingness does not depend on CAUSE.CATEGORY.

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis

## References
[1] Sayanti Mukherjee, Roshanak Nateghi, Makarand Hastak, Data on major power outage events in the continental U.S., Data in Brief, Volume 19, 2018, Pages 2079-2083, ISSN 2352-3409, https://doi.org/10.1016/j.dib.2018.06.067. (https://www.sciencedirect.com/science/article/pii/S2352340918307182)

#  ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 2 - Singapore Housing Data and Kaggle Challenge

## Background

Singapore's lauded public housing-home ownership scheme (BTO scheme) is currently facing many detractors. Recent world events have let to a supply chain issues and a shortage of manpower - all of which are contributing to the shortage of public housing. Even if you were one of the lucky ones to get a coveted BTO, the wait times for construction to be completed can take up to five years.

Given these challenges to buying a home in the primary market (BTOs), many wannabe homeowners are turning to the secondary market - resale flats. But the secondary market has it's own challenges, especially with regards to affordability. Resale prices are rising, and it seems like there is a record-breaking transaction every other month. There is also a trend of more home buyers having to pay cash over valuation (COV), given the increased competition for homes.

### Problem Statement

The primary goal for this project is to build a predictive model that can estimate the resale price of a HDB unit given various attributes. The secondary goal for this project is to find out which attributes most greatly impact the resale price of a HDB unit. 

This will help future home buyers plan their budgets and review/adjust their expectations/requirements accordingly.


## EDA

### Distribution of resale price

From our analysis of resale price, we find that the distribution is positively skewed. The resale prices range from a minimum of S\\$150,000 to a maximum of S\\$1,258,000. However, the mean is only S$448,661. This indicates the presence of outliers, where a low volume of very high prices are affecting the mean.

In this project, we retain the outliers in the dataset, as they represent rare/unusual events that would be useful for our analysis of HDB resale prices.

### Relationship between resale price and various independent variables

The assumptions coming into this project is that location and size are key factors that affect the resale price. We explore the relationship between location factors (townships, proximity to amenities, and accessibility), and size factors (floor area) here.

#### Relationship between resale price and township

The top three towns with the highest average resale prices are:
1. Bukit Timah (S\\$704,416.88)
2. Bishan (S\\$618,458.15)
3. Central Area (S\\$604,929.86)

While the top three towns with the lowest average resale prices are:
1. Yishun (S\\$375,472.45)
2. Bukit Batok (S\\$397,435.62)
3. Woodlands (S\\$402,712.31)

If we can infer a pattern, it seems that flats with closer proximity to Sinapore's central area have higher resale prices.

#### Relationship between resale price and amenities, and accessibility

There does not seem to be a strong relationship between resale price and distance to the closest amenities (malls and hawker centres). However, most resale transactions are clustered towards the shortest distance.

Similarly, there does not seem to be a strong relationship between resale price and distance to the nearest mrt station and bus stop. There is also a clustering of resale transaction towards the shortest distance. But this could also be attributed to the convenience of Singapore's public transport system.

### Correlation between features

The variables with the strongest correlation with resale price (over 50%) are:
1. Floor area, with a correlation coefficient of 0.66
2. Building height, with a correlation coefficient of 0.5

However, this correlation calculation should not be taken at face value as it does not consider categorical variables such as location.


## Model Fitting and Evaluation

We first fit the models on three types of linear regression before choosing the best model for production.

The three regressions used (linear, ridge and lasso) have similar R-squared and RMSE scores. We decided to use the ridge model, as it is able to deal with outliers and will incorporate all features - which helps with our secondary goal. 

### Training and testing

We split our data to train and test sets, then carried out the necessary encoding and scaling before deploying our chosen production model on the train and test sets separately. We also deployed the model on an independent data set.

The results of the running the model are detailed in the table below:
|Data set|R-squared score|RMSE score|
|-|-|-|
|Train set|0.893|80965|
|Test set|0.892|46988|
|Independent test|NA|46988|

Although the R-squared score for the train and test set are similar, the RMSE score difference is very high. This could be because of the outliers in the data set, and uneven splitting.

## Features that have the greatest impact on resale price

Based on the model, features such as location (planning area and town) have the most impact on resale prices. Flat size (floor area) has the next greatest impact on resale price. Specifically, the larger the floor area, the greater the impact on resale price. Flat models have the next greatest impact on resale price, with rarer flat models, such as DBSS, terraces and maisonettes, having the greatest impact on resale price.

However, there are some pecularities in impact of location on resale prices. In this project, Pasir Ris as a planning area has a negative impact on resale price, while Pasir Ris as a township has a positive impact on resale price. This peculiarity is also evident in Bedok, where as a planning area, it has a positive impact on resale price, but as a township, it has a negative impact on resale price.

As a future home buyer, if one were to buy a flat for investment (to flip): location, larger floor space, and having a rare flat model would be ideal. However, if one were to buy a flat for own-stay with a limited budget, there would need to be prioritisation and trade-offs between location and flat size.


## Conclusion and recommendations

There is definitely a need to better train the model. This could be done with feature interaction (eg. interaction between flat type and flat model, interaction between age of hdb and other variables), and domain knowledge to better understand the situation (eg. maybe a property agent or URA estate planner could explain the township vs planning area peculiarity).

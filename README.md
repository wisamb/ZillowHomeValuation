# Zillow Home Valuation

This was a school project in which I took the lead by finding several datasets to choose from, providing vision and direction throughout, and assisting a fellow student who was early in the program. Work performed by teammates where noted. All python and Jupyter Notebook files in this repositories are my own work. 

<b>Programming Languages/Software:</b> Python, Jupyter Notebook <br>

<b>Skills Used:</b> <br>
Ensemble Trees<br> 
Perceptron Learning<br>
Exploratory Analysis<br>
Imputation of Missing Values

## Introduction

Zillow is a marketplace website for real estate. It provides over 100 million home listings in the U.S. One of the site’s features is to estimate the purchase value of a listed home. In 2017, Zillow hosted a Kaggle competition to determine which factors influence the accuracy of Zillow estimates, known as Zestimate. Zillow accuracy can be summed as follows:

<i>Logerror = log(Zestimate) − log(SalePrice)</i><br>

Our project will determine which features influence the accuracy of Zillow estimates. Since logerror is a continuous response variable, we will use regression models for our analysis.

## Dataset and Metric

The data provided includes real estate transactions from 1/1/2016 to 9/15/2017 for three counties in California (Los Angeles, Orange, and Ventura), as well as property attribute data for the same counties. Note that logerror and transaction date, as well as property attributes, are provided. Actual Zestimate and SalePrice data are not provided. There are 58 features and a total of 6 million rows of data.

## Approach 

Highly correlated variables, columns with greater than 50% missing values, and extreme values, defined as greater than 3 standard deviations from the mean are removed from the dataset. Imputation of missing values is performed for the remaining missing values. In addition, we are interested in the accuracy of the algorithm and less interested if the algorithm underestimates or overestimates the SalePrice. Therefore, we use absolute of logerror to run our models.

We then proceed with model analysis by splitting the data into training (67%) and test (33%) datasets. We analyze 9 different models: k-NN, Linear Regression, LogReg Classification, Perceptron Learning, Neural Networks, SVMs and Kernel Method, Random Forest Decision Trees, Gradient Boosted Decision Trees, and XGBoosted Trees. For each model, a programmatic search is used to find the best parameters, and trial-and-error is used to fine tune the parameters. We use model accuracy, measured by Mean Squared-Error (MSE), to determine the best model and conduct feature analysis on that model. Feature analysis determined which features are most influential to Zillow accuracy.

## Exploratory Analysis

First, the dataset for each year is provided as 2 excel files, transaction data and property attributes. In order to work with the data, we combine the 2 excel files for each year by parcel id. Immediately, our dataset is reduced to 167,888 rows. This is due to the fact that there is far fewer transaction data than property data. 

<b>Correlation Matrices performed by teammate</b>
Second, we test our data for correlation. Below is a heatmap showing correlation between all 58 variables.

<img src="/images/image001.png">

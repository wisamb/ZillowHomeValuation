# Zillow Home Valuation

This was a school project in which I took the lead by finding several datasets to choose from, providing vision and direction throughout, and assisting a fellow student who was early in the program. Work performed by teammates are noted. All python and Jupyter Notebook files in this repositories are my own work.

<b>Programming Languages/Software:</b> Jupyter Notebook, Python, scikit-learn <br>

<b>Skills Used:</b> <br>
Ensemble Trees<br> 
Perceptron Learning<br>
Exploratory Analysis<br>
Imputation of Missing Values

Data files can be found <a href="https://www.kaggle.com/c/zillow-prize-1/data" target="_blank">here</a>.

## Introduction

Zillow is a real estate marketplace website. It provides over 100 million home listings in the U.S. One of the site’s features is to estimate the purchase value of a listed home. In 2017, Zillow hosted a Kaggle competition to determine which factors influence the accuracy of Zillow estimates, known as Zestimate. Zillow accuracy can be summed as follows:

<div align=center><i>Logerror = log(Zestimate) − log(SalePrice)</i></div><br>

Our project will determine which features influence the accuracy of Zillow estimates. Since logerror is a continuous response variable, we will use regression models for our analysis.

## Dataset and Metric

The data provided includes real estate transactions from 1/1/2016 to 9/15/2017 for three counties in California (Los Angeles, Orange, and Ventura), as well as property attribute data for the same counties. Note that logerror and transaction date, as well as property attributes, are provided. Actual Zestimate and SalePrice data are not provided. There are 58 features and a total of 6 million rows of data.

## Approach 

Highly correlated variables, columns with greater than 50% missing values, and extreme values (defined as greater than 3 standard deviations) from the mean are removed from the dataset. Imputation of missing values is performed for the remaining missing values. In addition, we are interested in the accuracy of the algorithm and less interested if the algorithm underestimates or overestimates the SalePrice. Therefore, we use absolute of logerror to run our models.

We then proceed with model analysis by splitting the data into training (67%) and test (33%) sets. We analyze 7 different models: kNN, SVM, Linear Regression, Multi-Layer Perceptron, Random Forest, Gradient Boosted trees, and XGBoosted trees. For each model, a programmatic search using a *for-loop* is used to find the best parameters, and trial-and-error is used to fine tune the parameters. We use model accuracy, measured by Mean Squared-Error (MSE), to determine the best model and conduct feature analysis on that model. Feature analysis determined which features are most influential to Zillow accuracy.

## Exploratory Analysis

First, the dataset for each year is provided as 2 excel files, transaction data and property attributes. In order to work with the data, we combine the 2 excel files for each year by parcel id. Immediately, our dataset is reduced to 167,888 rows. This is due to the fact that there is far fewer transaction data than property data. 

### Correlation Analysis 
<i>(performed by teammate)</i>

Second, we test our data for correlation. Below is a heatmap showing correlation between all 58 variables.

<div align=center><img src="/images/image001.png" width="60%"/></div>

Programmatically, we identify and remove variables that have correlation of greater than 0.9 and less than -0.9.

<div align=center>
<table>
  <tr>
    <th>Variable1</th>
    <th>Variable2</th>
    <th>Corr</th>
  </tr>
  <tr>
    <td>calculatedbathnbr</td>
    <td>bathroomcnt</td>
    <td>1.0</td>
  </tr>
  <tr>
    <td>finishedsquarefeet13</td>
    <td>calculatedfinishedsquarefeet</td>
    <td>1.0</td>
  </tr>
  <tr>
    <td>finishedsquarefeet15</td>
    <td>calculatedfinishedsquarefeet</td>
    <td>1.0</td>
  </tr>
  <tr>
    <td>finishedsquarefeet15</td>
    <td>finishedsquarefeet12</td>
    <td>1.0</td>
  </tr>
  <tr>
    <td>finishedsquarefeet50</td>
    <td>finishedfloor1squarefeet</td>
    <td>0.97</td>
  </tr>
  <tr>
    <td>finishedsquarefeet6</td>
    <td>calculatedfinishedsquarefeet</td>
    <td>1.0</td>
  </tr>
  <tr>
    <td>fullbathcnt</td>
    <td>bathroomcnt</td>
    <td>0.99</td>
  </tr>
  <tr>
    <td>fullbathcnt</td>
    <td>calculatedbathnbr</td>
    <td>0.99</td>
  </tr>
  <tr>
    <td>poolsizesum</td>
    <td>finishedsquarefeet15</td>
    <td>0.91</td>
  </tr>
  <tr>
    <td>rawcensustractandblock</td>
    <td>fips</td>
    <td>1.0</td>
  </tr>
  <tr>
    <td>unitcnt</td>
    <td>architecturalstyletypeid</td>
    <td>-1.0</td>
  </tr>
  <tr>
    <td>yardbuildingsqft26</td>
    <td>finishedsquarefeet13</td>
    <td>1.0</td>
  </tr>
  <tr>
    <td>taxamount</td>
    <td>taxvaluedollarcnt</td>
    <td>0.95</td>
  </tr>
</table>
</div>

After removing highly correlated values, there are 47 variables as shown in the heatmap below.

<div align=center><img src="/images/image002.png" width="60%"/></div>

### Imputation of Missing Values

The bar plots below illustrate the percent missing values by feature for each year.

<div align=center><img src="/images/image003.jpg" width="75%"/></div>
<div align=center><img src="/images/image003.jpg" width="75%"/></div>

The red dotted line marks the 50% cut-off mark. If features have greater than 50% missing values, those features are excluded from our analysis. This reduces the dataset to 35 total features. For features that have missing values below the 50% cutoff, we use kNN imputation for both continuous and categorical features <i>(performed by teammate)</i>.

### Extreme Values
<i>(performed by teammate)</i>

Third, we identify extreme outliers in the data using box plots. The below tables provide examples, such as high bathroom and bedroom counts, or homes with very large or small square footage. These values are programmatically removed from our analysis.  

<table>
  <tr>
    <th><img src="/images/image005.jpg"></th>
    <th><img src="/images/image006.jpg"></th>
    <th><img src="/images/image007.jpg"></th>
  </tr>
</table>

Our final dataset contains 148,241 rows and 35 features.

## Model Analysis

The table below summarizes MSE of each model performed. XGBoosted trees had the lowest MSE of all the models. 

<div align=center>
<table>
  <tr>
    <th>Model</th>
    <th>MSE</th>
  </tr>
  <tr>
    <td>SVM<br><i>(performed by teammate)</i></td>
    <td>0.00275331</td>
  </tr>
  <tr>
    <td>kNN<br><i>(performed by teammate)</i></td>
    <td>0.00122146</td>
  </tr>
  <tr>
    <td>Multi-Layer Perceptron</td>
    <td>0.00120851</td>
  </tr>
  <tr>
    <td>Linear Regression</td>
    <td>0.00120085</td>
  </tr>
  <tr>
    <td>Random Forest</td>
    <td>0.00117538</td>
  </tr>
  <tr>
    <td>Gradient Boosted Trees</td>
    <td>0.00117330</td>
  </tr>
  <tr>
    <td>XGBoosted Trees</td>
    <td>0.00116985</td>
  </tr>
</table>
</div>

### Example of *for-loop*

We also use a for-loop that loops through a sequence of numbers to determine key parameters for each model. Below is an example of how looping 1 through 15 for max_depth affected the MSE of random forest. 

<div align=center><img src="/images/image011.jpg" width="50%"/></div>

## Feature Analysis

Using feature analysis of the XGBoosted trees model, we determine the features most influential to Zillow accuracy. The waterfall plot below shows that longitude, latitude, lotsizesquarefeet, landtaxvaluedollarcnt, and calculatedfinishedsquarefeet are the top 5 variables for Zillow accuracy. These 5 variables are related to location, size of property, and property valuation by the county, which are top factors to influence sales price of a property. It makes sense that Zillow’s algorithm places greater weight on these variables rather than others. 

<div align=center><img src="/images/image012.png" width="70%"/></div>

## Detailed Roles

My specific technical contributions consisted of: <br> 
feature analysis of XGBoosted trees <br>
model analysis by Linear Regression, Multi-Layer Pereptron, Random Forest, Gradient Boosted trees, XGBoosted trees <br>
plots of missing values by feature

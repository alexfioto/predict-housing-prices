README.md

# Housing Data Linear Regression Models


### Introduction
Using Ames, Iowa housing data, this project walks through my approach to creating regression models that will predict the sale price of a house. 

I utilize the following python libaries:
- **matplotlib**: data visualization
- **numpy**: scientific computing
- **pandas**: data importing, cleaning, and exploratory analysis
- **sci-kitlearn**: machine learning
- **seaborn**: data visualization

### Overview

- Importing libraries and datasets
- Initial data inspection
- Data cleaning
- Exploratory data analysis using data visualization
- Data imputation
- Feature creation and selection
- Creating pipelines and grid-searches of various regression models
- Selecting a model and fine-tuning
- Conclusions and recommendations

## Problem Statement

What is the best linear model to predict housing prices? This question will be broken down into mulple subsets:

- How accurately can we predict house sale prices? 
- Which features are most important? 
- Which linear models work the best? 
- Within each model, what parameters work the best?

## Executive Summary

We will be analyzing and modeling housing data from Ames, Iowa. Below, I have broken down the process for each notebook. 

### Notebook 2.1 Data Cleaning and EDA

First we import the necessary libraries: 
 - matplotlib: data visualization
 - numpy: scientific computing
 - pandas: data analysis
 - sci-kitlearn: machine learning
 - seaborn: data visualization
 - statsmodels: statistical analysis
 
Next I inspect and clean the data using pandas. We will make sure all datatypes are appropriate for analysis, rename columns for ease of use and then appropriately simple impute any missing data for ease of use. I will eventually use KNNImputer in the last notebook.

Using pandas, we will explore and analyze our data looking for trends and patterns. This notebook only goes surface level. Notebook 2.2 includes a much deeper EDA. 

Using matplotlib and seaborn, we will visualize our data using barplots, histograms, scatterplots, regplots, boxplots, and choropleth maps. Each visualization will be accompanied by a description and interpretation.

### Notebook 2.2 Feature Creation and EDA

I list all features and use common knowledge of housing markets to manually select features for testing and further EDA. I mapped some ordinal features to corresponding numerical values including exterior quality and kitchen quality.

I created the following features:
 - total_bath: full baths (1 full bath = 1) and half baths (1 half bath = .5).  
 - all_sf: gr_liv_area + total_bsmt_sf (all square feet in the house)
 - all_flr_sf: 1st_flr_sf + 2nd_flr_sf (1st and 2nd floor square feet)
 - pool: 1 for pool, 0 for no pool
 - garage_ratio: garage_cars / garage_area
 
I use matplotlib and seaborn visualization libraries to interpret how features interact with sale price and remove any outliers. Graphs include scatterplots, boxplots, stripplots and heatmaps. 

I grouped all of the neighborhoods by median sale price and categorized them into 4 groups: Low value, medium-low value, medium-high value and high-value.

Once all features are created and selected I created a heatmap displaying correlations between each feature and sale price.

From those correlations I ran a statsmodels OLS and viewed the summary of its statistical test. I narrowed the features down based on if they had a significant effect on sale price. 

### Notebook 2.3 Inital Testing (Scratch Work)

Using the features and data from notebook 2.2, this notebook is a rough draft of all four linear regression models:
 - OLS
 - Ridge
 - Lasso
 - Elastic Net
 
I ran training data on each model, scored plotted residuals. I used GridSearchCV and Pipelines to search for the best hyperparameters. After much testing, I decided to use Ridge for my performance model.


### Notebook 2.4 Ridge Performance Model

This notebook combines everything that learned in the previous notebooks into one performance model. Much of the data listed in this notebook is explored in much more detail in previous notebooks. I will note in each cell which notebook to look into for explanations.

I have found that the Ridge Linear Regression is the best model for predicting house sale prices in Ames, Iowa. My model had an R2 score of .9381 and a RMSE of 18892 for the training data. The residual plot shows there are still some potential outliers in my data. A few predictions that my model guessed a high value but infact it was much lower. The best model hyperparameters ended up being an alpha of 175 and SelectKBest chose 148 of the 150 features including the polynomials. 

The bottom of the notebook contains a dataframe of all of the features used in the model and their corresponding coefficients. Lastly, there is a bar graph of the top five positive coefficients and top five negative coefficients. 


 
### Conclusion

I have found that the Ridge Linear Regression is the best model for predicting house sale prices in Ames, Iowa. My model had an R2 score of .9381 and a RMSE of 18892 for the training data. Per the residual plot in notebook 2.4, there are a few predictions that my model guessed a high value but infact it was much lower. The best model hyperparameters ended up being an alpha of 175 and SelectKBest chose 148 of the 150 features including the polynomials. 

These are the features that had the most impact on the performance model:


|Feature Name|Coefficient|
|------|------|
|All Floor Sqft|16128.387753|
|Overall Quality|13452.349135|
|Neighborhood|7228.165438|
|Total Basement Sqft|6728.712643|

When predicting sale price of houses I found these to be the main factors

- Quality
- Size
- Neighborhood

If you are a home owner and are going to sell your house, you should first focus on overall quality. Per the data, I would suggest focusing on upgrading kitchen appliances or remodeling to improve overall kitchen quality, making sure your garage is nice looking and clean to improve overall garage quality, and make sure the exterior of your house is high quality and has good curb appeal. This would probably give you the best bang for your buck. 

Next, if within budget, increase the square footage of your home with an addition. This is expensive and might not be worth it cost-wise, but it will most likely improve sale price. Also, examine the official square footage of your home and assess if that is correct. If you believe it to be wrong, you should hire an appraiser to recalculate. Lastly, finishing unfinished spaces in your home will increase your above grade sqft which might help increase sale price. 

Neighborhood: when purchasing a house be aware that you may be paying a premium based on neighborhood. On the flipside, your resale value is probably going to be higher as well. 

Thank you for your interest!


### Data Dictionaries

http://jse.amstat.org/v19n3/decock/DataDocumentation.txt
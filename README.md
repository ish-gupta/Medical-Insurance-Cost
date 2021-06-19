# Medical-Insurance-Cost
Linear Regression model which is optimized to forecast cost of medical insurance for a particular individual, along with statistical testing.

## Dataset
The dataset is taken from Kaggle. The link for the same can be found [here](https://www.kaggle.com/mirichoi0218/insurance).

The dataset is also uploaded in the repository as 'insurance.csv'. It contains the fields _age_, _sex_, _bmi_, _children_, _smoker_, _region_, and _charges_ (target variable).

## Understanding the Data 
After importing the libraries and storing the data in variables, we proceed to identify the numerical and categorical variables. The results are as follows:

![image](https://user-images.githubusercontent.com/59526423/122636153-58376880-d105-11eb-8ecd-d3c50555953b.png)

The heatmap identifies the numeric and categorical variables, and also shows the absence of any missing values.

## Pre-Processing
The categorical variables (_sex_, _smoker_, and _region_) are encoded, i.e., the individual values are assigned a number, using the LabelEncoder() function of the sci-kit library.   

## Data Visualization
We conduct univariate analysis for each of the variables. 

It is observed that the distribution of numeric variables has a lot of outliers. Thus, we apply the RobustScaler() transformation, which removes the median and scales the data according to the quantile range, to get the distribition closer to normal. 

## Feature Selection
p-value and regularization are both applied to identify the features that have a significant impact on the target variable. It is observed that _age_ and _smoker_ are such features.

In order to determine the features that we should use in training our model, we use the **ANOVA** test for numeric variables and the **Pearson's Correlation Coefficient** test for caategorical variables.

The tests show that all but the _region_ variable are significant/correlated. Thus, we will not use the variable in training our model.

## Statistical Testing 
The data is split into train and test data. 

We use the Variance inflation factor (VIF) test on the training data to check for multicollinearity. Since the VIF values for all features are low, we can conclude that there is no multicollinearity in the dataset.

## Model Training

### Model I
We use **k-fold validation** with 5 folds to train our model, and test it on or test dataset which gives us a mean accuracy of **78.9387%**

### Model II
We use the Ordinary Least Squares (OLS) method, which gives an R-squared value of **0.776**. 

## Assumption Testing
### White Test
The test chefcks for heteroskedasticity (unequal variance across range of values). Since we get a p-value of 0.116 (< 0.5), we can conclude that our model is homoskedastic.

### Breusch-Pagan Test
The test is also tests for heteroskedasticity but it is more speicific as it only checks for its linear form. The test confirms that there is no heteroskedasticity in our model.

### Ramsey Reset Test
The test is a general specification test for the model, i.e., whether linear combinations of the fitted values help explain the response variable. The test confirms that our trained model is sufficiently linear.


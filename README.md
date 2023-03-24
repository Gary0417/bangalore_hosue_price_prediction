# Bangalore House Price Prediction: Project Overview
* Created a tool that estimates house prices in Bangalore, India, to help buyers and sellers make informed decisions.
* Optimized Random Forest Regressors using RandomizedSearchCV to achieve the best possible performance. 
* Built a client-facing API using flask which allows users to input the features of a house (such as location, size, and number of bedrooms) and get an estimated price. 

## Code and Resources Used 
**Python Version:** 3.11  
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, re, flask, json, pickle  
**For Web Framework Requirements:**  ```pip install -r requirements.txt```  
**Flask Productionization:** https://youtu.be/Q5JyawS8f5Q?list=PLeo1K3hjS3ut2o1ay5Dqh-r1kq6ZU8W0M&t=1


## Data Cleaning
Before building a regression model, I needed to clean and preprocess the data to ensure that it was accurate and consistent. Here are the steps I took:

* Used mean imputation to fill in the missing values in the 'balcony' column
* Removed column with high percentage of missing values
* Fixed inconsistent data entry in the 'total_sqft' column by: 
    * Replacing the range with the average of the min and max values
    * Converting other measuring units to square feet
* Transformed 'size' to bedroom count
* Transformed 'availability' to move-in readiness
* Added two columns 'price_per_sqft' and 'total_sqft_per_bedroom to remove outliers
* Reduced the number of categories in the 'location' column by labelling any location with less than 10 data points as 'other'

## EDA
I looked at the distributions of the data and the value counts for the various categorical variables. Below are a few highlights.
#### Correlations
<img src="https://github.com/Gary0417/bangalore_hosue_price_prediction/blob/documentation/images/correlation_visual.png"  width="400" height="400">

| Top 10 locations with the highest price | Top 10 locations with the lowest price |
|-----------------------------------------|----------------------------------------|
| <img src="https://github.com/Gary0417/bangalore_hosue_price_prediction/blob/documentation/images/top_10_locations_with_highest_price.png" alt="Top 10 locations with the highest price" width="300"/> | <img src="https://github.com/Gary0417/bangalore_hosue_price_prediction/blob/documentation/images/top_10_locations_with_lowest_price.png" alt="Top 10 locations with the lowest price" width="360"/> |
| Price by Move-in Readiness | Total Square Feet vs Price |
|<img src="https://github.com/Gary0417/bangalore_hosue_price_prediction/blob/documentation/images/price_by_ready_to_move.png" alt="Price by Move-in Readiness" width="400" height="400"/>| <img src="https://github.com/Gary0417/bangalore_hosue_price_prediction/blob/documentation/images/total_sqft_vs_price.png" alt="Total Square Feet vs Price" width="400"/>



## Model Building 

First, I transformed the categorical variables into dummy variables. I also split the data into train and tests sets with a test size of 20%.   

I tried three different models and evaluated them using Mean Absolute Error. I chose MAE because it is more interpretable and easier to understand and more robust to outliers.

I tried three different models:
*	**Multiple Linear Regression** – Used as a baseline model for comparison
*	**Lasso Regression** – Chosen to handle the sparsity associated with the data from the many categorical variables, as well as to identify the most important variables for the model.
*	**Random Forest** –Selected to handle the sparsity of the data and capture potential non-linear relationships between the variables.

## Model performance
The Random Forest model far outperformed the other approaches on the test and validation sets. 
*	**Random Forest** : MAE = 18.70
*	**LASSO Regression**: MAE = 25.32
*	**Linear Regression**: MAE = 25.37

## Productionization 
In this step, I exported the trained machine learning model into a pickle file and built a Python Flask server by following the YouTube tutorial referenced earlier. The Flask server is hosted on a local web server and provides HTTP endpoints to handle incoming requests.

In addition to the server, I also built a website using HTML, CSS, and JavaScript, which allows users to interact with the model and make predictions on home prices. The website makes HTTP GET and POST requests to the Flask server, allowing users to input the necessary data and receive an estimated home price in response.





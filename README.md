# Bangalore House Price Prediction: Project Overview
* Created a tool that estimates house prices in Bangalore, India, to help buyers and sellers make informed decisions.
* Optimized Random Forest Regressors using RandomizedSearchCV to achieve the best possible performance. 
* Built a client-facing API using flask which allows users to input the features of a house (such as location, size, and number of bedrooms) and get an estimated price. 

## Code and Resources Used 
**Python Version:** 3.11  
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, flask, json, pickle
**Flask Productionization:** https://youtu.be/Q5JyawS8f5Q?list=PLeo1K3hjS3ut2o1ay5Dqh-r1kq6ZU8W0M&t=1


## Data Cleaning
Before building a regression model, I needed to clean and preprocess the data to ensure that it was accurate and consistent. Here are the steps I took:

* Imputing Missing Values: I used mean imputation to fill in the missing values in the 'balcony' column.
* Fixing Inconsistent Data Entry: The 'total_sqft' column had inconsistent data entries, including ranges and different measuring units. I fixed this issue by:
    * Replacing the range with the average of the min and max values.
    * Converting other measuring units to square feet.
* Adding New Columns: To remove outliers and improve the accuracy of our model, we added two new columns:
    * 'price_per_sqft': This column calculates the price per square foot for each house, which helps to identify houses with unusually high or low prices.
    * 'total_sqft_per_bedroom': This column calculates the total square feet per bedroom, which helps to identify houses with unusually small or large bedrooms.
* Adding Columns for Bedroom Count and Move-In Readiness: I added two additional columns to provide more information for our model:
    * 'bedrooms': This column indicates the number of bedrooms in each house.
    * 'ready_to_move': This column indicates whether a house is move-in ready or not.
* Reducing Location Categories: To reduce the number of categories in the 'location' column, I labeled any location with less than 10 data points as 'other'. This helped to simplify our model and reduce the risk of overfitting.

## EDA
I looked at the distributions of the data and the value counts for the various categorical variables. Below are a few highlights from the pivot tables. 

![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/salary_by_job_title.PNG "Salary by Position")
![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/positions_by_state.png "Job Opportunities by State")
![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/correlation_visual.png "Correlations")

## Model Building 

First, I transformed the categorical variables into dummy variables. I also split the data into train and tests sets with a test size of 20%.   

I tried three different models and evaluated them using Mean Absolute Error. I chose MAE because it is relatively easy to interpret and outliers aren’t particularly bad in for this type of model.   

I tried three different models:
*	**Multiple Linear Regression** – Baseline for the model
*	**Lasso Regression** – Because of the sparse data from the many categorical variables, I thought a normalized regression like lasso would be effective.
*	**Random Forest** – Again, with the sparsity associated with the data, I thought that this would be a good fit. 

## Model performance
The Random Forest model far outperformed the other approaches on the test and validation sets. 
*	**Random Forest** : MAE = 18.86
*	**LASSO Regression**: MAE = 25.32
*	**Linear Regression**: MAE = 25.37

## Productionization 
In this step, I built a flask API endpoint that was hosted on a local webserver by following along with the YouTube tutorial in the reference section above. The API endpoint takes in a request with a list of values from a job listing and returns an estimated salary. 





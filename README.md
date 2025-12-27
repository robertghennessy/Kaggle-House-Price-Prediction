This repository provides a solution for Kaggle's competition: https://www.kaggle.com/c/house-prices-advanced-regression-techniques

Steps taken:
1. Plot the histograms of the numerical features to check for outliers and missing values.
2. Run a baseline XGBoost model with enable_categorical=True
3. Impute the missing values <br>
   a. Replace nans with 'none' in categorical features where the object does not exist. For example, PoolQC='none' for PoolQC='none' if PoolArea=0. <br>
   b. Assumed that the lot frontage was related to the sqrt of the lot area. <br>
   c. Assume that GarageYrBuilt = YearBuilt <br>
   d. Created a pipeline to impute the remaining of the missing values. Numerical imputation was done with median and categorical imputation was done with mode. A rare label encoder was used on the categorical features.
4. Used an isolation forest to remove outliers. For example, there is a GarageYrBuilt in the future and some outliers in GrLivArea.
5. Created some new features. For example, the number of bathrooms in the house.
6. Removed features that mutual information score with SalePrice to prevent overfitting. 
7. Used optuna to tune the hyperparameters of the XGBoost model.

The final model achieved a RMSE of 0.12517 on the public leaderboard.

Lessons learned:
* Baseline XGBoost is pretty good at regression analysis. All of the steps taken to improve the score, only improved the score by about 20%
* Optuna lead to the largest improvement of the score (improved by ~18%).
* Removing outliers lead to second largest improvement of the score (improved by ~6%).
* Imputing, creating new feautres and removing unimportant did not have a significant impact on the score.  

Potential next steps:
* Create a better way to impute the lot frontage and other numerical columns
* Create new features. For example, the area of the backyard (area lot - area of house).
* Try different machine learning models
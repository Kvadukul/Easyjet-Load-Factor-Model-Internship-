# Easyjet-Load-Factor-Model-Internship

This is the project I built during my Data Science internship at EasyJet. The goal was to predict the Load Factor (what % of seats get filled on a flight) so the commercial teams can make better pricing and schedule choices. 

Note: All data, outputs, and exact code columns have been redacted because, I can't share EasyJet's data!


## What's in this repo?
The redacted Databricks notebook with all my Python/Pandas pipeline and models.
The final PDF slide deck I showed to a room full of stakeholders at the end of my internship.


## Tech & Libraries I Used
* Platform: Databricks
* Languages: Python (Pandas)
* Visuals: Matplotlib & Seaborn
* ML Stuff: Scikit-Learn (`sklearn`), LightGBM (`lightgbm`), XGBoost
* Tuning: Grid Search, Randomized Search, and Bayesian Optimization (`skopt`)


### Phase 1: Cleaning Data
* Imported a massive dataset with about 500,000 rows of flight data.
* Had to learn Pandas from scratch.
* Checked the rows, columns, data types, and hunted for missing values.
* Found about 700 rows (flights) with missing data. Instead of just deleting them, I built a smart rule:
  * Looked at flights with the exact same alpha_route to see how common they were.
  * If it was a super frequent route (over 75% common), I filled in the missing value using the route history.
  * If it was less than 75% common or unique, I dropped that specific flight row.
* Figured out flight averages: longest vs shortest flights, average load factors, and how morning vs evening flights differed by month.

### Phase 2: Plotting Graphs and making the model.
* Made tons of Histograms and Scatter Plots to check how new features mapped against the load factor.
* Preprocessed the columns using One-Hot Encoding for categories.
* Checked for multicollinearity (making sure features weren't making the model less efficent by creating noise).
* Built a standard Linear Regression model to get a baseline score using R², RMSE, MSE, and MAE.

### Phase 3: LightGBM and extra models to explore curiosity
The baseline was fine, but I wanted to see if I could get a better score, so I experimented:
* Tried out LightGBM (decision trees) which handled the patterns way better.
* To tune it, I ran three different methods: Grid Search, Randomized Search, and Bayesian Optimization (using the `skopt` library).
* Also coded up XGBoost just to see how it worked compared to LightGBM (got similar scores), and tried to make a basic Neural Network structure just to explore it.

### Final Results
After the tuning and adding new features, the final LightGBM model hit:
* R² Score: 0.91
* RMSE: 3.7
* MSE: 25.4


## Stakeholder Presentation & What I Learned
At the very end, I had to present all of this to a big team of business stakeholders. 

* Business Value: Showed them the LightGBM improvements and calculated how many flights could be saved and how planes can be swapped due to load factor maybe higher or lower that causes the business to save money.
* Teamwork & Code: Learned how a real data team operates, how an Agile Workspace operates for projects (such as sprints), and found out how to code using pandas and how to use a business software such as databricks.

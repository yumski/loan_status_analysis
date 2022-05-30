# Loan Default Rate Analysis

This project aims to understand which customer features result in a loan going into a negative status. I will be using the data provided through the Udacity Nanodegree Capstone. I will be going through the entire machine learning process to answer this question, starting with data cleaning, exploratory data analysis, modeling, and data visualization.

## Motivation

Any lender must understand which client features lead to negative loan status. By quantifying each feature's impact, the stakeholders can make informed business decisions. These decisions can include adjusting the underwriting guidelines and fee structure or applying other risk management strategies. 

## Methods

This project is performed with Python 3, Jupyter Lab, and Power BI with XGBoost as the estimator. The initial data consisted of 113937 rows and 81 columns. Due to time and hardware constraints, I focused on nine out of eighty-one features. These features are loan amount, borrower's credit rating, loan APR, debt to income ratio, loan term, income verifiable, open credit lines, monthly income, and the loan status. I chose these features because, in my experience, these are the criteria lenders use to make underwriting decisions.

#### ETL:
1. Read the data with the Pandas library.
2. Used various methods to review the completeness and outliers of the data set.
3. Filled the null values by reviewing the data distribution and cross-referencing them with the data dictionary. I also identified outliers during this step and treated them appropriately depending on the situation.
4. Reviewed each data type and adjusted them if they were incorrect.


#### Exploratory Data Analysis:

In this step, I will go through each feature to perform univariate and bivariate analyses by visualizing its distribution and comparing the differences when separated by the loan status. Then, I performed the appropriate test to determine if the distribution of the different loan status were significantly different. 

Next, I performed a multivariate analysis to uncover trends between the variables. First, I calculated the correlation matrix to visualize relations between the numerical variables. Then, I used a category plot to visualize the relationship between each numeric variable, credit rating, loan status, and the verifiable income features. 

## Modeling

Imputed the missing values in the features that was not covered in the EDA process with SimpleImputer.

The estimator used for this project is the eXtreme Gradient Boost (XGBoost) model, a popular model due to its accuracy and speed. XGBoost is an ensemble model that utilizes the boosting technique, regularization, and the basic exact greedy formula to minimize the chosen loss function. Please see the analysis for in-depth details about the model.

#### Model Limitation

The limitation of XGBoost models is the interpretability of the features. Unlike a basic decision tree with only one tree, XGBoost utilizes hundreds, if not thousands, of trees to optimize the prediction. So it's much more challenging to quantify the feature's importance. Therefore, I ordered them by how much "Gain" resulted from splitting each feature in this analysis. The resulting feature importance is shown in the horizontal bar graph above.


## Results

#### Analysis Results:

- All variables were statistically significantly different when comparing the two loan status groups.
- 16.67% of loans are in negative status (late payment, default, or charged-off).
- Borrowers with lower than a C rating made up 38% of loans but 60% of total negative loans.
- There is around a 4% difference in APR when comparing the two loan statuses.
- Borrowers in the positive status are concentrated around 20% APR, while the other group has two peaks around 35%.
 - On average, Loans in negative status were around 2000 USD less than their counterpart; more than 80% of loans in this status were less than 10,000.
- Over 75% of loans were the 36-month term; however, it made up 89% of total loans in a negative status.
- 60-month terms only made up 21% of loans; however, this term only 10.3% of total negative loans. This term poses less risk for the organization.
- Borrowers in the negative status made around 1000USD less than the positive status.
- Borrowers in the negative status had one less credit line on average than the other group.
- Borrowers that couldn't verify their income have a 3.1% higher chance of being in a negative status.
- No strong correlation between the numeric variables and some positive correlation between loan amount and income.
- A slight negative correlation between APR and loan amount, meaning lower rates for bigger loans.
- Majority of the high-interest loans (>30% APR) are 10,000 or less.

#### Model Results:

- Model resulted in an accuracy score of 0.98, an AUC-ROC score of 0.944, a precision of 0.89, a recall of 0.99, and an f1 score of 0.94.
- The top features are principal customer payments, loan month since origination, original loan amount, estimated return, and monthly payments when ranked by gains.

## Discrepancies

- All borrowers that didn't verify income have the same DTI ratio.
- NC credit rating has lower than expected APR despite having the highest proportion of defaults.

## Dashboard
![Loan Analysis Dashboard](https://github.com/yumski/loan_status_analysis/blob/main/loan_analysis_dashboard_ss.jpg?raw=true)

## Next Steps

It is important to note that due to both time and hardware constraints, I used RandomizedSearchCV for hyperparameter tuning. Setting more detailed hyper parameters in conjuction with GridSearchCV will result in a better tuned model. My next step is to further tune this model with PySpark; as well as perform EDA on all 81 features.

# Propensity :
A Propensity Model helps to predict the likelihood that specific groups of customers will respond to a marketing campaign

## ABSTRACT

In today's competitive market, companies recognize the critical need for robust strategies to engage customers effectively. These strategies, grounded in data, are pivotal for achieving success and driving revenue growth. By leveraging customer data, businesses gain invaluable insights into their audience, enabling them to develop smarter, data-driven marketing campaigns. However, these campaigns often come with significant costs, and unsuccessful efforts can result in financial losses. Therefore, adopting cost-effective approaches becomes essential. This project showcases the efficacy of a propensity model in leveraging data science to pinpoint potential customers, offering a more efficient and successful approach to marketing that ensures a solid return on investment.

## GOAL

The objective is to develop a model that forecasts the likelihood of individuals, leads, or customers responding to marketing campaigns. This model utilizes various statistical techniques to analyze customer behavior and employs Machine Learning to estimate the probability of customer engagement with specific marketing strategies. The project encompasses the following components:

    Data Analysis: This phase involves preparing and exploring the data, along with creating visual representations to gain deeper insights.

    Modeling: Here, the focus is on constructing Machine Learning models designed to predict customer response probabilities to marketing efforts. This stage also includes visualizing and assessing models to identify the most effective one.

    Model Deployment Plan: This step revolves around readying the model for practical application, ensuring reproducibility, and confirming its viability in a production environment.## Architecture


![architecture](https://github.com/PRIYANKJAIN22/super-octo-disco.gite)


## Data
There are 2 datasets provided. They are:
1. Train.csv which contains historical data of customers who have responded in 
yes/no.
2. Test.csv which contains a list of potential customers to whom to market. We 
will be predicting whether the customer will say yes/no on this data.

The column ‘responded’ will be used as the target variable to train the model. The 
corresponding value in the ‘test.csv’ will be ‘propensity’, which will be final predicted 
output.
From here on in this report, ‘train.csv’ will be called as ‘input data’

## Data Analysis
The columns and its corresponding inputs are:
![columns](https://github.com/PRIYANKJAIN22/super-octo-disco.git)
As seen above, there are a lot of null values in various columns. We will be handling 
through methods like removing, imputing, etc.

## Data  Cleaning
### Remove Extra Columns:
We delete the 'id' and 'profit' columns since they aren't needed.
### Handle Missing Data:
1.For 'custAge', we replace missing values with the median age.

2.For 'schooling', we use the most common (mode) value to fill in gaps.

3.For 'day_of_week', we replace missing values with 'unknown'.

4.Adjust 'pdays' Column: In 'pdays', a value of 999 means it's the first call. We change these 999 values to '-1' to avoid treating them as outliers.



## Exploratory Data Analysis

We have used the ‘sweetviz’ package to visualize the data along with its features and  'Dataprep' package to understand dataset.
The Reports extracted  from  the mentioned packages are provided in different file.

### Correlation Analysis



![download](https://github.com/PRIYANKJAIN22/super-octo-disco.git)

we will be removing ‘pmonths’ column because  both ‘pdays’ and 
‘pmonths’ are  highly correlated. The former has a high variability 
with the output variable, so we are keeping it.


## Feature Engineering

#### Encoding
The following columns  are categorical and required to be encoded :
1. schooling
2. profession
3. marital
4. default
5. contact
6. poutcome

We are using One hot encoding to achive this.

#### Scaling
The dataset's numerical fields have inconsistent scales. For example, some values like custAge, pdays, and cons.price.idx are in tens, while others, like nr.employed, are in thousands. This inconsistency can cause inaccurate results in modeling. To fix this, we use the Standard Scaler algorithm to make the data uniform.

## Modelling
The propensity model is a classification problem. So, will be using various 
classification models to train our dataset. The models considered are:
1. Logistic Regression
2. Decision Tree
3. Random Forest
4. XGBoost
We will be selecting the best model based on the accuracy metrics in the model 
evaluation phase.

#### Sampling
For class imbalance, we are adding stratified sampling method to the train-test split 
so that relatively equal representation is present in both

### Logistic Regression
We will be having a 80:20 split for train:test.
#### Hyper parameter tuning
we used grid search method.

We fit the Logic Regression model with the given data with ‘responded’ as the Target 
variable.

#### Model Evaluation
f1 score: 0.43170320404721757

roc-auc score: 0.7486687848432696

accuracy score: 0.7955097087378641

### Decision Tree
We transformed the data as required and fit the data with Decision Tree Classifier
![decision tree (2)](https://github.com/PRIYANKJAIN22/super-octo-disco.git)

We found the optimum results with max_depth = 5

#### Model Evaluation
f1 score: 0.3924528301886792

roc-auc score: 0.7844553050027212

accuracy score:0.9023058252427184

### Random Forest
We fit the data with the Random Forest Classifier method. We found the optimum 
result with max_depth = 6 and n_estimators = 10
#### Model Evaluation
f1 score: 0..35856573705179284

roc-auc score: 0.8073617669123164

accuracy score: 0.9023058252427184

#####  classification report for the model
              
![classification report](https://github.com/Sakshi1234-debug/pronsifier/assets/149681034/bbc54b88-141e-4c9c-a4f6-232cb678cda7)
### Feature Importance
top 14 features
![Screenshot_24-4-2024_201224_](https://github.com/Sakshi1234-debug/pronsifier/assets/149681034/79cb30fb-15b6-43d1-95a2-299efcf66217)

### XGBoost
As part of boosting tree classifier, its time  for the XGBoost mode
#### Model Evaluation
With cross validation, we did with num_boost_round = 500 and nfold=5. We found 
the below result.
![cross validation](https://github.com/PRIYANKJAIN22/super-octo-disco.git)
f1 score: 0.38554216867469876

roc-auc score:0.7679971463454098

accuracy score:0.8968446601941747

## Findings
The evaluation metrics indicate that Random Forest Classification is the best model for our data. We will use this model to calculate the propensity score for the potential customers in 'test.csv'. We use the same fitting parameters from the training data and create a new column with the probability score. In this project, a score of 0.5 or higher is labeled as '1', meaning the customer is likely to buy our product. A score below 0.5 is labeled as '0', indicating an unlikely customer.

---
title: "Machine learning project: Predicting customer churn with telecom data"
date: "2020-09-12"
tags: ["Machine learning", "Python", "Churn"]
---

# H1 Machine learning project: Predicting customer churn with telecom data
Customer churn is when an existing customer stops doing business with a company.
This can be contractual, such as a customer who cancels their Netflix subscription. Or non-contractual, such as a customer who decides to not visit a grocery store anymore.

For this occasion, I will analyze a telecom dataset (source: Kaggle) and predict customer churn by using three different machine learning algorithms.

# H2 Parsing and cleaning
First, the data has to be pulled into python and parsed into a Data Frame
format to be able to apply machine learning techniques. I use the pandas library for this. I call the Data Frame telco (short for telecom company)
Python code block:
```python code block
import pandas as pd #import pandas library

telco = pd.read_csv("Telco-Customer-Churn.csv") #read csv into pandas Data Frame
```
Then I check for some missing values.
```python code block
telco.isna().any().any() # checking for missing values
```
The output tells us that we should be fine.

# H2 Exploratory data analysis
Now, lets explore the data a bit.
```python code block
print(telco.head()) # explore top 5 rows
print(telco.dtypes) # explore datatypes
```
The output reveals that we have 21 variables, mostly of a categorical datatype.

```python code block
print(telco['Churn'].value_counts()) # number of churners
```
Apparently 36.12 % of the customers in this dataset are churners.

```python code block
import seaborn as sns #import data visualization library

sns.countplot(x="Contract", data=telco) # contract distribution
sns.countplot(x= "gender", data=telco) # gender distribution

sns.distplot(telco['MonthlyCharges']) # MonthlyCharges distribution
sns.distplot(telco['tenure']) # tenure distribution
```
Most of the customers are in a month-to-month contract and the gender is evenly
distributed. MonthlyCharges are for most of the customers low and tenure reveals that most of the customers are a customer for a short time.

```python code block
sns.boxplot(x = 'Churn', y = 'Tenure', data = telco) # spreading of tenure
```
# H2 Data transformation
# H2 Model fitting
# H2 Model tuning

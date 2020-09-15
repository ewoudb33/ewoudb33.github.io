---
title: "Machine learning project: predicting customer churn with telecom data"
date: "2020-09-12"
tags: ["Machine learning", "Python", "Churn"]
---

Customer churn is when an existing customer stops doing business with a company (Peterson, 2020).

For this project, I analyzed a telecom dataset (source: <https://www.kaggle.com/blastchar/telco-customer-churn>) and predicted customer churn by using three
different machine learning algorithms.

The telecom dataset has 20 features and 1 predictor that shows if a customer has churned or not (Yes = churned and No = not churned). The top 5 rows of the dataset look like this:

<img src="{{ site.url {{ site.baseurl }}/images/head_telco.png" alt = "head of telco dataset">

The majority of the variables are categorical. I transformed them into a numerical scale, either with binary or with dummy variables, to meet the criteria of the machine learning algorithms.

### Exploratory Data Analysis
After exploring the data, I discovered that 36.12 % of customers are churners. This seems quite high because the industry average is around 21 % annually (Mazareanu, 2018).

<img src="{{ site.url {{ site.baseurl }}/images/churn-rate.png" alt = "">

The distribution of the contract type reveals that most of the customers are in a month-to-month contract.

<img src="{{ site.url {{ site.baseurl }}/images/contract.png" alt = "">

And after looking at the distribution of customer tenure, it seems that most customers just joined this company.

<img src="{{ site.url {{ site.baseurl }}/images/tenure.png" alt = "">

Finally, the relation of tenure and churn reveals that most of the churners have a low tenure. In other words, customers who just joined the company have a higher churn rate than customers who are longer at the company.

<img src="{{ site.url {{ site.baseurl }}/images/tenure-churn.png" alt = "">

### Model fitting
After transforming the data to a numerical scale and normalizing the continuous variables (to get closer to a normal distribution), I conducted three different machine learning algorithms: logistic regression, support vector machines, and random forests. Also, I removed the variables customer ID (because it’s useless for machine learning) and multiple lines (because it correlates heavily with the phone service feature).

The variables that are left to train the model are Gender, SeniorCitizen, Partner, Dependents, Tenure, PhoneService, OnlineSecurity, DeviceProtection, TechSupport, StreamingTV, StreamingMovies, PaperlessBilling, MonthlyCharges, and TotalCharges.

Below you can find a summary of the performance metrics of the three machine learning models:

**Classification report logistic regression**

|              | Precision | Recall | F1-score | Support |
|--------------|-----------|--------|----------|---------|
| 0            | 0.83      | 0.90   | 0.86     | 1515    |
| 1            | 0.68      | 0.53   | 0.60     | 595     |
|              |           |        |          |         |
| Accuracy     |           |        | 0.80     | 2110    |
| Macro avg    | 0.75      | 0.72   | 0.73     | 2110    |
| Weighted avg | 0.79      | 0.80   | 0.79     | 2110    |



**Classification report support vector machines**


|              | Precision | Recall | F1-score | Support |
|--------------|-----------|--------|----------|---------|
| 0            | 0.73      | 1.00   | 0.84     | 1541    |
| 1            | 0.00      | 0.00   | 0.00     | 569     |
|              |           |        |          |         |
| Accuracy     |           |        | 0.73     | 2110    |
| Macro avg    | 0.37      | 0.50   | 0.42     | 2110    |
| Weighted avg | 0.53      | 0.73   | 0.62     | 2110    |



**Classification report random forest**

|              | Precision | Recall | F1-score | Support |
|--------------|-----------|--------|----------|---------|
| 0            | 0.83      | 0.91   | 0.87     | 1541    |
| 1            | 0.67      | 0.49   | 0.56     | 569     |
|              |           |        |          |         |
| Accuracy     |           |        | 0.80     | 2110    |
| Macro avg    | 0.75      | 0.70   | 0.72     | 2110    |
| Weighted avg | 0.78      | 0.80   | 0.78     | 2110    |

The logistic regression model has the highest performance with a precision of 68 percent (i.e. 68 percent of the customers which this model classifies as churners are actually churners) and an accuracy of 80 percent (i.e. of al the decisions the model made, 80 percent were correct).

In the figure below you can find the feature importances of the logistic regression model.

<img src="{{ site.url {{ site.baseurl }}/images/importances_lr.png" alt = "">

According to the feature importances, customers who are in a month to month contract, have a fiber optic internet service, pay by electronic check, or have no tech support are more likely to churn.

And customers who have a two-year contract, a DSL internet service, no multiple lines, and no paperless billing are less likely to churn.

So far the basic models are doing quite well. In the next post, I am trying to get better performances by tuning the data and trying new techniques.

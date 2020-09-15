---
title: "Machine learning project: Predicting customer churn with telecom data"
date: "2020-09-12"
tags: ["Machine learning", "Python", "Churn"]
---

Customer churn is when an existing customer stops doing business with a company.

For this occasion, I will analyze a telecom dataset (source: Kaggle) and predict customer churn by using three different machine learning algorithms.

The dataset has 20 features and 1 predictor that shows if a customer has churned or not (Yes = churned and No = not churned). The top 5 rows of the dataset looks like this:

<img src="{{ site.url {{ site.baseurl }}/images/head_telco.png" alt = "head of telco dataset">

The majority of the variables are categorical. I transformed them to numerical, either with binary or with dummy variables, to meet the criteria of the
machine learning algorithms.

### Exploratory Data Analysis
After exploring the data a bit, I discovered that 36.12 % of customers are churners. This seems quite high, since the industry average varies around 25 %
annually.

The distribution of contract type looks like this:

<img src="{{ site.url {{ site.baseurl }}/images/contract.png" alt = "">

Month-to-month contracts are apparently the most popular.

After looking at the distribution of customer tenure, it seems that most customers just joined this company.

<img src="{{ site.url {{ site.baseurl }}/images/tenure.png" alt = "">

The distribution of tenure and churn reveals that most of the churners, have a low tenure. In other words, customer who just joined the company seem to have a
higher probability of leaving.

<img src="{{ site.url {{ site.baseurl }}/images/churn_tenure.png" alt = "">

### Model fitting
After transforming the data to a numerical scale and normalizing the continuous variables to get closer to a normal distribution, I conducted three different machine learning algorithms: logistic regression, support vector machines and random forest. The variables that are left to train the model are: Gender      , SeniorCitizen, Partner, Dependents, Tenure, PhoneService, OnlineSecurity,      DeviceProtection, TechSupport, StreamingTV, StreamingMovies, PaperlessBilling  , MonthlyCharges and TotalCharges.

The classification reports below show the performance metrics of the three machine learning models:

**classification report logistic regression**

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |



|              | Precision | Recall | F1-score | Support |
|--------------|-----------|--------|----------|---------|
| 0            | 0.83      | 0.90   | 0.86     | 1515    |
| 1            | 0.68      | 0.53   | 0.60     | 595     |
|              |           |        |          |         |
| Accuracy     |           |        | 0.80     | 2110    |
| Macro avg    | 0.75      | 0.72   | 0.73     | 2110    |
| Weighted avg | 0.79      | 0.80   | 0.79     | 2110    |


**classification report support vector machines**

|              | Precision | Recall | F1-score | Support |
|--------------|-----------|--------|----------|---------|
| 0            | 0.73      | 1.00   | 0.84     | 1541    |
| 1            | 0.00      | 0.00   | 0.00     | 569     |
|              |           |        |          |         |
| Accuracy     |           |        | 0.73     | 2110    |
| Macro avg    | 0.37      | 0.50   | 0.42     | 2110    |
| Weighted avg | 0.53      | 0.73   | 0.62     | 2110    |


**classification report random forest**

|              | Precision | Recall | F1-score | Support |
|--------------|-----------|--------|----------|---------|
| 0            | 0.83      | 0.91   | 0.87     | 1541    |
| 1            | 0.67      | 0.49   | 0.56     | 569     |
|              |           |        |          |         |
| Accuracy     |           |        | 0.80     | 2110    |
| Macro avg    | 0.75      | 0.70   | 0.72     | 2110    |
| Weighted avg | 0.78      | 0.80   | 0.78     | 2110    |

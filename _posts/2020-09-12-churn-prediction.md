---
title: "Machine learning project: Predicting customer churn with telecom data"
date: "2020-09-12"
tags: ["Machine learning", "Python", "Churn"]
---

# Machine learning project: Predicting customer churn with telecom data
Customer churn is when an existing customer stops doing business with a company.
This can be contractual, such as a customer who cancels their Netflix subscription. Or non-contractual, such as a customer who decides to not visit a grocery store anymore.

For this occasion, I will analyze a telecom dataset (source: Kaggle) and predict customer churn by using three different machine learning algorithms.

The dataset has 20 features and 1 predictor that shows if a customer has churned or not (Yes = churned and No = not churned). The top 5 rows of the Data Frame looks like this:

<img src="{{ site.url {{ site.baseurl }}/images/head_telco.png" alt = "head of telco dataset">

The majority of the variables are categorical. I will transform them to numerical, either binary or with dummy variables, to meet the criteria of the
machine learning algorithms.

After exploring the data a bit, I discovered that 36.12 % of customers are churners. Furthermore, the distribution of contract type looks like this:

<img src="{{ site.url {{ site.baseurl }}/images/contract.png" alt = "">

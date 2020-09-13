---
title: "Machine learning project: Predicting customer churn with telecom data"
date: "2020-09-12"
tags: ["Machine learning", "Python", "Churn"]
---

# Machine learning project: Predicting customer churn with telecom data
Customer churn is when an existing customer stops doing business with a company.
This can be contractual, such as a customer who cancels their Netflix subscription. Or non-contractual, such as a customer who decides to not visit a grocery store anymore.

For this occasion, I will analyze a telecom dataset (source: Kaggle) and predict customer churn by using three different machine learning algorithms.

## Parsing and cleaning
First, the data has to be pulled into python and parsed into a Data Frame
format to be able to apply machine learning techniques. I use the pandas library for this. I call the Data Frame telco (short for telecom company)

Python code block:
```python:
    import pandas as pd #import pandas library
    telco = pd.read_csv("Telco-Customer-Churn.csv") #read csv into pandas Data Frame
```
## Data transformation
## Model fitting
## Model tuning

---
title: "Machine learning project: predicting customer churn with telecom data -
model balancing"
date: "2020-09-16"
tags: ["Machine learning", "Python", "Churn"]
---

In this post I am trying to improve the performance of the previous best performing
machine learning algorithm, which was the logistic regression model.

Due to the fact that the two classes of churn are unbalanced, the accuracy output
can be biased. In other words, there are a lot more people who didn't churn than
people who churned in the dataset. Solving this issue, should improve the
f1 score (based on precision and recall).
In the figure below you can find the results of a balanced model.

**Classification report logistic regression (balanced model)**

|              | Precision | Recall | F1-score | Support |
|--------------|-----------|--------|----------|---------|
| 0            | 0.91      | 0.71   | 0.80     | 1546    |
| 1            | 0.51      | 0.81   | 0.62     | 564     |
|              |           |        |          |         |
| Accuracy     |           |        | 0.74     | 2110    |
| Macro avg    | 0.71      | 0.76   | 0.71     | 2110    |
| Weighted avg | 0.80      | 0.74   | 0.75     | 2110    |

As you can see did the recall score improve to 81 percent. An increase of 47.27
percent ! , compared to the basic model (recall was 0.55).

The recall score represents the percentage of churners that the algorithm
correctly classified as churners out of all the people that would actually churn.
In my opinion is this measure the most important, because not identifying a churner
causes a customer that silently leaves with a missed opportunity to convince him
to stay. 

Finally, the figure below represent the relation between the false positive rate
and true positive rate of the balanced logistic regression model with an
area under the curve of 0.7611.

<img src="{{ site.url {{ site.baseurl }}/images/auc_plot.png" alt = "">

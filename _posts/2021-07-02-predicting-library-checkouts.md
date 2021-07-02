---
title: "Predicting checkouts from a public library"
date: "2021-07-02"
tags: ["Machine learning", "R"]
---
In the previous post, I explored checkouts, dictionary, and inventory data from the Seattle Library in Washington. Now, I try to use machine learning to predict checkouts. To be clear, machine learning is a technique where computers learn
from data and can predict outcomes on new observations. Roughly spoken, you have two different areas: a regression and classification problem. With regression, you deal with a continuous dependent variable, and with classification, you have a discrete dependent variable (e.g. Yes or No). In this case study, I used regression, because the dependent variable is the number of checkouts, a continuous variable.

When I first started this analysis, I thought it would make sense to use the following independent variables: ItemType, Collection, CheckoutDateTime, Author, PublicationYear, and Publisher. Later I realized that there were some problems with some of these variables, which I will explain later.
The code I used for cleaning, preparing, and analyzing the data can be found on my GitHub.

I started to create a final dataset, where one row represents one library item. You might remember the variable BibNumer, which corresponds to a unique item, from the previous article. I used that one to group by and then counted the number of rows per unique BiBnumber. That resulted in a new variable called number_of_checkouts, which will be my dependent variable.

I merged the inventory dataset with this dataset to get the Author, Publication Year, and Publisher information.
Then I had to clean the final dataset because there were some inconsistencies in the author and publisher variables. Moreover, the variable CheckoutDateTime was in the American format (mm/dd/yy mm/ss AM) and I wanted to only have a number that represents one month.

After the cleaning was done I had a good dataset with all the variables I wanted to use in regression. There was still a problem left: 4 variables were categorical and regression only allows numerical data. So, I created dummy variables. At this point, I realized that the variables Collection, Author, and Publisher were impossible to use for dummy coding because they had way too many levels. There are more than 10,000 Authors. That many levels of a feature will most likely overfit the model, because of the low cardinality of some levels. Therefore, I decided to only use Month (dummy), ItemType (dummy), and Publication Year. Item type had 30 levels, which was okay in my opinion.

I used a linear regression model to fit the data. The first output gave some NA coefficients of the ItemType categories, which meant they correlated a lot with other categories. I removed those which resulted in the following output:

<img src="{{ site.url {{ site.baseurl }}/images/linear_model_library.png" alt = "">

Publication year is significant explaining checkouts. How more recent the publication year, how higher the number of checkouts. This proves our initial idea, which we discovered in the previous article. Also, the month variable is significant. January seems to be the most popular month to loan something from the library, and September the least.

I was a bit disappointed that the item types weren't significant, which means that they have no significant impact on checkouts and are useless for predictions. However, there is one item type that was highly positive significant: “pkbknh”. I looked it up in the dictionary and it stands for peak pick books. These books are the latest bestsellers as well as other new books that are in high demand. No surprise there.

What is interesting to know in this model is the accuracy of the model on the test dataset. Normally, with a classification problem, you would measure this in the percentage of correct guesses. For a regression model, this isn't a good measure, because it very hard to predict exactly the right number of checkouts. Therefore, I used the RMSE (Root of the mean squared error) to measure accuracy.

On the training dataset, the RMSE is 32.4345. This is okay since there are some data points in the 100s or even 1000s. To be 32 off, on average, is not that bad. The RMSE on the test dataset was 33.57729. That's very good because it is pretty close to our training dataset. It seems that our model can predict something outside his 'world' with the same error rate. Still, this model is quite basic and may be improved by including the author and publisher variable, with fewer levels.

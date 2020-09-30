---
title: "Sentiment Analysis: Analyzing bookreviews of 'A Very Private Gentleman'"
date: "2020-09-16"
tags: ["Sentiment", "R", "Exploratary Data Analysis"]
---

A couple of months ago I scraped some data from the bookreview website
goodreads.com from one of my favourite novels A Very Private Gentleman.

Today I will show some statistics and analytics of the analysis I did, which is
called a sentiment analysis. With sentinment analysis you identify and quantitfy
affective states of text.

Firstly, I looked at the distribution of the ratings.

<img src="{{ site.url {{ site.baseurl }}/images/distribution_of_ratings.png"
alt = "">

As you can see is the distribution left skweded. We have to keep this in mind
when we want to continue this analysis with machine learning. The average of user
ratings is 3.65, which is according to goodreads between "I liked it" and "I
really liked it".

The distribution of review length (i.e. the number of words per single review)
can be found below.

<img src="{{ site.url {{ site.baseurl }}/images/distribution_review_length.png"
alt = "">

This distribtuion is also very right skweded. Furthermore, In a user-review
for "A very private genteleman" are 250 words used the most. This is an half paged
essay, which should give us enough information for the sentiment analysis.

Let's look at the relation between review length and rating.

<img src="{{ site.url {{ site.baseurl }}/images/box_plot_review_length_rating.png"
alt = "">

There seems to be an increasing trend from rating 3 to rating 5 of the review
length, whith exception of the 2 ratings. There are also a few outlier in the higher
ratings.

Now, I calclulated the average sentiment score per rating. This sentiment score is based
on the Afinn Lexicion, which is based on a scale from -5 to +5.
How higher the score, how more positive the alogrithms sees the review.

<img src="{{ site.url {{ site.baseurl }}/images/average_sentiment_score.png"
alt = "">

Again, there is trend of a higher rating when the sentiment score is more positive.
No surprise right? We can conclude that our sentiment algorithm is working.

Next time I'll dive deeper in the data.

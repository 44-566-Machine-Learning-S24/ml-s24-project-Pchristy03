[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/7lKBcjfN)
# 44-566 machine-learning project
Repo for all project documents

Links to Each Markdown Section

* [RAW_DATA]("RAW_DATA.md")
* [DATA]("DATA.md")
* [ANALYIS]("ANALYSIS.md")
* [CONCLUSIONS]("CONCLUSIONS.md")


# Project Introduction and Overview

The Goal of this project was to take historical spending information and make predictions about someones future spending. As I moved along through this project I did switch resources and questions as I found or lacked information that was needed. My initial question for the project was "Are there noticeable seasonal variations in personal spending, and what are the main reasons for this shift and what aspects affect said spending?". While there were changes made to this question and the dataset I was using to support it, the question stayed relatively the same. They all revolved around predicting some spending amount whether that was in a certain time frame or a spending category. More detailed explanations of my question and dataset changes can be found below in the **project update** sections.


---

# Conclusion

As I moved through the final dataset it was obvious that there was a relationship between the time of the year and someones spending amount, but I struggled to capture that in a well constructed model. 

During the initial exploration using linear regression it seemed reasonable to me that the trend was not going to be linear. Thinking in terms of the spending habits of myself and the people around me, peoples spending does not increase in a linear fashion so I expected the [poor results]("linear_regression.ipynb") that I got.

Moving away from linear regression it was time to try another form of prediction, Decision Trees. Here I had to change my question a 2nd time since I was trying to predict exact numerical values which is not categorical which is required for a Descision Tree classifier. I decided to try and predict the week in a given year in which a transaction was purchased. This gave me 52 categories to work with. When running the selected features, they can be found [here]("classification.ipynb") along with model metrics, through the Decision Tree I ended up with a fairly good score compared to the the linear model before. To me this made sense. Here is my reasoning behind that, when thinking of someones yearly spending amounts it makes sense that different week/months would be more expensive than others. For example the weeks leading up to Christmas or other big holidays are inheritantly going to be more expensive for most. 

This data in my mind would not have clusters of high spending amounts but rather spikes or slight increases and then fall offs based on what I had encountered in the previous models and exploration. When trying out SVMs that feeling held true as they performed relatively the same as the linear model. A similar thing happened with clustering models like Kmeans, but I was able to move into a new a different question realm here. When graphing the relationship between the week of the year and total daily transactions amounts I could see that we could potentially divide those results into spending categories which led me to my final question "Can I predict someones spending category". This prediction is done using a few peices of information including the day the transaction was made, how much they spend on average, and the quantity of items bought. This yeilded a interesting categorization and something that I felt I could potentially improve on. Visual can be found here in [graphing the findings]("classification.ipynb"). My final push was to use a neural net  with this same information. When trying to predict the categorization it ended up yeild really high results compared to other models! With ~80% accuracy on both the train and test set I felt pretty good, but I quickly realized that something didn't seem right. I had a suspicion that around 80% of the data could be in one category which could lead to a model thats no better than a model who always predicted one thing. 

I believe there are discoverable trends to be found here, and I think that I am on the right track. Refining my neural net or potentially going back to my data and performing transforms on it for linear regression would be my next steps.

---

# Project Update (3-1-24)

###### Original Dataset: https://www.kaggle.com/datasets/wenruliu/adult-income-dataset/data
###### New Dataset: https://www.kaggle.com/datasets/abhishekrp1517/online-retail-transactions-dataset
###### Original Question: Are there noticeable seasonal variations in personal spending, and what are the main reasons for this shift and what aspects affect said spending?
###### New Question: Can I predict someones online weekly spending amounts using previous transaction data?

**New Dataset and Question**
---
I ended up switched datasets during the initial exploration portion. I quickly realized that the original dataset just didnt have the information I needed to answer the question at hand. I also refined my question further. I felt that data revolving around seasons would not be adequatly available so I went with using month, week, and day values instead. I ultimately want to use those values to predict somes online weekly transaction amounts. 

**Initial Exploration Findings**

---
It was quickly obvious that in order to get information out of the data provided I would need to calculate new features so thats exactly what I did. I began by extracting the day, week, and month out of the date provided for each transaction. I then calculated total cost per transaction, along with average weekly spending, daily spending, and total daily and weekly spending.

After calculating this data I had a much smaller subset of values to look at. I started off by graphing many of those values mentioned above and noticed a very strong pattern of were days/weeks at the start of the year had fewer transactions and lower transaction totals compared to days/weeks around and before the end of the year. My initial thought here is that people/companies are spending money for the holidays or tax related reasons at a more frequent rate compared to other parts of the year

**Linear Regression Findings**

---
After performing linear regression on the newly created features I ultimately didn't find any string correlations with an r2 value of 0.07 and a RSME value of 2.12. Like I mentioned above and in that notebook though I think thats because of how large some of the data points are compared to others, and how it doesn't appear to be a linear relationship. 

**Next Steps**

---
The next steps for this dataset is to scale values in a way that makes sense and then also try to fit the data to a function that is not linear. By following those steps I can further improve the models scores and predictive powers overall. 

---

# Project Update (3-22-24)

###### Dataset: https://www.kaggle.com/datasets/abhishekrp1517/online-retail-transactions-dataset
###### New Question for the classifier: Can I predict the week of the year that a transaction amount may have occurred on

**New Question**

--

I decided to change my questions because the values I was trying to predict originally was not a typical question that could be answered categorically. Since the weeks of the year are categorical I felt that it was related to the original question and could provide good insight into either the original question or a new question.

**Dataset Cleaning**

--

I went through the dataset and cleaned it just like I had with the linear regression on March 1st. I also added some new features, those being "average_cust_expend" and "total_cust_expend". After cleaning the dataset I split the dataset into training and test sets with a 20% split.


**Classifier Findings**

--

After sending the data through a DecisionTreeClassifier I ended up getting decent results from the training set, but I was very suspicious of overfitting. Ultimately running the test set through the model did show a lot of overfitting in the form of a much lower Accuracy and F1 score. Those scores decreased by around 20% from the training set to the test set. 

I sent the data through an SVM as well, but since the data is not clumped with distinguishable dividing lines it preformed terribly. The overall F1 score was < 0.02 and the Accuracy was less than 0.07.

--

**Next Steps**

--

I really think there are trends here that can be identified, but not with a categorical classifier. I really think that a linear model with a degree 2 or 3 transformation would yield much better results. In my next attempt I plan on attempting a few transforms on features such as transaction totals, average transaction totals etc.


# Project Update (4-12-24)


**Trying Out Clustering**

--

When trying out clustering I wanted to see if I could classify spending categories for people by looking at the transactions per day, the daily total expenditure amounts and the country category. Ultimately the data is not very clustered, but it was able to divide the data up into 3 sections that make sense. I personally don't think clustering is the best idea for this data.

**More Dataset Cleaning**

I added one new features to the dataset to see if I could get more information. The new feature is called "transaction_spending_classification". This classifies the a transaction amount based on the total transaction cost. The categorization is as follows:
```
bins = [0, 20, 100, 10000000]
categories = [1, 2, 3]
```

--

**Neural Net Findings**

I decided to go with a few different features this time for X, but I still wanted to predict the spending classification of a customer. The new X features are as follows:
```
"trans_day", "average_cust_expend"
```
Those values stand for the date of the transaction and the average customer spending on a given day. 

The results were ver promising from both the test set and the training set! The training set received an accuracy score of 0.83 while the test set got a score of 0.84. This is good in two ways. It shows that the model is not overfit and that its correct over 80% of the time when predicting what category the expenditure may be in!

--



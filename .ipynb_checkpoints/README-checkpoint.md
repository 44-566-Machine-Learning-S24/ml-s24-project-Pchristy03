[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/7lKBcjfN)
# 44-566 machine-learning project
Repo for all project documents

# Project Update (3-1-24)

###### Original Dataset: https://www.kaggle.com/datasets/wenruliu/adult-income-dataset/data
###### New Dataset: https://www.kaggle.com/datasets/abhishekrp1517/online-retail-transactions-dataset
###### Original Question: Are there noticeable seasonal variations in personal spending, and what are the main reasons for this shift and what aspects affect said spending?
###### New Question: Can I predict someones online weekly spending amounts using previous transaction data?

**New Dataset and Question**
I ended up switched datasets during the initial exploration portion. I quickly realized that the original dataset just didnt have the information I needed to answer the question at hand. I also refined my question further. I felt that data revolving around seasons would not be adequatly available so I went with using month, week, and day values instead. I ultimately want to use those values to predict somes online weekly transaction amounts. 

**Initial Exploration Findings**
It was quickly obvious that in order to get information out of the data provided I would need to calculate new features so thats exactly what I did. I began by extracting the day, week, and month out of the date provided for each transaction. I then calculated total cost per transaction, along with average weekly spending, daily spending, and total daily and weekly spending.

After calculating this data I had a much smaller subset of values to look at. I started off by graphing many of those values mentioned above and noticed a very strong pattern of were days/weeks at the start of the year had fewer transactions and lower transaction totals compared to days/weeks around and before the end of the year. My initial thought here is that people/companies are spending money for the holidays or tax related reasons at a more frequent rate compared to other parts of the year

**Linear Regression Findings**
After performing linear regression on the newly created features I ultimately didn't find any string correlations with an r2 value of 0.07 and a RSME value of 2.12. Like I mentioned above and in that notebook though I think thats because of how large some of the data points are compared to others, and how it doesn't appear to be a linear relationship. 

**Next Steps**
The next steps for this dataset is to scale values in a way that makes sense and then also try to fit the data to a function that is not linear. By following those steps I can further improve the models scores and predictive powers overall. 

---

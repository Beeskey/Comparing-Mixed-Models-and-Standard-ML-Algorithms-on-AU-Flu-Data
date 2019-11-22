## Introduction
For this project I wanted to explore generalized linear mixed models (GLMMs), which are used frequently in the social sciences. I'm curious about applying data science methodologies in this field and improving results. The goal for this project was to identify a GLMM package for Python and build predictive models with it, logistic regression, and random forest to assess pros and cons of each.

## The Data
The dataset for my analysis is 10 years (2008-2017) of laboratory-confirmed flu cases from the Australian Department of Health.
Columns include: Week, Age, Sex, State, Indigenous, and Flu type.
- Week: Cases from the previous week were recorded every Friday, thus the values are the year and date of the Friday following when the person was tested. Ex: 2018-01-05
- Age: Grouped in 5-year increments, i.e. 0-4, 5-9
- Sex: Male, Female, X, and Unknown, where X represents people who are neither male nor female, and Unknown represents people who didn't want to provide their sex or didn't write/enter anything for that field.
- State: Which Australian state the patient lives in. If not Australian, it's the state in which they were tested.
- Indigenous: The indigenous status of the patient, Indigenous, Nonindigenous, Unknown, or Not Available.
- Flu type: Which strain of flu was found: multiple subtypes of type A, type B, type C, and types A & B.

## Tools
- General & EDA: NumPy, Pandas, Matplotlib, Seaborn.
- Preprocessing: Scikit-Learn KMeans to create cluster feature, StratifiedShuffleSplit to create train and test datasets, and SMOTE for balancing data.
- Models: Pymer4 (Python wrapper package for R Lmer & Lme4), statsmodels discrete_model.Logit for statistical summary of logistic regression, Scikit-Learn LogisticRegression and RandomForestClassifier for prediction, GridSearchCV to find ideal parameters for random forest.

## Summary
My target variable was flu type, which I narrowed down to types A and B. The goal was to see if mixed modeling could produce a more accurate prediction on unseen test data than either of the other models. Unfortunately, I was not able to predict with Pymer4 due to an unknown error that caused the predict() method to return an array of the same length as the train data set. So, this project ended up being a lesson in some of the realities of data science: so many areas of the field are being explore and developed as I write this, and results are not guaranteed. Before finding Pymer4 I searched through statsmodels for an appropriate package. What I found, Binomial Bayes Mixed GLM, was promising, but ultimately beyond my current level of statistical understanding and had little in the way of articles and tutorials. 

Thus, I kept searching and found Pymer4, which looked good on the surface. After reading the documentation and learning a bit about R data types, I was able to fit a model with it! But, there ended up being an issue somewhere and, due to time constraints on my project, I was unable to look into other options. Had I more time, I would have just learned how to use the R packages, themselves, within my notebook. 

The best performing model ended up being the RandomForestClassifier, which scored 75.6% accuracy on unseen test data. Due to model speed and interpretability, however, I prefer the Logistic Regression model on unbalanced data, which scored a 74.2. Depending on what kind of error is more detrimental for the use case, the data could be balanced to produce higher Type I errors, or left unbalanced to produce higher Type II errors. The most significant features ended up being State, Month, and Year. Least significant features were Sex and Cluster.

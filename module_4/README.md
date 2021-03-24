## BANK Credit Scoring 

We have a Bank dataset with **retail Customers info**. We need to create analyze it, clean and prep the data, and then design a scoring model which will predict whether a Customer will default on a loan or not.

Please check **Kaggle competition** here https://www.kaggle.com/c/sf-dst-scoring

Project on:
- git https://github.com/Sasha1904/teo-rep/tree/master/module_4
- kaggle https://www.kaggle.com/alexandrakhudyakova/khudyakova-bank-credit-scoring/

### Initial Features: 
- client_id - Client id
- education - level of education (school, undergraduate, graduate, postgraduate, academic qualification)
- sex - sex 
- age - age
- car - car mark (Y/N)
- car_type - foreign car mark (Y/N)
- decline_app_cnt - number of previously declined applications
- good_work - "good" work marker 
- bki_request_cnt - number of requests to BKI (Credit Buneau Agency)
- home_address - home address category
- work_address - work address category
- income - income level
- foreign_passport - foreign passport mark
- sna - level of affiliation of the Borrower with Clients of the Bank 
- first_time - first time information obtained
- score_bki - BKI (Credit Buneau Agency) score 
- region_rating - region rating/ranking
- app_date - application date
- default - credit default mark

### EDA observations:
1. There are 73 799 rows in train set, 36 349 rows in test set, which gives us **110 148 observations** in total. 
2. There are **20 variables**:

    - **6 numeric** variables, one of them is a unique client identifier with no value for analysis ('client_id', 'age', 'decline_app_cnt', 'bki_request_cnt', 'score_bki', 'income')
    - **6 categorical** variables ('education', 'region_rating', 'home_address', 'work_address', 'sna', 'first_time'). One of them, 'region_rating', is apparently ordered variable, hence sometimes it is analyzed together with numeric ones.
    - **5 binary** variables ('sex', 'car', 'car_type', 'good_work', 'foreign_passport')
    - **1 date** variable ('app_date')
    - **1 target** variable ('default') and **1 temporary** column for differentiating train and test datasets ('Train'), both are binary variables.

3. **14 columns have float and integer values, 5 columns have string values** - most of the latter need to be transformed into integer values (by labelling categorical variables) and one (application date) - to datetime.
4. Only **13 out of 100** Customers default on their loans.
5. **Distribution for all numeric variables, with exception of BKI score, is skewed.** BKI score has near normal distribution. Region rating distribution is about normal, however there are 2 peaks. Others are right-skewed (have positive skewness), hence log transformation might be useful.
6. **Defaulted Clients** are generally younger, have more declined applications and more BKI requests, have higher BKI score, are from regions with lower rankings, and, apparently, have lower income.
7. **Pearson correlation coefficient** for numeric variables is low (0.21 and lower) which is good, meaning variables are independent. Risk of overfitting is low, hence we do not need to apply regularization at this point.

### Steps taken to improve the data and the Model:
- Dealing with Missing Values
- Dealing with Outliers
- Labelling Binary and Categorical Variables
- Feature Engineering, incl. One-Hot Encoding and adding Polynomial (Cross) Features
- Data Log transformation, Standartization
- Choosing Significant Variables, using ANOVA test, Mutual Information and T-test

# Employee Attrition 
Analytics Vidhya Job-A-Thon November 2021

## Approach
- The problem is to predict employee attrition, and analogous to customer churn, and a similar approach can be used to model the data as a binary classification problem  
- The data is present over a time frame (reporting_dates) for each employee  
- The aim is to predict if an employee will churn in the next six months  
- The target variable in the train set will be generated for each record as a binary output (0 or 1, with 1 indicating attrition)  
- Inspiration to developing the approach has been derived from [Korichi et al.](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiTstyCgKr0AhXr8HMBHRHNDqoQFnoECAgQAQ&url=https%3A%2F%2Fwww.esann.org%2Fsites%2Fdefault%2Ffiles%2Fproceedings%2F2021%2FES2021-110.pdf&usg=AOvVaw1KAM5JbjCDVAQJqBXg7f5q)  

## Data Processing  
- Add the last working date to all records as applicable (for attritioned emp_id)  
- Evaluate `tenure` of emp_id for each record {record_date - dateofjoining}    
- Evaluate `grade_chg_join` {designation - joining_designation}  
- Evaluate median salary at a particular period and difference from employee salary (salary - median_salary)  
- Separate out the test set i.e. records of employees of date '2017-12-01'  
- Create target variable `attr_risk` 
- Calculate time before attrition `t_attr` (in months) for all records (lastworkingdate - record_date) 
- Binarize above result and evaluate attrition risk `attr_risk` as per the formula:  
 ![image](https://user-images.githubusercontent.com/51357266/142773621-a133c373-28cb-4754-8e06-97931fcd8bc5.png)
- Encode categorical variables

### Features provided in set
![image](https://user-images.githubusercontent.com/51357266/142773283-c792c1bc-c150-4702-aa33-deab02058bc3.png)

### Features input to model
![image](https://user-images.githubusercontent.com/51357266/142773586-f75a0bec-95a9-4f4e-8c3a-5803375c0f07.png)


## Final Model
- The train set is modelled using XGBoost
- There are 43 features in the final set
- The model is tuned using RandomizedSearchCV using 15 folds of 60 iterations  

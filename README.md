# Arrival-Prediction
As Machine Learning Intern at Pandocorp
### Aim: 
To predict wheter a transporter will breach arrival at depot.

### Workflow
#### 1.	Created a separate dataframe containing only those columns relevant to arrival_breached_at 

    Columns: indent_type           

            contract_type         
  
  		actual_freight  
  
 		destination           
  
  		transporter           
  
  		created_date          
  
  		vehicle_type          
  
  		source               
  
  		customer              
  
  		arrival_breached_at 

#### 2.	Extracted new features from created_date column namely:

a.	Created_date_day: date ranging from 0 to 30

b.	Created_date_weekday: day of the week ranging from 0-6

c.	Created_day_month: month ranging from 0-11

d.	Created_date_hour: hour ranging from 0-23

#### 3.	Converted arrival_breached_at column to binary numerical format follows:

0.0	– arrival was not breached

1.0	– arrival_was_breached

#### 4.	Clubbed market and no freight indent type into a single category(nfam).

-both of them had no arrival breached and negligible feature importance as compared to open and contract indent types when later checked by feature importance.
 
#### 5. Scaled actual_freight column using robust scaler

#### 6.	Filled null values in the following columns:

            a.	Transporter - Other

            b.	contract_type - Other

            c.	actual_freight -0.0

            d.	vehicle_type - Other

            e.	destination - Other

#### 7.	Calculated percentage of times each transporter has breached arrival

#### 8.	Created list of transporters who have always breached arrival and those who have never breached arrival, and clubbed all transporters who have always breached arrival into a single category (always_breached_transporter), and all transporters who have never breached arrival into a single category (never_breached_transporter)

#### 9.	Removed rows having customer as QA or Sandbox (dummy data)


#### 10.	Performed one hot encoding on all categorical variables in a way that the category name is retained as the column name, to be able to analyse importance of individual categories later


#### 11.	Separated arrival_breached_at from the dataframe and created a new dataframe (arrival_y).


#### 12.	Dropped categorical features which had been one hot encoded


#### 13.	Performing PCA:

            a.	determined number of components by plotting cumulative variance explained vs number of components
 
            b.	chode the optimum number of PCA components and performed PCA to downscale the data


#### 14.	Derived the most important features for each component and analysed importance of each category 


#### 15.	Divided data into train and test sets in the ratio 80:20


#### 16.	Over sampled the training data using SMOTE to remove class imbalance

Percentage of fraud counts in original dataset:11.24%

Percentage of fraud counts in the new data:50.0%


#### 17.	 Applied random forest classifier with max_features parameter set to ‘log2’ and all other hyperparameters set to default.


#### Test set metrics:

Accuracy:  0.938240430452636

Recall:  0.766799246388947

Precision:  0.7189401373895976

f1 score:    0.7420988654781199


#### Training set metrics (original imbalanced training set):

Accuracy:  0.9943066167143574

Recall:  0.9838565494031656

Precision:  0.9660264353572904

f1 score:  0.9748599713429725

#### Training set metrics (oversampled training set):

Accuracy:  0.9967237735748747

Recall:  0.9977936974175627

Precision:  0.9956631299734748

f1 score:  0.9967272751412317

### Practices tried to prevent overfitting:

1.	Clubbing categories on the basis of frequency.

-	Clubbed categories in source and destination having frequency less than a certain threshold (10, 20, … 50)

2.	Clubbing categories on the basis of target variable

-	Clubbed categories in transporter, source and destination for which the percentage of breaches in arrival was 100% and 0%

3.	Clubbing categories based on feature importance

-	Clubbed categories which did not lie in the top 50 most important features for each PCA component

4.	Performed hyperparameter tuning for the following parameters:

            a.	Increasing n_estimators

            b.	Decreasing max_features

            c.	Decreasing max_depth

            d.	Increasing min_samples_leaf



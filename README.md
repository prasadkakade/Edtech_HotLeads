# Edtech_HotLeads
* Run the code file 'Lead Scoring Case Study' with 'Lead.csv' as input file.

## Problem Statement
An education company called X education which sells online courses to industry
professionals is suffering from poor conversion rates to their courses. So, they want
us to build a model which helps them identify their most potential leads ('Hot leads'),
so that they can be targeted easily by the Sales team to increase their conversion rate.
We'll perform Logistic Regression on the given data and generate the lead scores
using the converted probabilities.

## Analysis Approach

#### 1. Loading and understanding the data
* By reading the given data, we know that there are 9240 rows and 37 columns.
Then we understood it’s summary, data distribution, data types and null values
in each of the columns.

#### 2. Data Cleaning
* First, we dropped the columns with high number of unique values.
* ‘Select’ category is present in 4 columns namely ‘Specialization’, ‘How did
you hear about X education’, ‘Lead profile’ and ‘City’. For ‘Specialization’
column, we filled this with ‘Others’ and for the other columns, we considered
it as null values for our analysis.
* We dropped all the columns having null values greater than 35% as we
cannot get proper insights from such columns. Mode and median
imputation were done for the missing values in categorical and numerical
columns respectively.
* Columns with highly skewed data (having more than 90% of their values in a
single category) were removed. They would have made our model biased.
* We used count plots to get the distribution of categorical columns and to
understand which categories have high conversion rate, the boxplot to
analyse the distribution of numerical variables and identify the outliers and
heatmap was used to get correlation between columns.
* Outliers were identified and capped at 99th percentile.

#### 3. Data Preparation
* The columns with binary values, ‘no’ and ‘yes’ were mapped to 0 and 1
respectively.
* Dummy variables were created in the place of categorical variables.
* The data was split into train and test set in the ratio 70:30. X_train, X_test
had all predictor variables while y_train, y_test had the target variable
‘Converted’.
* The numerical columns were standardised using StandardScaler, for our
model to perform better.

#### 4. Model building
* Selecting top predictor variables using RFE
The top 15 predictors were selected using RFE technique. Then, we
successively removed variables having high p-values (> 0.05) and high VIF
(> 2) from the logistic regression model one by one.
The final model had all the predictors with p-values < 0.05 and VIF < 2. This
model consisted of 7 variables.
* Predicting conversion probability
The conversion probabilities were predicted for the train data using the final
model. Initially, we used 0.5 as the threshold value of probability, to predict
whether a person will convert into a lead or not.
* Calculating initial model metrics
Using confusion matrix, we calculated the model metrics such as accuracy,
sensitivity, specificity, false positive rate, positive predictive rate and
negative predictive rate.
Also, ROC curve was plotted to check the behaviour of model and it was
closer to the y-axis, which is a good sign.
* Finding the optimal threshold
Optimal threshold was identified by plotting the accuracy, sensitivity,
specificity against converted probability value and finding their intersection
point. We got 0.3 as the optimum threshold value i.e. if converted probability > 0.3, then it will be considered as lead.
* Calculating final model metrics and lead score
With 0.3 as threshold value for converted probability, model metrics were
calculated. We also calculated the lead scores by multiplying the conversion
probabilities by 100. Here, higher lead scores have higher probability of
getting converted i.e., they are hot leads.

#### 5. Model Evaluation & Results -
* After preparing the test data in a similar manner to that of train data, the
conversion probabilities were predicted for the test data using the final
model.
* Finally, model metrics were calculated and compared with the train data
model metrics. It turned out to be almost similar. So, the model is effective.
* By comparing the average scores of the converted and not converted, we
found out that converted has an average lead score of around 60 and not
converted has 20.

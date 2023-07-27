# Tips-Predictions
This program were made to predict how much money we should pay to the waiter(waitress) according to some information as are total bill, the amount of people, the time, etc.


# What have been used

Starting with project firstly we import all the important libraries, modules, models 
In this project were used
1. Pandas
2. Numpy
3. Scikit learn -> model_selection (train_test_split , GridSearchCV) / preprocessing (StandardScaler, OneHotEncoder) / linear_model (Ridge) / compose (make_column_transformer)
4. matplotlib.pyplot
5. plotly.express

To get comparatively better results we'll use linear regression model's special ridge regularization (RidgeRegression model)


# Starting the porject / Working with data

At first we must change our .csv file into pandas dataframe to start working with it

Use .info() to check whether there are missing values in our dataset

<img width="363" alt="Screen Shot 2023-07-27 at 11 57 51" src="https://github.com/Lunatikkkkk/Tips-Predictions/assets/110426439/1cdc9606-8eb4-4a28-8ace-89ffb1d8b1cf">
 
And as we can see there are no NULL values

****
Then create some graphics to see any kind of correlation between features

with px.scatter we will create scatter graphics with x = total_bill, y = tips , the color will indentify the day of the week and the size will be the amount of people


<img width="975" alt="Screen Shot 2023-07-27 at 12 07 17" src="https://github.com/Lunatikkkkk/Tips-Predictions/assets/110426439/d82ca93e-db45-4b95-80bb-bdff497cf302">

So we can understand that the higher is the total bill, the higher should be the given tips.

We can do the same thing but color can be indentified by the gender not by the day day of the week
****
And let's use the sb's pairplt() method to see the relation between each pair in our dataset

<img width="550" alt="Screen Shot 2023-07-27 at 12 15 47" src="https://github.com/Lunatikkkkk/Tips-Predictions/assets/110426439/a5d98756-64d6-4920-aa6f-92df77d5d818">

Imagine that each graphic is a square matrix, so if the all values are higher than the secondary diagonal of that matrix than we have 'positive' relations
so we again can see that in the second matrix almost all values are higher thab the diagonal, so the higher of value x (total_bill), the higher will be our y (tips)
****

Let's add new feature which will be bill_per_person = total_bill / size

Now check the impact of all features to the tip value using .corr() method

We'll get the following

<img width="302" alt="Screen Shot 2023-07-27 at 12 24 26" src="https://github.com/Lunatikkkkk/Tips-Predictions/assets/110426439/3a411d11-881f-4355-b286-88972cf68a29">

so the new total_per_person has 34% impact to the given tip

# Splitting the dataset

We can calculate the hash of observations' identifier using some kind of a hashing function and split the data with it, but instead because we got not that large dataset we'll use another method

1. make y which will contain only labels of our project
2. make X which will be our dataset but with dropped labels
3. use train_test_split with test_size=0.2 and random_state=42 to create X_train, X_test, y_train, y_test

That's it we got our data splitted

# Working with the train dataset
 
So as was mentioned before we dont have missing values so we dont need to use imputer for our train data

But we can notice that we have a lot of categorical features, so we need to use OneHotEncoder to indentify them as 0s and 1s
Also we can use StandardScaler to do feature scaling but as results will show us later it is better not to use StandardScaler on them

to transform all the numeric and categorical features and merge them we'll use make_column_transformer

<img width="400" alt="Screen Shot 2023-07-27 at 12 45 31" src="https://github.com/Lunatikkkkk/Tips-Predictions/assets/110426439/9e2f4f4a-5a3d-43ae-bcde-48aa22cbbbcf">

As it is shown was used 'passtrough' just for merging and not doing anything to that values

So our tips_prep will do some changes to our X_train dataset and return us ndarray


# Model Selection and tunning with hyperparameters

In project description was required to use LinearRegression but I wanted to do some regularizations, so I used RigdeRegression in this project

It's good to use GridSearchCV for getting the best hyperparameters and solvers for our model, 

We set our param = {'alpha': [1,10,50,100], 'solver': ['svd', 'cholesky', 'lsqr'],}
this means that it will try to get the best combination of alpha-solver pair from written ones above

So we used GridSearchCV on our linear model with ridge regularization, it's time to check what we have got

For getting the scores we'll use cross validation to get the rmse score

<img width="500" alt="Screen Shot 2023-07-27 at 12 57 21" src="https://github.com/Lunatikkkkk/Tips-Predictions/assets/110426439/e5337cec-aa6a-415f-8a58-0094fbd3518f">

So we get our cross validation rmse meaon score 1.07


# Testing

Last thing we need is to use the model on our test set. So we take the X_test, then do some changes as we did with the X_train and use our model to get the predictions

<img width="554" alt="Screen Shot 2023-07-27 at 13 06 26" src="https://github.com/Lunatikkkkk/Tips-Predictions/assets/110426439/6bfd91fc-a18f-43de-b808-b08e7285d770">



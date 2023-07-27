# Tips-Predictions
This program were made to predict how much money we should pay to the waiter(waitress) according to some information as are total bill, the amount of people, the time, etc.


# What have been used

Starting with project firstly we import all the important libraries, modules, models 
In this project were used
1. Pandas
2. Numpy
3. Scikit learn -> model_selection / preprocessing / linear_model / compose
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

# Splitting the data
f



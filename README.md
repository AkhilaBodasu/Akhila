# Akhila
# -*- coding: utf-8 -*-
"""
Created on Tue Feb  8 10:37:24 2022

@author: akhila bodasu
"""
# TASK 1  # TSF GRIP TASKS
# simple linear regression

# importing libraries

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


# importing the data

data=pd.read_csv("https://raw.githubusercontent.com/AdiPersonalWorks/Random/master/student_scores%20-%20student_scores.csv")
data
data.describe()
data.info()

# VISULIZATION
plt.scatter(x = data['Hours'], y = data['Scores'], color = 'green') 
plt.xlabel('Hours')
plt.ylabel('Scores')
plt.title('No of hours vs Scores',fontweight=50, color="green")


 #DATAPREPROCESSING
 X = data.iloc[:,:-1].values  #independent variable array 
y = data.iloc[:,1].values  #dependent variable vector

# splitting the data

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=1/3,random_state=0)



from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train,y_train) #actually produces the linear eqn for the data


y_pred = regressor.predict(X_test) 
y_pred
y_test


#plot for the TRAIN data
 
plt.scatter(X_train, y_train, color='red') # plotting the observation line
 
plt.plot(X_train, regressor.predict(X_train), color='blue') # plotting the regression line
 
plt.title("Hours vs Scores (Training set)") # stating the title of the graph
 
plt.xlabel("Hours") # adding the name of x-axis
plt.ylabel("Scores") # adding the name of y-axis
plt.show() # specifies end of graph



#plotting for the TEST data
 
plt.scatter(X_test, y_test, color='red') 
plt.plot(X_train, regressor.predict(X_train), color='blue') 
plt.title("Hours vs Scores (Training set)") # stating the title of the graph
 
plt.xlabel("Hours") # adding the name of x-axis
plt.ylabel("Scores") # adding the name of y-axis
plt.show() # specifies end of graph


#### THE OUTPUT FOR THE GIVEN TASK : STUDENT WHO STUDIED 9.25 HOURS


print("score of a student who stuides for 9.25 hours per day is", regressor.predict([[9.25]]))



#here we check Mean Absolute error

from sklearn import metrics  
print('Mean Absolute Error:', 
      metrics.mean_absolute_error(y_test, y_pred)) 


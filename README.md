# Ames Housing Data: Modeling and Analysis

----

## Table of Contents

 - [Problem Statement](#Problem-Statement)
 - [Executive Summary](#Executive-Summary)
 - [Conclusions and Recommendations](#Conclusions-and-Recommendations)

----
## Problem Statement
 
We have received a comprehensive data set regarding home sales in Ames, Iowa from 2007 - 2010.  The set includes over 2,000 observations and has over 80 features including size, number of rooms, quality, and various style features.  We are tasked with cleaning the data set and building a regression model to best predict the home prices from a set of testing data.  In conjunction with this, we are to analyze which features are key drivers of home price and how best to utilize the model outputs.  Our problem statement includes three components: what are the factors driving home price in this data set?  How can prospective home buyers take advantage of this information?  And lastly, what are the next steps we can take with this model?

This project was completed with General Assembly in October 2019.

----
## Executive Summary

Our first step in this exercise was conducting a brief exploratory analysis of the data given.  There were three types of features in the set: numerical figures that could be measured that represented either discrete variables or continuous variables, ordinal features that contain a ranking of attributes within a feature, and nominal values that represented categorical variables.

The next step was cleaning the data we were given.  Notably, the file contained numerous null values that needed to be scrubbed.  For the most part, this was solved by converting numerical nulls to 0 and ordinal and nominal nulls to 'NA'.

Second, we had to reconcile certain data types and begin the process of removing columns that lacked predictive value.  For instance, we removed an extra ID column and changed the data type of zoning areas from numerical values to categorical values as there is no actual relationship between the numbers in the category and Sale Price.

Next, we began our Exploratory Data Analysis.  This included examining various statistical parameters of the numerical data points and identifying any trends that may need to be examined.

The next stage involved converting our nominal and ordinal variables to numerical figures so that they could be included in the model.  For the nominal features, we replaced each column with dummy columns filled with binary values indicating whether or not the home fell into a certain subset of the category.  For the ordinal features, we replaced the object names with a number based on where the home's feature fell in the ranking of the subset of features.  This will allow us to ascribe linearity to these figures and include them in the model.  We also completed some feature engineering that allowed us to create new variable tracking the relationship between others.

At this point, we conducted a more thorough deep dive into the data distributions through visualizations.  This included looking at histograms of certain variables, which gave us the realization that the log of sale price was more normally distributed than sale price and would actually be a better target variable for our linear regression models than sale price on its own.  Moreover, we looked at the relationship between various features and Sale Price to demonstrate the relationship between the two and what is driving home price.

Finally, we fit our model.  For our inputs, we included features with a greater than 0.3 or less than -0.3 R^2 value with sale price.  We naturally concluded that these would be true drivers and truly impactful in terms of making predictions, but the exact range was determined through trial and error to best maximize the bias/variance tradeoff.  To reiterate, our target was the log of sale price.  We then conducted a train test split with the training data and fit our linear regression model to the data.  We then completed Lasso and Ridge regression models with the scaled versions of our features.  

Finally, to determine our best model, we conducted various forms of testing on all three of our models including cross validation scores, r^2 figures, and root mean squared error values.  Ultimately, our three models came out roughly in line with each other with root mean square errors in the low 20,000 range.  Ultimately, we decided to use our linear regresion model for discussion as this is the most interpretable for a broad range of audiences.

Finally, we answered the three components of our problem statement in the Conclusions & Recommendations section (please see below).

----
## Conclusions and Recommendations

My problem statement is ultimately, what are the factors driving home price in this data set?  How can prospective home buyers take advantage of this information?  And lastly, where can we take this model from here?

To begin with, we would like to restate some ideas behind my model.  First of all, the target variable is a log of the sale price, not the sale price itself.  We noticed that the sale prices follow a distribution with a positive skew on their own; after taking a log of the price, we find the prices following a normal distribution.  Moreover, we took a log of the above ground living area as this follows the same distribution as the sale prices.  Finally, I looked at including features with varying degrees of correlation with sales price and ultimately found that our best model that had the best fit along the bias/variance tradeoff included features with a more than 0.3 or less than -0.3 R^2 value with the sale price.  Ultimately, all of my models performed similarly well and there is not much to differentiate them given that R^2 scores and Root Mean Squared Errors are roughly in line between them.  Therefore, I selected the Linear Regression model given that it is easier to discuss to a broader range of audiences.

Returning to the problem statment.  For the first part (regarding what factors are driving home prices), some of the answers are fairly obvious and are backed up by both visualizations of the data as well as the final coefficients of our model.  The three features with the strongest beta coefficients in our model are lot area, living area (log version), and whether or not the sale price was new.  The first two are fairly obvious and do not require much additional explanation - the bigger the property, the more expensive it is.  The third is also fairly intuitive in that newer homes are likely nicer and more in line with current trends.  High up on this list of factors driving home prices includes other factors that should seem fairly obvious - overall quality of the home, various internal system qualities, and certain neighborhoods.

The more interesting question to us are the features that help drive the model that are not quite so obvious on the surface.  We note that some of this may be noise, but it is worth discussing.  These features include various, what I would call, style features, such as Vinyl Exterior Siding, having fireplaces, and having strong basement finishes.  Moreover, having a strong concrete foundation was heavily correlated with price.  Although this seemed odd at first, we realize this may be largely due to the regions propensity for tornadoes and as such this is not too suprising.  Additional features can be found in the coefficient analysis section of the code book.  

This leads us to the second question, which is how can homeowners take advantage of this?  We feel that homeowners who are willing to sacrifice certain style features are going to be able to get a strong house in terms of both size and quality may not have the most up to date or trendy features in conjunction with it.  Certainly there is a cost benefit analysis to such decision making but in terms of where this model can become useful, we feel that this is a key spot for it. 

Finally, where can we take our model from here?  First things first, we do realize the need to update this with new information to make forward looking decisions.  However, assuming we are able to do this, we would like to note that this model can be used to find value on the home market, and especially for middle income residents as our model is particularly accurate for these types of homes.  We would do this by noting when our model has a home price far above its listing price - it stands to reason that this may be a deal worth looking at. Second, we would look forward to seeing which coefficients that are important in our model change as time goes on - this may be an interestin way to track trends and once again, find the certain styles to avoid to drive value in other aspects of the home.
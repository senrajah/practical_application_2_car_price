# priceofacar
GitHub Repository for work done on Professional Certificate in Machine Learning and Artificial Intelligence - December 2022

# Practical Application Assignment 11.1: What Drives the Price of a Car?

**Contents**

 * [Introduction](#Introduction)
 * [Business Understanding](#Business-Understanding)
 * [Data Understanding](#Data-Understanding)
 * [Data Preparation](#Data-Preparation)
 * [Regression Models](#Regression-Model)
 * [Findings](#Findings)
 * [Next steps and Recommendations](#Next-steps-and-Recommendations)
 
## Introduction

The objective is to build a model to find out what features impacts and make the price of the car more expensive or less expensive, for this we used a data from kaggle at this location [vehicles.csv](https://github.com/yemifalokun/priceofacar/blob/main/data/vehicles.csv), if vehicles features like Fuel, Condition, Size, Type, Color etc. can be used to determine used car prices for the Car Dealership and Sales Team. This evaluation will help the Car Dealership with fine tuning their inventory by stocking cars that consumers are interested in.

## Business Understanding

Again the objective is build a model to identify the features which impacts the car price by building a linear regression model. 
For this we follow the CRISP-DM frame work.

Source - https://centricconsulting.com/blog/machine-learning-a-quick-introduction-and-five-core-steps/

We analyse the data and prepare dataset that would be fit to train and fit the model. For this we follow the data preparation and split the data into train and test.

We build the model and train the model with the training data set and use the test dataset to evaluate the model and find their accuracy and score to find the best fit model.


## Data Understanding
The provided data consists of the features like color, fuel type, odometer reading, year, engine type etc. The data is not ready to fit the model straight away, since it has NaN values in most of the features and also some of the columns are irrelevant to the model or they does not have any relation to the price of the car like ID, VIN etc

## Data Preparation

We had to do the below to prepare and cleanse the data
- Drop all the records with NaN values
- Drop records with 0 values on the odometer and price, since they are not much of use
- Drop features like ID, VIN, Region, state etc - irrelevant for price prediction
- Also since most of the data are with Auto transmission - we removed those feature too
- After the analysis we also find that the cars does not have much variance till the year 1990 - so we would consider only data after 1990


## Regression Models

We built several models with several features upto model 7. Each one with filters and including and excluding some features.

Filtering (i.e., Price and Odometer > 5000 and Year > 1990) were also used to create datasets used from some of the models below.

For Most of these Models, the accuracy was less than 50% with the exception of the last 2 models. See table below:


| Model Name  	| Description                                                                                                                      	| Accuracy Score (Training) 	| Accuracy Score  (Test) 	|
|-------------	|:----------------------------------------------------------------------------------------------------------------------------------	|:-------------------------:	|:----------------------:	|
| Model       	| Built with all features from data manipulation dataset                                                                           	| 44.54                     	| 43.09                  	|
| Model1      	| Odometer and Year as inputs from data manipulation dataset                                                                       	| 6.94                      	| 1.92                   	|
| Model2      	| Odometer and Price greater than 5000, Odometer and Year as inputs                                                                	| 12.45                     	| 12.54                  	|
| Model3      	| Odometer and Price greater than 5000, Year as the only input                                                                     	| 0.3                       	| 0.26                   	|
| Model4      	| Odometer and Price greater than 5000, odometer as the only input                                                                 	| -97.45                    	| -96.91                 	|
| Model6      	| Odometer and Price greater than 5000 with Odometer, Year, fuel_diesel, drive_4wd  and size_full-size as the only inputs              	| 45.26                     	| 46.88                  	|
| Model7      	| Odometer and Price greater than 5000 and  Year > 1990 with Odometer, Year, fuel_diesel,  drive_4wd and size_full-size as the only inputs 	| 47.52                     	| 48.26                  	|
|             	|                                                                                                                                  	|                           	|                        	|

Based on the scores, there is still some way to go to get to a model with a higher accuracy score with the highest score for training and testing data currently less than 50%

## Findings


For ML Applications ``Model6`` and ``Model7`` which are the recommended/selected models, see below for the prediction testing results:

| Test Description                                                         	| Predicted Used Car Price Model6	| Predicted Used Car Price Model7 ($)	|
|:--------------------------------------------------------------------------	|:-------------------------------:	|:-------------------------------:	|
| Car with Year of 1940, 100k Miles with Diesel Fuel, 4WD and Full Size    	| 38,785.04                      	| 39,107.49                      	|
| Car with Year of 1990, 100k Miles with No Diesel Fuel, 4WD and Full Size 	| 22,417.60                      	| 22,569.71                      	|
| Car with Year of 2020, 10k Miles with Diesel Fuel, 4WD and Full Size     	| 47,456.98                      	| 48,238.24                      	|
| Car with Year of 2020, 10k Miles with No Diesel Fuel, 4WD and Full Size  	| 31,089.55                      	| 31,700.49                      	|
|                                                                          	|                                 	|                                 	|

With regards to high quality model based on the dataset provided, ``Model6`` and ``Model7`` are the recommended models.

When we analyze the importance of feature selection based on the trained model, we observe the following order
- ``Model6`` - Diesel Fuel, Odometer, Four Wheel Drive, Full Size and Year
- ``Model7`` - Diesel Fuel, Year, Odometer, Four Wheel Drive and Full Size


## Next Steps and Recommendations


As analysed in the above models, ``Model6`` and ``Model7`` would make send and be the recommended models to use.  

These models were built with the following logic:
- ``Model6`` - Odometer and Price greater than 5000, Odometer, Year, fuel_diesel, drive_4wd  and size_full-size as the only inputs
- ``Model7`` - Odometer and Price greater than 5000, Odometer, Year > 1990, Year, fuel_diesel,  drive_4wd and size_full-size as the only inputs

These models  provided the following model feature selection:
- ``Model6`` - Diesel Fuel, Odometer, Four Wheel Drive, Full Size and Year
- ``Model7`` - Diesel Fuel, Year, Odometer, Four Wheel Drive and Full Size

For Next Steps, while the recommended models (i.e., ``Model7`` etc.) can be deployed, we would also recommend gathering more quality data that would produce a model with an accuracy of 75%+ based on used cars data no more than 10-15 years old.

Updated data should also provide a better indication on the latest features that consumers are looking for so that the Dealership can source these cars for their inventory.

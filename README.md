# NYC-Boro-Taxi-Tip-Predictions

This project focuses on a dataset describing the trips completed by NYC Boro taxis (green taxis) in the month of September 2015. These taxis can pick up passengers in all boroughs of NYC – except few areas in Manhattan. The dataset provides details regarding various aspects of each trip - ranging from the duration of the trip, pickup and drop-off locations, passenger count per trip, trip distance, fare amount charged, tip amount received, payment methods, and so on. The overall objective of this study is to analyze patterns and trends (i.e. exploratory data analysis) in the data available, and to eventually be able to predict the tip amount (in US dollars) a taxi driver is likely to receive for a particular trip by using statistical learning methods that are trained to leverage the granularity of data at hand. 
To begin with, we explore the dataset we have obtained and its characteristics. As observed, the data consist of  approximately 1.49 million trips that can be described using 21 features. Upon conducting a preliminary analysis of the distances covered per taxi trip, it is evident that more than 75% trips are short hauls (4 or less miles). Also, the mode of trip distances covered in that month is ~ 1 mile, which will also be factored-in, when predicting the tip amount for every journey. Next, another pattern that can be noticed here is the significantly higher likelihood of long hauls in the hours outside the time window for general working hours (9am to 9pm) on a given day – the mean trip distance during working hours is 3 miles or below, whereas it spikes to higher average distances (4 miles or more in some cases) outside that window. Another thing to note, is that about 0.28% (4217 trips) of the total trips we to and/or from airports serving the NYC metropolitan area. The average fare for these tips is found to be significantly higher ($49) compared to the overall average fare for all trips ($15.03, the median is even lesser at $11.76). This could be a result of multiple features, longer trip distances, the location of pickup/dropoff, trip duration, and so on. For most trips to and/or from airports, payment is done using credit cards (~ 3000 trips) rather than cash(~ 1200 trips) – which might also play a role in the tip being handed out to the taxi driver (hypothetically, a tip is much more convenient when given out via credit card payments rather than cash payments which can be difficult since the exact change might not be at hand).
Moving on from the exploratory data analysis, we build a calculated metric for tip as a percentage of the fare amount charged for each trip (i.e. tip to fare percentage ratio will be the response variable). This will be the metric that we shall predict using the data available here. A correlation matrix displays appreciable correlation between the response variable and the following predictor variables – payment type, trip distance, fare amount and trip type (street-hail or dispatch). Further, upon performing Forward Subset Selection (FSS) for feature selection, it is evident that the best predictors in decreasing order of importance are Payment type, Trip type, improvement surcharge, VendorID, Pickup longitude & Pickup latitude, Fare amount, Trip distance. We shall proceed to using these to train our statistical learning models for prediction. 
For training and testing purposes, we split the data in a 75:25 ratio – i.e. 75% of the data will be used for training and the rest for testing our models’ predictions. We employ the pickup and dropoff times as predictor variables, in addition to the ones chosen based on FSS to predict using a linear regression model. Based on the first iteration, it is evident that a few of these are better at predicting our response variable compared to others. We try a second iteration of the regression, discarding a few of the predictor variables and the resultant model explains about 60% of the variation present in our data. 
However, since a linear regression is a very crude model for prediction we move on to use a conditional decision tree model to better predict our response metric. Feeding the same response variables for prediction, the result of which provides is zero median prediction error, and a small mean prediction error (magnitude of 2.59 percent) over the test dataset. Further, by plotting the individual prediction errors (per trip) against the respective test observations, we can conclude that this model is only effective in predicting tips for trips that are likely to be awarded tips lower than or equal to 20% of the trip fare charged by the taxi driver.
As an additional exploration, we also explore the variation of average taxi speeds for trips pertaining to each hour of a day. As observed from the constructed visualization, taxi trips are slowest in the time frame when people finish work and travel back home (the 3pm to 8pm window). The hypothesis/conclusion that can be drawn based on this data is that - if one books a green cab in NYC within the 3pm to 8pm window on a given day in the month of September 2015, they should be prepared to put up with average trip speeds below 14 miles per hour.

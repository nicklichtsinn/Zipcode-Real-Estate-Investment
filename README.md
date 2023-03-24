# Zipcode-Real-Estate-Investment

## Introduction

Choosing where to invest money is crucial for long term success and financial stability, most trust funds and financial planners have different algorithms and ways to predict return on investment and where clients should invest money.

This project will use time series forecasting models created with Python to determine the three zip codes that are the best investment opportunity for a Real Estate Investment Trust. 

## Analysis

First I read in the dataframe with zillow data on average home value by zipcode over the last 20 years. 

![image](https://user-images.githubusercontent.com/94664740/227401328-16f76523-db24-4a5c-8fc0-39af7d9fa2a3.png)

I removed n’s from the data as there were some missing values for some zip codes. I then created a tim series line graph for each of AR largest metro areas, Hot Springs, Little Rock, Fayetteville and Searcy. I aggregated the graphs onto one visualization shown below.

![image](https://user-images.githubusercontent.com/94664740/227401391-a470d229-3e5c-4a84-ac35-b47c9e34bba9.png)

I then dropped the columns from the dataframe that would not be included in the ARIMA model. RegionID, City, State, CountyName, RegionType and StateName were removed.

I created a 5 year and 3 year ROI for each zipcode.

![image](https://user-images.githubusercontent.com/94664740/227401448-87a7bb62-9f5f-4626-b34c-9cb15e9c236d.png)

I then changed the data from wide format to long using melt and changed sipcode to a string and the date column to datetime. 

![image](https://user-images.githubusercontent.com/94664740/227401474-0845f6cf-d092-4e73-a23b-bd5607cdbbaf.png)

![image](https://user-images.githubusercontent.com/94664740/227401490-b33f78da-cf8f-47a3-9e27-29a909fa857f.png)

I plotted the average home value by month for all zipcodes and the top ten mean value zipcodes.

To limit the runtime for the processing of the model I took only the zip codes in the top 1% of ROI to use in the model and dropped the metro and sizerank columns so that I could feed the zip codes and values into a list to loop into a dictionary to use as a dataframe with each zipcode as a column and dates as rows.

I chose one zip code to use as a model to find the acf and pacf values.

![image](https://user-images.githubusercontent.com/94664740/227401541-74195400-9dc9-42a2-af9c-dd0bd8877baa.png)

A train dataset was created using 80% of the dataset and the remaining 20% was used to create a test dataset to test the accuracy of the models. I split the data into a train and test set with 80% of the instances used in the training set. And ran the arima model with a p, q and d of 1 to test the efficacy. 

![image](https://user-images.githubusercontent.com/94664740/227401573-c2aded0a-cdfa-4c44-bcf4-a0c0a0fe84d1.png)

As you can see the model did not accurately predict the test set so I used the auto arima package to find the optimal order for the model. The resulting model was SARIMAX(0,2,0) this was then used in a loop for all zip codes to predict home values through 2024 with an upper and lower confidence interval.

Below are the three most valuable zipcodes with the highest ROI based on the model.


![image](https://user-images.githubusercontent.com/94664740/227401624-e17e431f-a88b-4a7d-b124-f66380914297.png)


![image](https://user-images.githubusercontent.com/94664740/227401640-10d6d871-a0e5-4a67-bb27-b7a08832cc5d.png)


![image](https://user-images.githubusercontent.com/94664740/227401654-cd0783f7-5160-4e59-97cf-1a957be6f104.png)


## Conclusion

To down sample I took the zip codes with the highest calculated 5 year ROI. After using the auto arima to calculate the optimal order for the model the zip codes that would provide the best investment were 90020, 90212, 90211. These all provided a predicted ROI of over 1.7 and based on the confidence intervals have very low risk involved for the investor. There were other zip codes that were cheaper to invest in if the trust is low on funds but given the exponential increase in housing prices in California in recent years this investment strategy makes sense if the trust has the necessary capital to invest.


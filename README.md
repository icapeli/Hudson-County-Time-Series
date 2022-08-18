# FINDING THE 5 BEST ZIP CODES TO FOR REAL ESTATE INVESTMENT IN THE NYC SUBURBS
![image](https://user-images.githubusercontent.com/101752113/184942973-f7bc9ea3-39ca-4a1e-bdaa-8416f10b1748.png)

# SUMMARY
I have been retained in May 2018 by a Private Equity firm looking to expand into the New York City suburbs. In particular, they are targeting 4 of the closest and wealthiest counties in the area: Westchester County, NY to the city’s north, Nassau County, NY to the city’s east, and Bergen County, NJ, and Hudson County, NJ across the Hudson River to the city’s west. They want to know, quite simply, which areas should they invest in? Which areas will have the highest ROI in a 5 year investment horizon? 

Using an oustanding dataset from Zillow, the firm hired me to answer those questions. The dataset contains thousands of zip codes from across the country with the mean home sale price for each month from April 1996 to April 2018. I narrow the zip code down to the 201 zip codes in the relevant counties.  The data is clearly non-stationary and transformations have no effect. Splitting the data into an 80-20 train-test split, I define predicted ROI percentage as the last predicted price-the last training price/ the final training price. That number is then multiplied by 100 to generate a percentage.

![image](https://user-images.githubusercontent.com/101752113/184943420-36b5d437-da3b-45bb-b457-4369fc36a0a1.png)

The predicted highest performing zip codes in the next 5 years( May 2018 to March 2023) **were 10590, 10553, 11804,  10536, and 10504**.  However, the RMSE for each is very high, the confidence intervals are very wide, and the predicted values differ greatly from the test data. The differences are wide but may be a product of the Great Financial Crash and the disruption that event caused in the real estate market.


# BUSINESS UNDERSTANDING

The New York City area real estate market is perhaps the most valuable in the country and is among the most valuable in the world. According to Statista(https://www.statista.com/statistics/815095/new-york-metro-area-population/) , the combined population of the New York metropolitan area is almost 20 million people. When people think of the New York area, they often only think of the city proper consisting of the 5 boroughs of the Bronx, Manhattan, Queens, Brooklyn, and Staten Island. The city's fabled real estate market is lucrative but it’s important for investors to look beyond the city. The city’s suburbs form an essential part of the area’s economic ecosystem. The 4 closest counties to the city’s 4 most populated boroughs are Westchester County, NY to the north, Nassau County, NY to the east, and Hudson County, NJ and Bergen County, NJ to the west over the Hudson River. The city’s doctors, police officers, custodians, bus drivers, teachers, and bankers often reside in these counties.

This analysis will examine average home sale prices fromm every month from April 1996 to April 2018 to forecast which zip codes have the highest ROI the next 5 years. The projections are for 5 years because that is a typical investment horizon for a PE firm.

# DATA UNDERSTANDING

Zillow kindly provided average home sale data for each month from April 1996 to August 2018 for almost every zip code in the United States. Obviously, that is an immense amount of data. There are some counties with missing information so it’s certainly best to do a narrow search when using this dataset and to understand its limitations. The dataset consists purely of the months and the prices.

The evaluation metric I will use is Root Mean Squared Error(RMSE). RMSE is best for this case because (RMSE) will penalize large error terms. This is important because I want the error metric to be harsh because the predictions need to be as accurate as possible in order for the model to pass muster.

# MODELING

Out of the 201 zip codes that I examined, only was stationary. Therefore, I tried other transformations. however, none yielded a significant number of stationary zip codes. Therefore, I used pmdarima's auto.arima function. It is Python's version of R's auto.arima. I used auto.arima's default criterion, lowest 'AIC' value. The most common result was (0,2,0) which the data was differenced by a measure of 2. 

# RESULTS
![image](https://user-images.githubusercontent.com/101752113/184944904-446c461a-dce3-4502-9f3d-c666b0d6c372.png)

According to the model, the top 5 zip codes with the highest ROI% from May 2018 to March 2023 were 10590, 10553, 11804, 10536, and 10504.

![image](https://user-images.githubusercontent.com/101752113/184945073-edd58962-ffd3-4178-a850-0eeb6bdf6efb.png)

# EVALUATION


## 10590
* Test RMSE for baseline: 56830.818
* Test RMSE for model: 497165.197
* Predicted ROI_percent: 371.188
![image](https://user-images.githubusercontent.com/101752113/184945872-fb2547e4-5f49-4a16-94bb-0b9a17e4651b.png)

## 10553
* Test RMSE for baseline: 36555.793
* Test RMSE for model: 186502.012
* Predicted ROI_percent: 255.495

![image](https://user-images.githubusercontent.com/101752113/184946137-3193103b-2ce6-482b-9e52-a7496558204a.png)

## 11804
* Test RMSE for baseline: 36671.901
* Test RMSE for model: 278445.064
* Predicted ROI_percent: 190.459

![image](https://user-images.githubusercontent.com/101752113/184946409-a84fa348-c290-43f2-95f3-296427956f3d.png)

## 10536

* Test RMSE for baseline: 50051.282
* Test RMSE for model: 336974.519
* Predicted ROI_percent: 188.629

![image](https://user-images.githubusercontent.com/101752113/184946671-22ca5592-e54d-47b6-8998-8eb13b737ea4.png)

## 10504
* Test RMSE for baseline: 93168.259
* Test RMSE for model: 492617.709
* Predicted ROI_percent: 180.919

![image](https://user-images.githubusercontent.com/101752113/184947024-15944ed3-f611-414f-ac97-4248d5d6f2dc.png)


For each zip code, the predicted value far outstripped both the actual value and the baseline value for the time period. The confidence intervals for each zip code prediction is also very large. In 4 of the zip codes, the confidence intervals veer into negative $ amounts. Also, the difference in RMSE for the baseline model(a shift of 12 months) and the predictions was large. Overall, the wide discrepancy in the RMSE, actual ROI and the predicted ROI and the wide confidence intervals may raise doubts about the efficacy of the model and its predictions.

# CONCLUSION 

However, there may be meaningful reasons for the differences in RMSE, predicted and actual ROI and the wide confidence intervals. The wide confidence intervals are a product of either a small sample or a large degree of variation in the data. I cannot say whether the sample was big enough but the graphs of the prices suggest that the data has a high degree of variation. For each zip code in the dataset, there is a fall around the time of the Great Financial Crash or GFC(circa 2008). The values start to rise again in 2011 and either stabilize or continue to increase. However, the larger trend, from 1996 to 2018, is a significant increase for most of the zip codes. To speculate a bit, the discrepancy evidenced in zip code value in the predicted data and the baseline and original data for the top 5 predicted values may simply be the model anticipating  that the prices will move toward where it might have moved if there had been no Great Financial Crash.

# FINDING THE 5 BEST ZIP CODES FOR REAL ESTATE INVESTMENT IN HUDSON COUNTY, NJ
![image](https://user-images.githubusercontent.com/101752113/188214095-33d3b1e7-56db-44a7-827f-5bd729430e8c.png)

# SUMMARY
I have been retained in May 2018 by a Private Equity firm looking to expand into the New York City suburbs. In particular, they are targeting Hudson County, NJ across the Hudson River to the city’s west. They want to know, quite simply, which areas should they invest in? Which areas will have the highest ROI in a 5 year investment horizon? 

Using an oustanding dataset from Zillow, the firm hired me to answer those questions. The dataset contains thousands of zip codes from across the country with the mean home sale price for each month from April 1996 to April 2018. I narrow the dataset down to 13 zip codes in the county.  The data is clearly non-stationary and transformations have no effect. I define predicted ROI percentage as the last predicted price-the last observed price/ the final obeserved price. That number is then multiplied by 100 to generate a percentage.

![image](https://user-images.githubusercontent.com/101752113/184943420-36b5d437-da3b-45bb-b457-4369fc36a0a1.png)

First, I used pmdarima's auto.arima model but the RMSEs were too high and the confidence intervals were incredibly wide. Then, I employed a SARIMAX model. After grid searching for the optimal parameters (lowest AIC), I obtained results with lower errors although the confidence intervals were still wide. The predicted highest performing zip codes in the next 5 years( May 2018 to March 2023) **were 07029, 07030, 07302, 07032, and 07307. Furthermore, for investors looking for homes at or below 500k, they should target 07029 and 07032**.


# BUSINESS UNDERSTANDING

The New York City area real estate market is perhaps the most valuable in the country and is among the most valuable in the world. According to Statista(https://www.statista.com/statistics/815095/new-york-metro-area-population/) , the combined population of the New York metropolitan area is almost 20 million people. When people think of the New York area, they often only think of the city proper consisting of the 5 boroughs of the Bronx, Manhattan, Queens, Brooklyn, and Staten Island. The city's fabled real estate market is lucrative but it’s important for investors to look beyond the city. The city’s suburbs form an essential part of the area’s economic ecosystem. Hudson County, NJ is actually the closest suburbs to Midtown and Lower Manhattan and houses not only many of the city's professionals but also the middle and backend offices of many financial institutions.

This analysis will examine average home sale prices from every month from April 1996 to April 2018 to forecast which zip codes have the highest ROI the next 5 years. The projections are for 5 years because that is a typical investment horizon for a PE firm.

# DATA UNDERSTANDING

Zillow kindly provided average home sale data for each month from April 1996 to August 2018 for almost every zip code in the United States. Obviously, that is an immense amount of data. There are some counties with missing information so it’s certainly best to do a narrow search when using this dataset and to understand its limitations. The dataset consists purely of the months and the prices.

**The evaluation metric I will use is Root Mean Squared Error(RMSE). RMSE is best for this case because RMSE will penalize large error terms and large outliers**. 

# MODELING

Out of the 13 zip codes that I examined, only 1 was stationary. Therefore, I tried other transformations. However, none yielded a significant number of stationary zip codes. Therefore, I used pmdarima's auto.arima function. It is Python's version of R's auto.arima. I used auto.arima's default criterion, lowest 'AIC' value. Unfortunately, the errors here were too large and the confidence intervals too wide. Therefore, I used a SARIMAX model and was able to obtain more reliable results.

# RESULTS

![image](https://user-images.githubusercontent.com/101752113/188214095-33d3b1e7-56db-44a7-827f-5bd729430e8c.png)
![image](https://user-images.githubusercontent.com/101752113/188215334-52100b8b-1d63-4465-bb59-c75dc235fc94.png)

**According to the model, the top 5 zip codes with the highest ROI% from May 2018 to March 2023 were 07029, 07030, 07302, 07032, and 07307**.

![image](https://user-images.githubusercontent.com/101752113/184945073-edd58962-ffd3-4178-a850-0eeb6bdf6efb.png)

# EVALUATION


## 07029
![image](https://user-images.githubusercontent.com/101752113/188215638-b4f1ea63-3af3-430b-a45b-9b4eadbcfee0.png)

## 07030
![image](https://user-images.githubusercontent.com/101752113/188215772-41b0e0f5-b05a-407f-ac85-f19e115a0ca4.png)

## 07302
![image](https://user-images.githubusercontent.com/101752113/188215921-d77d5622-26e4-4c63-9164-f472b4ded374.png)

## 07032

![image](https://user-images.githubusercontent.com/101752113/188216014-cb2adb02-d041-4aae-a891-1251f9c020b3.png)

## 07307
![image](https://user-images.githubusercontent.com/101752113/188216107-e3bac9f1-26c4-413b-91aa-91dd284bbe32.png)

Each zip code has a positive ROI%. The RMSEs are better than the auto.arima model and, for some of the zip codes, are actually quite low. An objection may be raised to the fact that the confidence intervals are wide and even sink into the negative $ amounts for each zip code.

# CONCLUSION 

However, there may be meaningful reasons for the wide confidence intervals. The wide confidence intervals are a product of either a small sample or a large degree of variation in the data. I cannot say whether the sample was big enough but the graphs of the prices suggest that the data has a high degree of variation. For each zip code in the dataset, there is a fall around the time of the Great Financial Crisis or GFC(circa 2008). The values start to rise again in 2011 and either stabilize or continue to increase. However, the larger trend, from 1996 to 2018, is a significant increase for most of the zip codes. While I could I have used a truncated dataset that began after the GFC, I decided to include the GFC and pre-GFC data because this area is very tied to Wall Street so omitting that data would be doing investors a disservice. 

# NEXT STEPS
- An updated dataset that extends to 2022 would obviously be useful and would possibly generate more accurate predictions. It would also be interesting to see how a model would account for the COVID pandemic.
- More data on 07304 and 07310 would also be very useful to investors and to the model. Unfortunately, the Zillow dataset omitted these zip codes. 
- Lastly, another ML model may yield more fruitful results. An XGBoost Regressor or a neural network model may yield better and more meaningful results.

# REPOSITORY STRUCTURE

```bash
├── Data
│   ├── zillow_data.csv 
│   ├── zipcodes.json
├── .gitignore
├── README.md
├── phase_4_project.ipynb
├── phase_4_v2.pdf
```

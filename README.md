# Laptop Price Prediction : Exploratoratory data analysis and best line fit for Laptop data

Motivation:
  Buying a new laptop can get a bit trickier as there are 100s of brands available. I created an application which can help the consumer in chosing the laptop that suits them.
  This is a regression problem, and the prediction is done on the price as title suggests. TypeName, Inches, ScreenResolution, Cpu, Ram, Memory, Gpu, OpSys, Weight, TouchScreen, 
  IPS, X_res, Y_res are taken as independent variables.
  
Dataset Description:
  My first impressions of the data said that the data isn't clean. And it's quite clear that sufficient attention needs to be paid for this data during pre-processing.
  The sample data looks as follows:<br/>
  
  <img src="https://github.com/ferozqureshi/Laptop-Price-Prediction/blob/main/headlaptop.png" height="200" /> <br/>

## Process followed in solving the problem:
&nbsp; &nbsp;1️⃣Loading in data <br/> 
&nbsp; &nbsp;2️⃣Preprocessing the data <br/> 
&nbsp; &nbsp;3️⃣Creating different models <br/> 
&nbsp; &nbsp;4️⃣evaluating model performance <br/> 
&nbsp; &nbsp;5️⃣Hyper-parameter optimization <br/>
	
	
### 1️⃣Loading in data:
&nbsp; &nbsp;&nbsp; &nbsp;Pandas has been used to load the csv from local machine.
### 2️⃣Pre-processing the data
&nbsp; &nbsp;&nbsp; &nbsp;It was clear that pre-processing is an important step when I've seen the data for first time. Firstly, I've divided the columns into
categorical and numerical types; Company, TypeName, ScreenResolution, Cpu, Ram, Memory, Gpu, OpSys, Weight being the categorical columns and Inches, Price are 
numerical columns.<br/>
&nbsp; &nbsp;&nbsp; &nbsp;The price distribution can be viewed as below: <br/><br/>
&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;<img src="https://github.com/ferozqureshi/Laptop-Price-Prediction/blob/main/price_distribution.png" height="200" /><br/>
&nbsp; &nbsp;&nbsp; &nbsp;On observation I saw that if I remove "GB" from RAM, I can 
make it an integer value, now same goes with Memory and Weight. For Weight, I can classify it as floating variable
using the str.replace().<br/>
 <br/>
&nbsp; &nbsp;&nbsp; &nbsp;The heatmap looks as follows:<br/>
&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;<img src="https://github.com/ferozqureshi/Laptop-Price-Prediction/blob/main/heatmap2.png" height="200" width="500" /><br/>


&nbsp; &nbsp;&nbsp; &nbsp;From the correlation plot I've observed that as the X_res and Y_res is increased, the price of the laptop also increased. That means X_res and Y_res are positively correlated and they are giving much information, so that is the reason why I've splitted Resolution column into X_res and Y_res columns respectively. <br/>

&nbsp; &nbsp;&nbsp; &nbsp;To make things good, I've created a new column named PPI{pixels per inch}, now as we saw from the correlation plot that the X_res and Y_res are having much collinearity, so why not combine them with Inches which is having less collinearity. <br/>
&nbsp; &nbsp;&nbsp; &nbsp;Formula for PPI(Pixel Per Inch), PPI = √(X_resolution² + Y_resolution²) / inches <br/>
&nbsp; &nbsp;&nbsp; &nbsp;At the end of pre-processing, the data looks as below: <br/>
&nbsp; &nbsp;&nbsp; &nbsp;<img src="https://github.com/ferozqureshi/Laptop-Price-Prediction/blob/main/data_after_preprocessing.png" height="200" /> <br/>




### 3️⃣Creating models

I've fit the data for following models:
1) linear Regression 
2) Ridge Regression 
3) Lasso Regression 
4) Decision Tree 
5) Random Forest 



### 4️⃣Evaluating model performance
As this is a regression problem, I've used Mean Absolute Error as metric.
The values for different models are as follows:

1) linear Regression (MAE = 0.210)
2) Ridge Regression (MAE = 0.2092)
3) Lasso Regression (MAE = 0.211)
4) Decision Tree (MAE = 0.180)
5) Random Forest (MAE = 0.158)

From this we can conclude that using Random Forest yields best results.

### 5️⃣Hyper-parameter optimization
&nbsp; &nbsp;&nbsp; &nbsp;I've used RandomizedCv for Hyper-parameter optimization.<br/>
&nbsp; &nbsp;&nbsp; &nbsp;I've settled on the following values for random forest:<br/>
&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;RandomForestRegressor(ccp_alpha=0.0025, criterion='mae', max_depth=15,<br/>
                        &nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;max_features='log2', min_samples_leaf=5,<br/>
                        &nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;min_samples_split=14, n_estimators=588)}<br/>

  

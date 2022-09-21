# Renew-Power-Hackathon
Renew Power Hackathon organised by Machine Hack

APPROACH:-

Hackathon

Approach Presented By: Akshay Thorat

` `![](https://github.com/axethor512/Renew-Power-Hackathon/blob/main/Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](https://github.com/axethor512/Renew-Power-Hackathon/blob/main/Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.002.png)

Introduction

- In this hackathon, ReNew Power shared minute-wise normalized data of wind speed, power and temperature data for multiple components of a wind turbine. 
- The company is looking to create a model to get an ideally functioning turbine’s expected rotor bearing temperature.
- It will then use the model to check the deviation of the actual rotor bearing temperature of the faulty turbine from the expected temperature.![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.003.png)


Data Description

- Dataset is divided into 15 features and one Target variable
- 15 features can be broadly classified into 4 factors:
  - Power factor:- Active Power, Reactive Power (both raw and converted), generator speed and Average Power for 10 minutes.
  - Temperature factor:- Ambient Temperature, Nacelle Temperature(both inside and outside) and wire winding temperature
  - Wind factor:- Wind speed, wind direction, wind speed Turbulence
  - Other:- Timestamp and Turbine Id
  - We have to predict Rotor bearing Temperature.

` `![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.003.png)
Feature Engineering

Hypothesis 1: *Wind Speed and Ambient Temperature are Time and season specific. Hence, there is a need to extract time and season features from timestamp variable*

New Features created: - Hour (Time specific), Month(Season specific) Hypothesis 2 :- *Rotor Bearing Temperature is dependent on power loss*

New Features created: - Active Power loss, Reactive Power loss and Apparent Power(Active+Reactive)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.003.png)


Feature Engineering

- ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.004.png)
- ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.005.png)
- ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.006.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.003.png)

Exploratory Data Analysis-Univariate Analysis

- Most of the Features are right-skewed having high presence of outliers![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.007.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.008.png)

![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.009.png) ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.010.png)

- Target Variable is normally distributed having outliers present on both sides. It shares similarity with nacelle temperature ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.003.png)

![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.011.png) ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.012.png)


Bivariate Analysis:- Correlation

- We can observe that variables  ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.013.jpeg)are highly correlated. Specially  power factor variables are highly  correlated  ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.007.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.008.png)

Bivariate Analysis: Turbine Id vs Target

- Target variation is significant  ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.014.png)w.r.t Turbine id 
- We can observe that Turbine 20  and Turbine 1 shows high  variability in Rotor bearing  Temperature ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.007.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.008.png)

Bivariate Analysis: Hours vs Target

- We can observe that, Median  ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.015.png)Rotor Bearing Temperature do  increase in the noon. ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.007.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.008.png)

Bivariate Analysis: Months vs Target

- Median Bearing Temperatures are higher in the month of  ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.016.png)March, April, May and June. 
- March and April  data shows  High Variability. ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.007.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.008.png)

Feature Selection

- Since, Highly correlated features are present in the dataset. Feature Selection has been done to reduce noise.
- Method Selected:-Forward Feature selection
- Estimator Used:- Decision Tree Regressor is chosen over Linear Regression due to presence of outliers.
- Scoring:- MAPE

Feature Selection list

- Following were the features  ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.017.png)selected using forward feature  selection: ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.007.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.008.png)

Model Training

Model Training![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.018.png)

Scoring=‘MAPE

` `![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.003.png)

Decision Tree![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.019.png)

0.00825

Random Forest

0.007288![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.020.png)

Extra Tree Regressor

0.005512![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.021.png)

` `![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.003.png)

Model selection

- Extra Tree Regressor model was performing better than other ensemble models. Hence it was selected for final prediction![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.003.png)

![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.022.png)


Feature Importance

- We can observe that in Extra  ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.023.png) tree Regressor model training,  ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.024.png)following are important  features:- 
- Ambient Temperature:- Explaining 20 % variability 
- Turbine Id:- 23% variability 
- Month:- 28% variability ![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.007.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.008.png)

![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.025.png)
` `![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.001.png)![](Aspose.Words.39f3e8a0-66d5-466c-bc58-0ef9d6aec78d.002.png)

**Modeling-U.S.-Urban-Electricity-Prices-Using-Time-Series-Techniques**

Time series forecasting of U.S. urban electricity prices using SARIMA, Holt-Winters, and Facebook Prophet Models (with &amp; without external regressors)

<p> </p>

## **PROJECT SUMMARY**
As of May 2025, the average residential electricity rate in the United States was **0.182 dollar (18.2 cents) per kilowatt-hour (kWh)**. This cost can vary significantly depending on the geographic region, utility provider, and pricing plan. For example, Hawaii is among the states with the highest electricity rates, while North Dakota has some of the lowest. 

<img width="2091" height="770" alt="image" src="https://github.com/user-attachments/assets/e8373d6c-b494-4b38-80c5-20f5eacee9f3" />

<br> <br>
The primary objective of this project was to model and predict **average monthly electricity prices** ($/kWh) in the United States. To accomplish this, three time series forecasting techniques were applied: **Facebook Prophet**, **SARIMA**, and **Holt-Winters (Triple Exponential Smoothing)**. The dataset used in this project were collected from various sources, spanning from **January 1980 to March 2025**. Models were trained on data from **January 1980 to December 2022** and evaluated on a test set from **January 2023 to March 2025**.

To enhance prediction accuracy, several **external regressors** were incorporated into the Facebook Prophet and SARIMA models. Among the candidate models, the **Facebook Prophet model with external regressors** significantly outperformed SARIMA and Holt-Winters in terms of **RMSE** and **MAE**, indicating superior predictive accuracy. The inclusion of variables such as the **monthly production index of utilities**, **monthly population**, and a **gas price spike indicator** helped the model better capture volatility and seasonal behavior in electricity prices. In contrast, the Prophet model without external regressors and Holt-Winters yielded substantially poorer predictive performance.

The findings of this project highlight that both **historical patterns** (e.g., trend and seasonality) and **key external factors** play an important role in predicitng time-varying electricity prices. Practically speaking, the results provide valuable insights into long-term electricity price trends and can help decision makers in prioritizing **infrastructure investment** and **operational planning** efforts in the energy sector.

---
---

## **Data Collection and Applied Time Series Models**

### **Data Collection and Processing**

### **Target Variable:**

**Average Monthly Electricity Price ($/kWh) – U.S. City Average**: This is the primary time series used in this project for developing time series models.  
> ***Note:*** The original dataset had a missing value for September 1985. To address this, the missing value was imputed using the average of the electricity prices from August and October 1985.

<img width="1165" height="492" alt="image" src="https://github.com/user-attachments/assets/f2c6821b-dd4e-4048-b0e3-e66dfef7c092" />

---

### **List of Potential External Regressors:**

- **Monthly Production Index of electric and gas utilities**
- **Henry Hub Natural Gas Spot Price**  
- **Average Monthly Temperature (in °F)**  
- **Monthly Population Estimates**

> ***Note:*** These external regressors were evaluated to understand their influence on electricity prices and improve prediction accuracy.

<img width="1188" height="805" alt="image" src="https://github.com/user-attachments/assets/17439bba-d342-4310-a8ed-36a04369eb38" />

---

### **Data Sources**

- **Average Monthly Electricity Price**  
  Retrieved from the [U.S.  Federal Reserve Economic Data (FRED)](https://fred.stlouisfed.org/series/APU000072610)

- **Utility Production Index, Natural Gas Price, and Monthly Population:**  
  Collected from [U.S.  Federal Reserve Economic Data (FRED)](https://fred.stlouisfed.org/)
  
- **Average Monthly Temperature:**
  Collected from [National Centers for Environmental Information (NCEI)](https://www.ncei.noaa.gov/access/monitoring/climate-at-a-glance/national/time-series/110/tavg/ytd/0/1975-2025)


---

### **Note about data collection**
- Data on the variables used in this project, including the target and external regressors, are based on **nationwide U.S. data**, not specific to any individual state or region.

---
### **List of Time Series Models Developed in this Project**
The following time series models were applied to model and predict monthly electricity prices:
- **Facebook Prophet model with external regressors**
- **Facebook Prophet model without external regressors**
- **SARIMA model with external regressors**
- **SARIMA model without external regressors**
- **Holt-Winters model (without external regressors)**

---
---

## ** Data Preprocessing & Exploratory Analysis**
### Scatter Plots of Monthly Electricity Price ($/kWh) vs. Potential External Regressors
<img width="1189" height="765" alt="image" src="https://github.com/user-attachments/assets/abf80284-3305-41ae-b5a3-9075d72dcb28" />

---

### Dual-Axis Time Series Plot of Monthly Electricity Price and Natural Gas Price
<img width="1190" height="490" alt="image" src="https://github.com/user-attachments/assets/075ef290-0b0e-4173-aa36-b50b73679bc7" />

### **Capturing Natural Gas Price Spikes Using a Dummy Regressor**
The dual-axis line plot above reveals a clear pattern: sudden increases in natural gas prices frequently coincide with jumps in monthly electricity prices. This relationship is expected, given that natural gas has become the dominant source of electricity generation in the U.S., particularly after 2018.
Neverthless, unlike other external regressors—such as utility production index, temperature, and population, which contains full data coverage from January 1980, the Henry Hub natural gas price data is only available from January 1997 onward. This limited temporal coverage posed a challenge for incorporating gas price effects on monthly electricity price. To address this, a binary indicator variable named **spike** was created to represent gas price surge periods. This dummy variable is assigned a value of 1 for a 4-month period if the average natural gas price in that current 4-month window is higher than the average values of the preceding and following 4-month windows plus half the standard deviation above the overall mean gas price. Otherwise, the dummy variable remains 0. This logic was implemented using a sliding window approach with a step size of 4 months, ensuring detection of localized gas price spikes while preventing overlapping flags. The graph below displays the dual-axis plot of monthly electricity and natural gas prices with spike indicators.

<img width="1189" height="495" alt="image" src="https://github.com/user-attachments/assets/962734ab-79f0-430d-9d74-33e1d8ccaf10" />

<br> <br>
**As illustarted in the dual-axis plot above**, there is a direct relationship between natural gas price spikes and subsequent increases in electricity prices. Notably, during the four-month period from **May 2022 to August 2022**, natural gas prices experienced a sharp surge. Following this spike, a significant rise in electricity prices was observed, indicating a potential lagged effect of natural gas cost changes on electricity pricing. Similar patterns appear during other periods as well, where electricity prices responded to natural gas price volatility. This relationship is consistent with expectations, given that natural gas has recently become the primary source of electricity generation in the United States.


---
### **TRAIN-TEST SPLIT FOR MODEL DEVELOPMENT & EVALUATION**

To develop and evaluate the prediction performance of the alternative models, the dataset was divided into two subsets:

- **Training Sample (95%)**: Includes all data points prior to January 2023, used to train the models.
- **Test Sample (5%)**: Contains data from January 2023 onward, reserved for testing and evaluating the models' prediction accuracy.

<img width="1010" height="492" alt="image" src="https://github.com/user-attachments/assets/af662186-74ad-417b-999e-93569efc0c3d" />

---

## **TIME SERIES MODEL DEVELOPMENT AND COMPARISON**

This section presents the development and evaluation of multiple time series forecasting models to predict monthly electricity prices. The models implemented include:

**1. Facebook Prophet**  
**2. SARIMA (Seasonal Autoregressive Integrated Moving Average)**  
**3. Holt-Winters Triple Exponential Smoothing**

Each model was developed on training data and assessed on test data using common prediction metrics to compare their performance. The goal was to identify the most accurate and robust model for capturing both trend and seasonal patterns in electricity prices.

## **1. Fitting the Facebook Prophet Model**

The **Facebook Prophet** model is a powerful time series forecasting model developed by Facebook’s Core Data Science team. It offers several advantages over traditional forecasting methods, including the ability to:
- Incorporate **holiday effects**
- Model **multiple built-in and customized seasonalities** (e.g., yearly, weekly, or custom)
- Detect and model **changepoints** in time series trends

Like SARIMA model, Prophet also supports **external regressors**, but with a key difference: Prophet applies **ridge regularization (L2 penalty)** to its regressors by default. This helps reduce overfitting and mitigate the impact of multicollinearity among predictors.

---

**Modeling Strategy**

To evaluate the impact of external variables on electricity price prediction, two Prophet models were developed and compared:

1. **Model with external regressors**, including:
   - `Utility Production Index`
   - `Population`
   - `Average Monthly Temperature`
   - `spike` (a dummy variable indicating natural gas price spikes)

2. **Model without external regressors**


Since Prophet’s prediction performance can highly be influenced by changepoint-related hyperparameters, a **custom grid search** was implemented to tune the following:

- `changepoint_prior_scale`  
- `n_changepoints`  
- `changepoint_range`

Each combination of hyperparameters was evaluated using **time series cross-validation** from the Facebook Prophet diagnostics module, with performance assessed based on the **average Root Mean Squared Error (RMSE)**.

---
---

### **1.1. Fitting the Facebook Prophet Model with External Regressors**

#### **Key Implementation Steps**

- Define a parameter grid for changepoint hyperparameter tuning
- Add external regressors to the model
- Fit the model using the training dataset
- Perform cross-validation using prophet.diagnostics.cross_validation()
- Select the best model configuration based on validation RMSE

The following **optimal changepoint-related parameters** were extracted from the algorithm used to identify the best-fitting model. These parameters were used to fit the Facebook Prophet model.
- 'changepoint_prior_scale': 0.2
- 'changepoint_range': 1.0
- 'n_changepoints': 10

#### **Facebook Prophet Model Prediction & Visualization for the Training & Test Sets**
The Facebook Prophet model above was used to predict monthly electricity price over two separate time periods:
- **Training period**: 516 future observations spanning from **January 1980 to December 2022**.
- **Test period**: 29 observations from **January 2023 to March 2025**, used to evaluate the model's predictive accuracy on unseen data.

The predicted values for the aformentioned periods were then visualized alongside the correspodning actual samples to assess the model’s performance, especially for the test period.

**Note:** The fitted model is capable of forecasting monthly electricity prices beyond March 2025, given that future values for the external regressors (e.g., utility production, population, and gas price spikes) are available. However, since these future regressor values are currently unavailable, the prediction was limited to the training and test periods only.

<img width="1165" height="569" alt="image" src="https://github.com/user-attachments/assets/3296deb4-63cb-46e4-87aa-2da1a04cd521" />

---
---

### **1.2. Fitting the Facebook Prophet Model without External Regressors**
A similar iterative algorithm used for the Facebook Prophet model with external regressors was employed to tune changepoint hyperparameters for the model without external regressors. The following steps were taken to identify the best-fitting configuration:
- Define a parameter grid for changepoint hyperparameter tuning
- Fit the model using the training dataset
- Perform cross-validation using prophet.diagnostics.cross_validation()
- Select the best model configuration based on validation RMSE

The following **optimal changepoint-related parameters** were found from the algorithm used. These parameters were used to fit the Facebook Prophet model without external regressors.
- 'changepoint_prior_scale': 0.1
- 'changepoint_range': 0.9
- 'n_changepoints': 50

#### **Facebook Prophet Model (without Regressors) Prediction & Visualization for the Training & Test Sets**
- **Training period**: 516 future observations spanning from **January 1980 to December 2022**.

- **Test period**: 29 observations from **January 2023 to March 2025**, used to evaluate the model's predictive accuracy on unseen data.

**Note:** Since the Facebook Prophet model above did not incorporate external regressors, it is capable of forecasting monthly electricity prices beyond March 2025. However, the prediction was limited to the training and test periods to enable a more consistent and meaningful comparison with the counterpart model that includes external regressors.

<img width="1165" height="569" alt="image" src="https://github.com/user-attachments/assets/9ff61e5e-e9f2-4354-a543-265903285cfd" />

### **Plotting the RMSE and MAE Metrics for the Facebook Prophet Model with and without External Regressors**
<img width="790" height="390" alt="image" src="https://github.com/user-attachments/assets/ba94e9e9-6586-4042-8f42-bd88e6d37ebd" />

#### **Inference from the Barplot of RMSE and MAE**
The bar plot comparison of RMSE and MAE on the test dataset clearly shows that the Facebook Prophet model with external regressors substantially outperformed the model without them. Including monthly utility production index, and population, and gas price spike indicator as external features improved prediction accuracy by approximately 45% in RMSE and 47% in MAE, highlighting the value of incorporating relevant contextual variables.

---
### **Actual vs. Predicted Electricity Prices for the Facebook Prophet Model with and without External Regressors**

This superiority of the Facebook Prophet model with regressors is also visually evident in the line plot below, where the blue curve representing the FB-Prophet model with external regressors follows more closely the actual electricity price (green dashed line) than the orange curve (FB-Prophet without external regressors).

<img width="1952" height="797" alt="image" src="https://github.com/user-attachments/assets/6bad9061-07ba-48e2-884e-78b8f9fabe82" />

---
---

## **2. Fitting the SARIMA Model**

The **Seasonal Autoregressive Integrated Moving Average (SARIMA)** model is an advanced extension of the ARIMA model. It accounts for both non-seasonal and seasonal components of time series data, making it suitable for capturing complex temporal patterns such as trends and periodic fluctuations. SARIMA is widely used in domains such as economics, energy, and meteorology to forecast time-dependent phenomena.

In this project, the **`auto_arima()`** function from the `pmdarima` library was used to automatically identify the optimal combination of model parameters `(p, d, q, P, D, Q)` based on information-based performance criteria, such as **AIC** and **BIC**. The function internally handles differencing and seasonal component selection, streamlining the model selection process.

---

### **2.1. Fitting the SARIMA Model with External Regressors**
#### **Important tips when using external regressors in the SARIMA model**

- **(A) Manual Scaling of Regressors**  
  Unlike the Facebook Prophet model, the SARIMA does not include any built-in mechanism for scaling external regressors. Therefore, scaling must be performed manually. In this project, `StandardScaler()` from the `sklearn.preprocessing` module was used to standardize the regressors before model fitting.

- **(B) Handling Multicollinearity**  
  In contrast to the Facebook Prophet model, the SARIMA model does not include a regularization term to address multicollinearity among external regressors. If multicollinearity is present, one solution is to remove the regressor that has a weaker impact on the target variable.  
  In this project, a strong correlation was found between the **utility production index** and **population**. Between these two inter-correlated variables, **population** was found to have a statistically significant effect on monthly electricity prices (p-value < 0.05). Therefore, it was retained in the model.

- **(C) Variable Selection**  
  A **backward stepwise selection** approach was used to iteratively include only statistically significant external regressors. Selection was guided by **AIC/BIC** values and **Wald statistics**, using a 5% significance threshold.

---

#### **Finding Optimal SARIMA Model Order (p, d, q)(P, D, Q)[12]**
The `auto_arima()` function selected **ARIMA(0,1,0)(0,1,1)[12]**, with **monthly population** as the sole external regressor, as the optimal model based on the AIC criterion.

Similar to the Facebook Prophet model, a total of 29 observations spanning from **January 2023 to March 2025**, was used to evaluate the SARIMA model's predictive accuracy on unseen data. The predicted values were then visualized alongside the actual training and test samples to assess the model’s performance and long-term forecasting behavior.
<img width="1165" height="569" alt="image" src="https://github.com/user-attachments/assets/976d3933-60b3-4680-a1c0-267139c67377" />

---
### **2.2. Fitting the SARIMA Model without External Regressors**
A similar modeling process to that used for the SARIMA model with external regressors was followed here, but without including any external predictors (e.g., population, utility production index). The `auto_arima()` function selected **ARIMA(0,1,0)(0,1,1)[12]** as the optimal model based on the AIC criterion.

<img width="1165" height="569" alt="image" src="https://github.com/user-attachments/assets/b7a49392-f531-4145-ab3f-9b9ad128c062" />

### **Plotting the RMSE and MAE Metrics for the SARIMA Model with and without External Regressors**
<img width="790" height="390" alt="image" src="https://github.com/user-attachments/assets/0e7cecaa-f4ee-4cd9-8332-9a3ed1ef2b10" />
#### **Inference from the Barplot of RMSE and MAE for the SARIMA Models**
The bar plot comparison of RMSE and MAE on the test dataset indicates that the **SARIMA model without external regressors** yielded better performance than the model that included monthly population as the only external predictor. Although this outcome may seem counterintuitive—given that external regressors are generally expected to enhance predictive performance—one possible explanation is that the inclusion of population, despite its statistical significance, may have introduced noise into the model or perhaps may not have captured variations in monthly electricity prices.

---
---
## **3. Fitting the Holt-Winters (Triple Exponential Smoothing) Model**
As previously mentioned, the Holt-Winters model does not support the inclusion of external regressors; therefore, none were incorporated into the model. The Holt-Winters model was fitted using the training sample, where both trend and seasonality were set to *additive*.
<img width="1165" height="492" alt="image" src="https://github.com/user-attachments/assets/8c10216c-1dd8-4a67-85c0-c6405c9ca0d3" />

---
---

## **COMPARISON OF RMSE AND MAE ACROSS TIME SERIES MODELS ON TEST DATA**
The bar plot below of RMSE and MAE values on the test dataset for the time series models indicates that the **Facebook Prophet model with external regressors** achieved the best predictive performance among the candidate models, followed by the SARIMA model without external regressors.

<img width="1089" height="490" alt="image" src="https://github.com/user-attachments/assets/458edf70-a16c-4b9f-8802-8b9e15a5ff69" />


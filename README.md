# **Modeling-U.S.-Urban-Electricity-Prices-Using-Time-Series-Techniques**

Time series forecasting of U.S. urban electricity prices using SARIMA, Holt-Winters, and Facebook Prophet Models (with &amp; without external regressors)

<br>

## **PROJECT SUMMARY**
As of May 2025, the average residential electricity rate in the United States was 0.182 dollar (18.2 cents) per kilowatt-hour (kWh). This cost can vary significantly depending on the geographic region, utility provider, and pricing plan. For example, Hawaii is among the states with the highest electricity rates, while North Dakota has some of the lowest. 

<img width="2091" height="770" alt="image" src="https://github.com/user-attachments/assets/e8373d6c-b494-4b38-80c5-20f5eacee9f3" />

<br> <br>

The primary objective of this project was to model and predict **average monthly electricity prices** ($/kWh) in the United States. To accomplish this, three time series forecasting techniques were applied: **Facebook Prophet**, **SARIMA**, and **Holt-Winters (Triple Exponential Smoothing)**. The dataset used in this project were collected from various sources, spanning from **January 1980 to March 2025**. Models were trained on data from **January 1980 to December 2022** and evaluated on a test set from **January 2023 to March 2025**.

To enhance prediction accuracy, several **external regressors** were incorporated into the Facebook Prophet and SARIMA models. Among the candidate models, the **Facebook Prophet model with external regressors** significantly outperformed SARIMA and Holt-Winters in terms of **RMSE** and **MAE**, indicating superior predictive accuracy. The inclusion of variables such as the **monthly production index of utilities**, **monthly population**, and a **gas price spike indicator** helped the model better capture volatility and seasonal behavior in electricity prices. In contrast, the Prophet model without external regressors and Holt-Winters yielded substantially poorer predictive performance.

The findings of this project highlight that both **historical patterns** (e.g., trend and seasonality) and **key external factors** play an important role in predicitng time-varying electricity prices. Practically speaking, the results provide valuable insights into long-term electricity price trends and can help decision makers in prioritizing **infrastructure investment** and **operational planning** efforts in the energy sector.

---

### **Additional Details on Data Collection and Applied Time Series Models**

#### **Data Collection and Processing**

##### **Target Variable:**

**Average Monthly Electricity Price ($/kWh) – U.S. City Average**: This is the primary time series used in this project for developing time series models.  


##### **List of Potential External Regressors:**

- **Monthly Production Index of electric and gas utilities**
- **Henry Hub Natural Gas Spot Price**  
- **Average Monthly Temperature (in °F)**  
- **Monthly Population Estimates**


> ***Note:*** These external regressors were evaluated to understand their influence on electricity prices and improve prediction accuracy.

---

##### **Data Sources**

- **Average Monthly Electricity Price**  
  Retrieved from the [U.S.  Federal Reserve Economic Data (FRED)](https://fred.stlouisfed.org/series/APU000072610)

- **Utility Production Index, Natural Gas Price, and Monthly Population:**  
  Collected from [U.S.  Federal Reserve Economic Data (FRED)](https://fred.stlouisfed.org/)
  
- **Average Monthly Temperature:**
  Collected from [National Centers for Environmental Information (NCEI)](https://www.ncei.noaa.gov/access/monitoring/climate-at-a-glance/national/time-series/110/tavg/ytd/0/1975-2025)


---

##### **Note about data collection**
- Data on the variables used in this project, including the target and external regressors, are based on **nationwide U.S. data**, not specific to any individual state or region.

---
---
#### **List of Time Series Models Developed in this Project**
The following time series models were applied to model and predict monthly electricity prices:
- **Facebook Prophet model with external regressors**
- **Facebook Prophet model without external regressors**
- **SARIMA model with external regressors**
- **SARIMA model without external regressors**
- **Holt-Winters model (without external regressors)**

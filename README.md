# Statistical Modelling Assignment: California Housing Data

**Course:** Statistical Modelling (Year 3)  
**Weight:** 20 Marks  
**Due Date:** 17th October 2025  

---

## Objective
Understand **regularization** and **dimension-reduction** techniques in regression:
- **Ridge Regression**
- **Lasso Regression**
- **Partial Least Squares (PLS) Regression**

---

## 1. Data Description
- **Dataset:** California Housing Dataset  
- **Source:** [Public dataset](https://www.dcc.fc.up.pt/~ltorgo/Regression/cal_housing.html)  
- **Sample size:** 20,433 observations  
- **Predictors:** 13 variables (longitude, latitude, total rooms, households, median income, ocean proximity categories)  
- **Response variable:** `median_house_value` (continuous)  
- **Reason for use:** Dataset contains continuous and categorical predictors suitable for regression and demonstrates multicollinearity.

---
### Correlation
<img width="653" height="403" alt="image" src="https://github.com/user-attachments/assets/a4624da8-35d0-4754-9d43-3b024cfc3e69" />

###### Strongest Relationships (Important for Modeling)

| Variables                                         | Correlation | Meaning                                                                                                           |
| ------------------------------------------------- | ----------- | ----------------------------------------------------------------------------------------------------------------- |
| **median_income ↔ median_house_value**            | **+0.688**  | 💰 Strong positive link — as income rises, house prices rise. This will be your **most important predictor**.     |
| **total_rooms ↔ total_bedrooms**                  | **+0.93**   | 🏠 Very strong correlation — more rooms mean more bedrooms (redundant variable, may cause **multicollinearity**). |
| **population ↔ households**                       | **+0.91**   | 👨‍👩‍👧 Strong link — higher population → more households (also redundant).                                      |
| **ocean_proximityINLAND ↔ median_house_value**    | **–0.485**  | 🏜️ Negative — inland houses are cheaper than coastal ones.                                                       |
| **ocean_proximity<1H OCEAN ↔ median_house_value** | **+0.258**  | 🌊 Positive — homes near the ocean (<1 hour) are more expensive.                                                  |

##### Moderate or Weak Relationships


| Variables                                   | Correlation | Interpretation                                                           |
| ------------------------------------------- | ----------- | ------------------------------------------------------------------------ |
| **housing_median_age ↔ median_house_value** | +0.106      | Older neighborhoods are *slightly* more expensive.                       |
| **longitude ↔ latitude**                    | –0.925      | Strong negative — these two describe location (redundant spatially).     |
| **total_rooms ↔ median_house_value**        | +0.133      | Slightly higher house value with more rooms, but not a strong predictor. |


3️⃣ Collinearity Warnings (Variables too similar)

To prevent overfitting during regularization or regression:

total_rooms, total_bedrooms, households, and population are highly correlated.
👉 Keep only one or two (e.g., total_rooms and population) or standardize before modeling.

longitude and latitude are location proxies — keep both, but be aware they are not independent.

## 2. Model Fitting

### 2.1 Linear Regression
- **Formula:**  
  `median_house_value ~ longitude + latitude + housing_median_age + total_rooms + total_bedrooms + population + households + median_income + ocean_proximity variables`
- **Test Performance:**  
  - RMSE: 67,873.12  
  - R-squared: 0.655431  

---

### 2.2 Ridge Regression (L2 Regularization)
- **Best λ (via CV):** 7,889.342  
- **Test Performance:**  
  - RMSE: 69,274.66  
  - R-squared: 0.6399324  
- **Interpretation:** Shrinks coefficients to reduce multicollinearity while keeping all predictors.

---

### 2.3 Lasso Regression (L1 Regularization)
- **Best λ (via CV):** 55.77027  
- **Test Performance:**  
  - RMSE: 67,651.67  
  - R-squared: 0.6566063  
- **Interpretation:** Performs feature selection by setting some coefficients exactly to zero, simplifying the model.

---

### 2.4 Partial Least Squares (PLS) Regression
- **Optimal Components:** 10  
- **Test Performance:**  
  - RMSE: 67,902.41  
  - R-squared: 0.6555516  
- **Interpretation:** Reduces dimensionality and handles multicollinearity while preserving predictive power.

---

## 3. Comparative Results

| Model  | RMSE       | R-squared |
|--------|------------|-----------|
| Linear | 67,873.12  | 0.655431  |
| Ridge  | 69,274.66  | 0.6399324 |
| Lasso  | 67,651.67  | 0.6566063 |
| PLS    | 67,902.41  | 0.6555516 |

**Key Insights:**
- **Lasso** performs best in RMSE and R².  
- **Ridge** reduces multicollinearity without dropping variables.  
- **PLS** reduces dimensions, balancing complexity and prediction.  
- **Linear regression** performs well but may suffer from multicollinearity.

---



## 4. Visualizations
- **Coefficient Paths:** Show Ridge/Lasso coefficient shrinkage as λ increases.
  <img width="636" height="393" alt="image" src="https://github.com/user-attachments/assets/ca757c0f-cfe1-45bb-8224-1f5a3bbba13f" />
 
- **Cross-Validation Curves:** RMSE vs λ (Ridge/Lasso) and vs number of components (PLS).
-  <img width="636" height="393" alt="image" src="https://github.com/user-attachments/assets/c6e6944d-453b-48ab-8223-7a17e5fe38f5" />

- **Best lambda for lasso =67.03995**
<img width="636" height="393" alt="image" src="https://github.com/user-attachments/assets/a9853795-1ca9-48d8-acc4-031e11506c20" />

<img width="636" height="393" alt="image" src="https://github.com/user-attachments/assets/4f23833a-17f7-4d0b-b98d-c3122f61e9fd" />
- **Best lambda for Ridge= 7889.342**

- **Fitted Line / Scatter:** Predicted vs actual house values.
<img width="636" height="393" alt="image" src="https://github.com/user-attachments/assets/8c8c069d-6e84-4c5e-9f3b-5d5e2dd7123e" />
<img width="636" height="393" alt="image" src="https://github.com/user-attachments/assets/64bf6e65-2af1-4524-a050-c84b66435e96" />

- **Diagnostic Plots (Lasso):** Residuals vs fitted, Q-Q plot.
 <img width="636" height="393" alt="image" src="https://github.com/user-attachments/assets/6b9363b9-a0c4-469a-8e9c-04de9918eeb9" />


---
## Table 4: Comparative Coefficient Analysis — California Housing Dataset (Unscaled)

| Predictor Variable             | OLS Coefficient | Ridge Coefficient (λ = 7,889.342) | Lasso Coefficient (λ = 55.77027) |
|--------------------------------|----------------:|----------------------------------:|---------------------------------:|
| Intercept                      | -2,255,000      | -774,929                          | -2,159,600                       |
| longitude                      | -26,720         | -9,294                            | -25,624                          |
| latitude                       | -25,490         | -8,527                            | -24,590                          |
| housing_median_age             | 1,074           | 995                               | 1,061                            |
| total_rooms                    | -6.61           | 0.72                              | -6.02                            |
| total_bedrooms                 | 108.8           | 41.80                             | 103.8                            |
| population                     | -35.97          | -23.53                            | -33.33                           |
| households                     | 37.85           | 35.66                             | 32.99                            |
| median_income                  | 39,610          | 35,555                            | 39,330                           |
| ocean_proximity <1H OCEAN      | -4,668          | 18,331                            | 0                                |
| ocean_proximity INLAND         | -44,430         | -45,075                           | -41,324                          |
| ocean_proximity ISLAND         | 147,700         | 160,311                           | 133,277                          |
| ocean_proximity NEAR BAY       | -7,389          | 22,084                            | -1,181                           |
| ocean_proximity NEAR OCEAN     | NA              | 27,409                            | 4,408                            |

### Insights
- **Ridge Regression** shrinks large coefficients to reduce overfitting.  
- **Lasso Regression** sets some coefficients to zero, performing feature selection.  
- **Lasso** retains strong predictors like `median_income` and `longitude`, offering both accuracy and interpretability.


## 5. Interpretation & Discussion
- **Feature Selection:** Lasso removes irrelevant predictors.  
- **Handling Multicollinearity:** Ridge shrinks correlated coefficients; PLS combines them into components.  
- **Predictive Performance:** Lasso achieves lowest RMSE.  
- **Practical Implications:** Use Lasso for variable selection; Ridge/PLS for multicollinearity handling or dimension reduction.

---

## 6. References
1. Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning*. Springer.  
2. James, G., Witten, D., Hastie, T., & Tibshirani, R. (2013). *An Introduction to Statistical Learning*. Springer.  
3. California Housing Dataset. Retrieved from [https://www.dcc.fc.up.pt/~ltorgo/Regression/cal_housing.html](https://www.dcc.fc.up.pt/~ltorgo/Regression/cal_housing.html)  

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
- **Cross-Validation Curves:** RMSE vs λ (Ridge/Lasso) and vs number of components (PLS).  
- **Fitted Line / Scatter:** Predicted vs actual house values.  
- **Diagnostic Plots (Lasso):** Residuals vs fitted, Q-Q plot.

---

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

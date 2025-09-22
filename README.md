# Regression Regularization Project

## 📌 Objective
The purpose of this project is to explore **regularization** and **dimension-reduction** techniques in regression analysis.  
Specifically, it compares **Ridge Regression**, **Lasso Regression**, and **Partial Least Squares (PLS)** regression in terms of their ability to handle multicollinearity, perform feature selection, and improve predictive performance.

---

## 📚 Contents
- `data/` – dataset (or link to source) and dataset description  
- `R/` – R scripts for data preprocessing, model fitting, and helper functions  
- `report/` – final RMarkdown report (max 10 pages)  
- `docs/` – generated figures and tables  
- `outputs/` – model outputs and saved results  

---

## 📊 Dataset
- **Source:** [Insert dataset link or package name here]  
- **Response Variable (Y):** Continuous outcome variable  
- **Predictors (X):** ≥10 predictors (continuous and/or categorical)  
- **Sample Size:** [Insert sample size here]  
- **Reason for Selection:** The dataset includes multiple predictors and potential multicollinearity, making it suitable for demonstrating Ridge, Lasso, and PLS regression.

---

## ⚙️ Methods
1. **Ridge Regression** – adds L2 penalty to shrink coefficients and handle multicollinearity.  
2. **Lasso Regression** – adds L1 penalty, shrinking some coefficients to zero (feature selection).  
3. **Partial Least Squares (PLS)** – projects predictors into latent components while considering the response.  

---

## 📈 Deliverables
- **Report:** Includes introduction, methodology, results, discussion, and references (≤10 pages).  
- **Code:** All R scripts (`.R`) or RMarkdown (`.Rmd`) files.  
- **Dataset:** Either uploaded or linked if publicly available.  

---

## ▶️ How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/aykahsay/regression-regularization-project.git
   cd regression-regularization-project

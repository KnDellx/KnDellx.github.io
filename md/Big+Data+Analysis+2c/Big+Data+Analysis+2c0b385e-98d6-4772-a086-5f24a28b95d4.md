<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD007 -->
# Telecom Customer Churn Survival Analysis Report

## 1. Research Background and Objectives

Customer churn in the telecommunications industry is a key factor affecting company profits. This study employs survival analysis methods to explore the impact of different variables on customer churn behavior, aiming to help telecom companies develop more effective customer retention strategies.

## 2. Data Preparation

### 2.1 Data Source

Using the [Telco-Customer-Churn.csv](vscode-file://vscode-app/d:/program/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) dataset, which contains various customer attributes and service usage information.

### 2.2 Data Processing

- **Data Transformation**: Converting the "churnString" column (Yes/No) to numeric values (1/0)

- **Data Filtering**:

    - Selecting customers with month-to-month contracts

    - Selecting customers using internet services

- **Data Layering**: Creating Bronze tables (raw data) and Silver tables (cleaned data)

<div style="flex: 1; margin: 10px; text-align: center">
    <img src="..\md\Big+Data+Analysis+2c\Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4\1742644798474.png" alt="Silver Table" /style="max-width: 100%; height: auto;">
    <p>Bronze Table</p>
</div>
<div style="flex: 1; margin: 10px; text-align: center">
    <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/1742644856598.png" alt="Silver Table" /style="max-width: 100%; height: auto;">
    <p>Silver Table</p>
</div>
## 3. Implementation of Survival Analysis

### 3.1 Kaplan-Meier Survival Analysis

The Kaplan-Meier method was used to estimate customer retention probability, with customer tenure as the time variable and churn as the event variable.

#### 3.1.1 Overall Survival Curve

Analyzed the overall retention situation of all customers, calculating the median survival time (average tenure before customer churn).

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;text-align: center">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image.png" alt="Overall Survival Curve"/style="max-width: 100%; height: auto;">
    </div>
</div>

**Median Survival Time**: 34 

#### 3.1.2 Group Survival Curve Analysis

Group survival curves were compared for the following variables:

- Gender

- Senior Citizen status

- Partner status

- Dependents status

- Phone Service

- Multiple Lines

- Internet Service type

- Online Security

- Online Backup

- Device Protection

- Tech Support

- Streaming TV

- Streaming Movies

- Paperless Billing

- Payment Method

#### 3.1.3 Log-rank Test

Log-rank tests were used to assess the statistical significance of differences between survival curves of different groups. For example, the code `print_logrank('streamingMovies')` tests the impact of different streaming movie service statuses on customer retention rates.

<div style="flex: 1; margin: 10px; text-align: center">
    <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/1742645425200.png" alt="Log-rank Test"/style="max-width: 100%; height: auto;">
</div>
<div style="flex: 1; margin: 10px; text-align: center">
    <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/1742645425204.jpg" alt="Log-rank Test"/style="max-width: 100%; height: auto;">
</div>

### 3.2 Cox Proportional Hazards Regression Model

The Cox proportional hazards model was used to analyze the simultaneous impact of multiple factors on customer churn risk.

#### 3.2.1 Variable Selection and Encoding

- Selected variables including dependents status, internet service type, online backup, tech support, paperless billing, etc.

- One-hot encoding was applied to categorical variables

<div style="flex: 1; margin: 10px;">
    <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/1742645600231.png" alt="Variable Selection"/style="max-width: 100%; height: auto;">
</div>
<div style="flex: 1; margin: 10px;">
    <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/1742646502580.png" alt="Variable Selection"/style="max-width: 100%; height: auto;">
</div>

#### 3.2.2 Model Assumption Verification

Verified whether the model meets the proportional hazards assumption:

- Statistical tests

- Schoenfeld residuals analysis

- Log-log Kaplan-Meier curve comparison

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/1742646539757.png" alt="Statistical Tests"/style="max-width: 100%; height: auto;">
        <p>Statistical Tests</p>
    </div>
</div>

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 1.png" alt="Schoenfeld Residuals"/style="max-width: 100%; height: auto;">
    </div>
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 2.png" alt="Schoenfeld Residuals"/style="max-width: 100%; height: auto;">
    </div>
</div>

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 3.png" alt="Log-log Kaplan-Meier Curve"/style="max-width: 100%; height: auto;">
    </div>
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 4.png" alt="Log-log Kaplan-Meier Curve"/style="max-width: 100%; height: auto;">
    </div>
</div>

Based on the results of the statistical test and the Schoenfeld residual plots, it's clear that our model violates the proportional hazards assumption many times over.

To get another view of what the issue at play is here, we can use log-log Kaplan-Meier plots. As the name implies, this technique plots Kaplan-Meier curves on a log-log scale.

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 5.png" alt="Log-log Kaplan-Meier Plot"/style="max-width: 100%; height: auto;">
    </div>
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 6.png" alt="Log-log Kaplan-Meier Plot"/style="max-width: 100%; height: auto;">
    </div>
</div>

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 7.png" alt="Log-log Kaplan-Meier Plot"/style="max-width: 100%; height: auto;">
    </div>
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 8.png" alt="Log-log Kaplan-Meier Plot"/style="max-width: 100%; height: auto;">
    </div>
</div>

## 4. Accelerated Failure Time Model (AFT)

### 4.1 **Understanding the AFT Model**

- The **Accelerated Failure Time model** is a **parametric** approach in survival analysis, unlike **Kaplan-Meier** (non-parametric) or **Cox Proportional Hazards** (semi-parametric).

- It assumes the outcome variable follows a specified distribution (e.g., **Log-Logistic, Weibull, or Log-Normal**).

- The **acceleration factor (λ)** determines how time-to-event (e.g., churn) changes between groups. For example, if dogs age 7× faster than humans, the acceleration factor for dogs is **7** relative to humans.

---

## 4.2 **Fitting the AFT Model to Telco Customer Churn Data**

### **Data Preparation**

- The dataset includes customer tenure, churn status, and categorical variables such as **internet service type, payment method, and security features**.

- **One-hot encoding** is used for categorical variables to avoid multicollinearity issues.

### **Model Fitting**

- A **Log-Logistic AFT model** is fitted to the data, specifying:

    - **Tenure** (time until churn or right-censored observation).

    - **Churn** (event indicator: churned or still active).

- The model outputs a **median survival time of 135.51 months**.

---

## 4.3 **Interpreting the Results**

### 4.3.**1. Statistical Significance**

- All covariates have a **p-value < 0.005**, meaning they are statistically significant.

- Insignificant variables (if any) could be dropped or recategorized.

### 4.3.**2. Effect of Covariates**

- The **coefficient (coef)** and its exponentiated form **exp(coef)** indicate how each factor accelerates or decelerates churn risk.

- Example: If **exp(coef) = 1.47** for **internet service (DSL vs. Fiber Optic)**, customers with DSL churn **47% faster** than those with Fiber Optic.

### 4.3.**3. Model Performance Metrics**

- **Concordance Index (C-Index)** measures predictive accuracy.

- **AIC (Akaike Information Criterion)** and **log-likelihood ratio** help compare model fit.

---

<div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/1742745348996.png" alt="Model Performance Metrics"/style="max-width: 100%; height: auto;">
</div>
<div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 9.png" alt="Model Performance Metrics"/style="max-width: 100%; height: auto;">
</div>

## 4.4 **Assessing Model Assumptions**

### **Proportional Odds & Distribution Assumption**

- **Log-log plots** check assumptions:

    - **Parallel lines** → Satisfies proportional odds.

    - **Straight lines** → Confirms log-logistic distribution is appropriate.

- Results:

    - Lines are **mostly straight** → Log-logistic distribution is a reasonable choice.

    - Lines are **not parallel** → Violates the proportional odds assumption, meaning AFT may not be the best fit.

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 10.png" alt="Proportional Odds"/style="max-width: 100%; height: auto;">
        <p>Partner</p>
    </div>
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 11.png" alt="Proportional Odds"/style="max-width: 100%; height: auto;">
        <p>MultipleLine</p>
    </div>
</div>

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 12.png" alt="Proportional Odds"/style="max-width: 100%; height: auto;">
        <p>internetService</p>
    </div>
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 13.png" alt="Proportional Odds"/style="max-width: 100%; height: auto;">
        <p>onlineSecurity</p>
    </div>
</div>

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 14.png" alt="Proportional Odds"/style="max-width: 100%; height: auto;">
        <p>onlineBackup</p>
    </div>
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 15.png" alt="Proportional Odds"/style="max-width: 100%; height: auto;">
        <p>deviceProtection</p>
    </div>
</div>

<div style="display: flex; flex-wrap: wrap;">
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 16.png" alt="Proportional Odds"/style="max-width: 100%; height: auto;">
        <p>techsupport</p>
    </div>
    <div style="flex: 1; margin: 10px;">
        <img src="../md/Big+Data+Analysis+2c/Big+Data+Analysis+2c0b385e-98d6-4772-a086-5f24a28b95d4/image 17.png" alt="Proportional Odds"/style="max-width: 100%; height: auto;">
        <p>paymentMethod</p>
    </div>
</div>
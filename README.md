# Banking Risk Analytics and Data Analysis

## Problem Statement
Banks face significant financial risk while issuing loans due to uncertainty in customers repayment behavior. Identifying high-risk applicants is essential to minimize potential defaults and ensure sustainable lending practices. Traditional loan evaluation methods often rely on limited manual assessment and may not fully leverage available customer financial data. This project focuses on applying data analytics to evaluate customer profiles, classify financial risk, and support data-driven loan approval decisions. The goal is to improve risk management and reduce potential financial losses in lending operations.

## Objective
The main objective of this project is to develop a banking risk analytics solution that helps financial institutions make better lending decisions by identifying risky customers and understanding their financial behavior.

The project aims to:
- Analyze customer financial data including income, loans, deposits, and credit usage
- Identify high-risk customers using a risk scoring model
- Classify customers into Low Risk, Medium Risk, and High Risk categories
- Recommend loan approval decisions based on customer risk profiles
- Build interactive dashboards for business decision-making and performance monitoring

## Tools and Technologies Used
- Python
- MySQL
- Power BI
- Canva
## Python Libraries
- Pandas
- NumPy
- Matplotlib
- Seaborn
- PyMySQL

## Dataset Overview

The dataset contains customer-level banking and financial information stored across multiple related tables. These tables are connected using primary keys and foreign keys.

### Main Tables Used
- Clients and Banking Details
- Banking Relationship
- Gender
- Investment Advisor
- Time Period
- Key Columns
- Estimated Income
- Bank Loans
- Business Lending
- Credit Card Balance
- Bank Deposits
- Checking Accounts
- Saving Accounts
- Foreign Currency Account
- Risk Weighting
- Occupation
- Nationality
- Loyalty Classification

This structured dataset helps analyze customer financial behavior and lending risk.

### Step 1: Data Extraction from MySQL

The project started with extracting data from a MySQL database into Jupyter Notebook using Python.

#### Process Performed
- Connected MySQL database using PyMySQL
- Executed SQL queries to fetch customer data
- Loaded the data into a Pandas DataFrame for analysis

### Step 2: Data Cleaning and Feature Engineering

Data preprocessing was performed to improve data quality and prepare the dataset for analysis.

#### Cleaning Activities
- Verified missing values
- Checked data types
- Standardized data for analysis
#### Feature Engineering
A new column called Income Band was created by converting Estimated Income into customer segments.
##### Income Band Logic
- Low: Income less than 100000
- Mid: Income between 100000 and 300000
- High: Income greater than 300000

### Step 3: Exploratory Data Analysis (EDA)

EDA was performed to understand customer behavior, identify patterns, and discover relationships between financial variables.

#### Univariate Analysis

Used to understand the distribution of individual variables.

**Performed Analysis**
- Count plots for categorical variables
- Histograms for numerical variables
- Income Band distribution analysis
**Example**
- Distribution of customers by income group
- Distribution of customers by gender, occupation, and loyalty classification
  
#### Bivariate Analysis

Used to compare relationships between two variables.

**Performed Analysis**
- Category comparisons using Gender
- Category comparisons using Nationality
- Loan and deposit behavior across customer groups
**Example**
- Occupation vs Nationality
- Income Band vs Loan Amount

#### Correlation Analysis

A correlation heatmap was created to identify relationships between numerical features.

**Numerical Columns Used**
- Estimated Income
- Bank Loans
- Bank Deposits
- Credit Card Balance
- Business Lending
- Savings Account
- Checking Accounts

**Key Findings**
- Bank Loans are positively related to Credit Card Balance
- Income influences loan and deposit behavior
- Certain customer segments show higher financial risk

### Step 4: Risk Scoring Model

A risk scoring model was created in Power BI using DAX to identify risky customers.

**Risk Score Formula**

The score was calculated using:
- Loan-to-Income Ratio
- Credit Utilization
- Risk Weighting
**DAX Logic**
Risk Score = 
VAR LoanToIncome = DIVIDE([Bank Loan], 'Clients - Banking'[Estimated Income], 0)
VAR CreditUtilization = DIVIDE([Credit Cards Balance], 'Clients - Banking'[Estimated Income], 0)

RETURN 
LoanToIncome * 0.6 + CreditUtilization * 0.3 + ('Clients - Banking'[Risk Weighting] * 0.1)

### Step 5: Risk Classification

Based on the Risk Score, customers were classified into three categories.

**Risk Levels**
- Low Risk
- Medium Risk
- High Risk
**DAX Logic**
Risk Level = 
SWITCH(
    TRUE(),
    [Risk Score] > 8, "High Risk",
    [Risk Score] > 4, "Medium Risk",
    "Low Risk")

### Step 6: Loan Approval Recommendation System

A decision model was created to support loan approvals.

**Decision Logic**
- Low Risk → Approve
- Medium Risk → Review
- High Risk → Reject
**DAX Logic**
Loan Decision = 
SWITCH(
    TRUE(),
    [Risk Level] = "High Risk", "Reject",
    [Risk Level] = "Medium Risk", "Review",
    "Approve")

### Step 7: Power BI Dashboard Development

Interactive dashboards were built using Power BI to provide clear business insights and decision support.

#### Dashboard 1: Home Dashboard
**Included KPIs**
- Total Clients
- Total Loan
- Total Deposit
- Bank Deposits
- Savings Account
- Business Lending

This dashboard provides an overall business summary.
<img width="1286" height="709" alt="Screenshot 2026-05-04 200022" src="https://github.com/user-attachments/assets/c2bf4a4d-21c7-4427-aa25-94bc506df341" />

#### Dashboard 2: Loan Analysis Dashboard
**Included Analysis**
- Total Loan
- Bank Loan
- Business Lending
- Credit Card Balance
- Loan by Income Band
- Loan by Occupation
- Loan by Nationality
- Loan by Banking Relationship

This helps understand loan distribution and exposure.
<img width="1277" height="707" alt="Screenshot 2026-05-04 200054" src="https://github.com/user-attachments/assets/1b19cdb9-29b6-4b63-a3de-8f638e744ffb" />

#### Dashboard 3: Deposit Analysis Dashboard
**Included Analysis**
- Total Deposit
- Bank Deposit
- Savings Accounts
- Checking Accounts
- Foreign Currency Accounts
- Deposit by Income Band
- Deposit by Occupation
- Deposit by Nationality

This helps analyze customer deposit behavior.
<img width="1291" height="701" alt="Screenshot 2026-05-04 200120" src="https://github.com/user-attachments/assets/cf6653ef-8b45-4ef9-811d-a570843be741" />

#### Dashboard 4: Risk and Recommendation Dashboard
This is the most important dashboard in the project.
**Included KPIs**
- High Risk Clients
- Percentage of High Risk Clients
- Total Loan Exposure for High Risk Customers
- Approval Rate
- Rejection Rate
- Loan by Risk Level
- Risk Distribution
- Loan Decision Breakdown
- Risk by Income Band
- Average Risk Score by Occupation

This dashboard transforms the project from descriptive analytics into decision-driven analytics.
<img width="1318" height="719" alt="Screenshot 2026-05-04 200154" src="https://github.com/user-attachments/assets/402853fc-319d-4242-8bbf-48073d3cc64c" />

### Key Insights
- High loan exposure is concentrated among specific customer groups
- Customers with lower income and higher loans tend to be high risk
- Credit card utilization strongly influences customer risk
- Private banking customers contribute significantly to loan and deposit volume
- Risk levels vary across occupations, income bands, and demographic segmen

### Business Recommendations
- Limit loan approvals for high-risk customers to reduce default risk
- Prioritize low-risk customers for premium financial products
- Monitor customers with high credit card utilization closely
- Strengthen lending policies for low-income customers with high borrowing patterns
- Use customer segmentation insights to improve banking strategies

### Conclusion

This project demonstrates how data analytics can improve banking risk management and lending decisions. By combining MySQL, Python, and Power BI, an end-to-end analytics solution was developed to identify risky customers, classify financial behavior, and recommend loan approvals.

The project moves beyond simple dashboard reporting by integrating risk scoring and business recommendations, making it a practical decision-support system for banking operations.

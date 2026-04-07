# financial-customer-analysis-sql

This project explores **customer behavior** and **business insights** using SQL. It answers key business questions around **customer value, engagement, inactivity, and segmentation** using data from users, plans, and transactions tables.

---

## Dataset Overview

The project uses four main tables:

- **`users_customuser`** → Customer information  
- **`plans_plan`** → Savings and investment plans  
- **`savings_savingsaccount`** → Transaction records
- **`savings_savingsaccount`** → Withdrawal records 

** Key Relationships **  
- `owner_id` → Foreign key to `users_customuser.id`  
- `plan_id` → Foreign key to `plans_plan.id`  

**Notes**  
- Savings plans → `is_regular_savings = 1`  
- Investment plans → `is_a_fund = 1`  
- `confirmed_amount` → Deposit/inflow  
- `amount_withdrawn` → Withdrawal  
- Monetary values are stored in **Kobo** (converted to Naira where needed)  

---

## Project Questions & Approaches

### 1️. High-Value Customers with Multiple Products
**Objective:**  
Identify customers who have **both savings and investment plans**, sorted by **total deposits**.

**Approach:**  
- Count savings and investment plans per customer.  
- Calculate **total deposits** per customer.  
- Join these results with the users table.  
- Filter for customers with **at least one savings and one investment plan**.

---

### 2️. Transaction Frequency Analysis
** Objective:**  
Segment customers based on how frequently they transact **per month**.

**Approach:**  
- Calculate **monthly transactions** per customer.  
- Compute **average monthly transactions**.  
- Categorize customers into:  
  - **High Frequency:** ≥10 transactions/month  
  - **Medium Frequency:** 3–9 transactions/month  
  - **Low Frequency:** ≤2 transactions/month  
- Aggregate results by frequency category.

---

### 3️. Account Inactivity Alert
**Objective:**  
Flag accounts with **no transactions in the last 365 days**.

**Approach:**  
- Define **account types** (savings vs. investment).  
- Determine a **reference date** (latest transaction date).  
- Use **LEFT JOIN** to include even accounts with **no transactions**.  
- Calculate inactivity days:  
  - If transactions exist → difference between last transaction and reference date  
  - If no transactions → difference between start date and reference date  
- Filter accounts **inactive for over 1 year**.

---

### 4️. Customer Lifetime Value (CLV) Estimation
**Objective:**  
Estimate **customer value** based on transaction volume and account tenure.

**Approach:**  
- Join users with transaction data from savings table.  
- Calculate:  
  - **Tenure:** months since signup  
  - **Total transaction value**  
- Apply CLV formula: CLV = (Total Transactions / Tenure) × 12 × 0.001
- Use `NULLIF` to avoid division by zero.

---

##  Key SQL Concepts Used

- **Joins:** INNER JOIN, LEFT JOIN, CROSS JOIN  
- **Aggregations:** SUM, COUNT, AVG, MAX  
- **Conditional Logic:** CASE WHEN  
- **CTEs:** For structuring complex queries  
- **Subqueries:** For modular data preparation  
- **Date Functions:** DATEDIFF, TIMESTAMPDIFF

---

## Final Takeaways

- Broke down complex business problems into **step-by-step SQL logic**.  
- Combined **CTEs** for readability and **subqueries** for modular joins.  

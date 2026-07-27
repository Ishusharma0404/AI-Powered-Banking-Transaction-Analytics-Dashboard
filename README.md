# AI-Powered Banking Transaction Analytics (SQL + Power BI)

## Problem Statement

This project helps a banking business analyze **customer accounts and transaction activity** from a single Power BI dashboard. The solution combines customer, account, and transaction data prepared in **SQL Server**, cleans inconsistent date formats, and uses **Power BI, DAX, and AI-assisted KPI/chart recommendations** to turn the data into useful banking insights.

The dashboard focuses on transaction type, monthly transaction value and balance trends, customer/account balances, inactive accounts, customer demographics, and account-type distribution. The source database intentionally contains data-quality issues such as mixed date formats, inconsistent text casing, missing values, unmatched account/customer IDs, negative values, and transaction outliers, making data preparation an important part of the project.

## Steps followed

- **Step 1:** Created the `Power_BI2` database in SQL Server and created three source tables: `Customers`, `Accounts`, and `Transactions`.
- **Step 2:** Added sample customer and account records containing realistic data-quality issues such as missing values, inconsistent capitalization, mixed date formats, unmatched customer IDs, zero balances, and negative balances.
- **Step 3:** Generated **10,000 synthetic banking transactions** in SQL with Credit/Debit activity, mixed transaction-date formats, positive/negative amounts, outliers, missing descriptions, inconsistent currency casing, and unmatched Account IDs.
- **Step 4:** Cleaned and standardized `OpenDate`, `DateOfBirth`, and `TransactionDate` using SQL `TRY_CONVERT`, `CASE`, and `FORMAT`.
- **Step 5:** Combined Transactions, Accounts, and Customers using **LEFT JOINs** and created `CombinedBankingDataset` for analysis.
- **Step 6:** Loaded the combined banking dataset into **Power BI Desktop**.
- **Step 7:** Used **Perplexity/AI assistance** for KPI, chart, and DAX recommendations while developing the analytical dashboard.
- **Step 8:** Created transaction analysis including **Count of Transaction by Transaction Type** and **Monthly Transaction Amount by Month**.
- **Step 9:** Created customer/account analysis including **Total Balance by Name**, **Total Amount by Name**, and **Total Balance by AccountType**.
- **Step 10:** Created **Inactive Accounts by Year and Month** to monitor account inactivity over time.
- **Step 11:** Created demographic analysis using **Customer Count by Gender** and **Number of Customers by Age Group**.
- **Step 12:** Created and formatted a **Treemap** for account count by account type and assembled the visuals into the final Power BI report.

## Snapshots

### Dashboard – Monthly Balance, Customer Balance & Demographics
<img width="1122" height="633" alt="AI-Powered Banking Transaction Analytics Dashboard 1" src="https://github.com/user-attachments/assets/d9b753d2-2800-428a-9cc7-c4090ebe04cb" />

### Dashboard – Inactive Accounts, Transaction Amount & Transaction Type
<img width="1323" height="606" alt="AI-Powered Banking Transaction Analytics Dashboard 2" src="https://github.com/user-attachments/assets/643c32ad-a2f4-480d-8ca3-b8efb0c25800" />

# Insights

The project uses a SQL-generated dataset of **10,000 transactions** and combines it with customer and account information for Power BI analysis.

### [1] Transactions by Type

The dashboard compares transaction volume between **Credit** and **Debit** transactions. The generated SQL data alternates the transaction type, producing an approximately even split of **5K Credit and 5K Debit transactions (50% each)**.

### [2] Monthly Transaction Amount

The monthly transaction amount visual shows how transaction value changes throughout the year. The displayed dashboard ranges from approximately **0.9M to 4.9M**, with **March showing the highest displayed monthly amount at about 4.9M** and **August the lowest at about 0.9M**.

### [3] Monthly Transaction Balance

The monthly balance visual highlights changes in balance across months. In the displayed report, monthly values are negative, ranging roughly from **-0.95M to -1.74M**, with the lowest displayed point occurring in **July (-1.74M)**.

### [4] Total Balance by Account Type

The dashboard compares aggregate balance between **Savings** and **Current** accounts. The displayed data shows Savings at approximately **1.48K**, while Current contains a substantial negative balance of approximately **-15,782.44K**, showing how an outlier/negative account balance can strongly affect aggregate results.

### [5] Customer / Transaction Value by Name

Customer-level visuals compare balance and transaction amount by customer name. The report makes unusually large positive or negative customer values easy to identify and investigate.

### [6] Inactive Accounts

The **Inactive Accounts by Year and Month** visual tracks accounts that meet the inactivity logic over time. The DAX recommendation defines inactivity using accounts whose latest transaction date is more than **90 days before today**.

### [7] Customer Gender Distribution

A donut chart displays the customer distribution by gender and also exposes blank/missing gender values, demonstrating the effect of incomplete customer data on reporting.

### [8] Customers by Age Group

Customers are grouped into age brackets using Date of Birth. The recommended calculated logic uses the groups **≤25, 26–35, 36–50, and 51+**, making demographic comparison easier.

### [9] Accounts by Account Type

A treemap compares the number of accounts by account type. In the displayed dashboard, **Current and Savings each show 200 records**, reflecting the dataset/model aggregation used in the report.

## Key DAX / Analytical Logic

- **Monthly Transaction Amount:** `CALCULATE(SUM(CombinedBankingDataset[Amount]), ALLEXCEPT(CombinedBankingDataset, CombinedBankingDataset[TransactionDate].[Month]))`
- **Total Balance:** `SUM(CombinedBankingDataset[Balance])`
- **Customer Count by Gender:** `DISTINCTCOUNT(CombinedBankingDataset[CustomerID])`
- **Customer Age:** `DATEDIFF(CombinedBankingDataset[DateOfBirth], TODAY(), YEAR)`
- **Age Group:** `SWITCH(TRUE(), [Customer Age]<=25, "≤25", [Customer Age]<=35, "26-35", [Customer Age]<=50, "36-50", "51+")`
- **Inactive Accounts:** Accounts whose maximum transaction date is earlier than `TODAY()-90`.

## Tools & Technologies

**SQL Server | SQL | Power BI | DAX | Data Cleaning | Data Visualization | Perplexity AI**

## Project Files

- `SQLQuery(1).sql` – Database creation, synthetic data generation, date cleaning, and table joins.
- `AI-Powered Banking Transaction Analytics.pbit` – Power BI project/template.
- KPI reference files – KPI descriptions, recommended visuals, and DAX/calculated-column examples.

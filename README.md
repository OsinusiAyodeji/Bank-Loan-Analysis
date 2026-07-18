# Bank Loan Portfolio Analysis & Strategic Risk Dashboard

## Abstract Summary
This project involved developing a comprehensive Business Intelligence system to transform raw loan data into actionable financial intelligence. Managing a portfolio of **38,576 loans** totaling **$435.76M**, I designed a diagnostic dashboard to identify the drivers of loan defaults and capital recovery. By analyzing borrower behavior, I moved beyond simple volume tracking to provide the lending team with a clear "action plan"—highlighting exactly who to lend to, which high-risk segments to restrict, and why traditional income verification is failing to predict default risk.

![Loan Portfolio Dashboard Overview](Loans%20Image.png)

## Introduction
In the banking sector, high lending volume is often mistaken for success, but without understanding the risk behind those loans, a bank can easily lose more in defaults than it makes in interest. This project was born from the need to move the lending team away from reactive, static reports and toward a proactive, data-driven strategy. 

The goal was to create a "truth-telling" system. By analyzing thousands of individual loan records, I transformed messy transaction data into an interactive tool that allows stakeholders to see the real impact of loan terms, grades, and borrower profiles on the bank’s bottom line.

## Background: Context & Relevance
Most banks sit on mountains of data regarding loan amounts, repayment dates, and borrower demographics, yet they often struggle to turn that information into specific lending policies. Static reporting tracks *what* happened but fails to explain *why* or what to do next. 

This project is highly relevant because it bridges the gap between raw data and strategic decision-making. It provides a blueprint for any financial institution looking to optimize its portfolio, recover capital more efficiently, and minimize the 13.8% default rate currently impacting their lending success.

## Problem Statement
The bank’s current lending strategy relies on reports that only track volume, leaving the team blind to underlying risk factors. This has led to a situation where:
* **Capital is being trapped** in high-risk segments that consistently default.
* **Underwriting policies are outdated**, specifically regarding income verification, which is currently providing a false sense of security.
* **Profitability is being eroded** by poor loan structuring (e.g., long-term loans for high-risk small business ventures). 

Without a clear, data-driven system to prioritize safe borrowers and restrict risky ones, the bank is losing millions in potential revenue and unrecovered capital.

## Objectives
The primary goal of this project was to build a tool that helps management make better, faster lending decisions. My core objectives were:
* **Quantify Performance**: Clearly distinguish between "Good Loans" (fully paid or current) and "Bad Loans" (charged off) to track actual capital recovery.
* **Identify Risk Drivers**: Uncover the combinations of features—such as high Debt-to-Income (DTI) ratios, specific loan purposes, and long term lengths—that lead to defaults.
* **Segment the Portfolio**: Rank borrowers by risk grade and repayment behavior to identify the bank’s "engine" (the safest, most profitable customers).
* **Provide Actionable Insight**: Translate data trends into a clear "Action Plan" that tells the bank exactly which policies to change, whom to lend to more, and whom to restrict.

## Data Description

### Data Source
The dataset used for this evaluation was sourced from **DataVerse Africa**, comprising anonymized loan performance records spanning multiple borrower demographics and financial distributions.

### Data Collection
The data captures standardized loan application entries, payment histories, and credit bureau summaries. It simulates a high-volume transactional system used by credit scoring and underwriting teams to gauge borrower risk and capital returns.

### Data Characteristics
The dataset consists of detailed customer credit records and loan metrics, organized around the following key categories:

* **Borrower Profile**: `annual_income`, `emp_length`, `emp_title`, `home_ownership`, and `verification_status`.
* **Loan Parameters**: `loan_amount`, `term`, `int_rate`, `installment`, `purpose`, `grade`, and `sub_grade`.
* **Timeline Indicators**: `issue_date`, `last_payment_date`, `next_payment_date`, and `last_credit_pull_date`.
* **Performance Indicators**: `loan_status` and `total_payment`.
* **System Identifiers & Context**: `id`, `member_id`, `application_type`, and `address_state`.
* **Credit Behavior Proxies**: `dti` (Debt-to-Income ratio) and `total_acc` (Total Credit Accounts).


## Methodology

To ensure clean, efficient data modeling within Power BI, the processing pipeline prioritized data architecture optimization rather than heavy restructuring:

* **Data Profiling**: Executed comprehensive value distributions and column character checks across all variables to verify data alignment and type consistency.
* **Geographic Structural Splitting**: Extracted the `address_state` parameter into a dedicated **Location Dimension table** to establish a clean, starry relational schema for geographical default heatmaps.
* **Integrity Validation**: Verified that individual loan and member IDs had zero duplicate conflicts to guarantee that portfolio financial metrics were completely accurate.
* **Data Load Optimization**: Reviewed the full schema and explicitly disabled the load for redundant or uninformative columns that did not contribute to solving the target risk and capital tracking goals, significantly boosting dashboard responsiveness.


## Analysis & Custom Logic

To turn raw lending numbers into clear business strategies, I used DAX to build custom loan tracking rules, borrower profile groupings, and calendar logic:

### 1. The Loan Health Classification
Instead of manually sorting through various transaction stages, I created a simple rule to instantly separate successful lending from financial loss:
*   **Good Loans**: Any loan where the status is **Fully Paid** or **Current**. This represents healthy, active capital returning to the bank.
*   **Bad Loans**: Any loan marked as **Charged Off**, meaning the borrower defaulted and the bank has written off the debt as unrecovered capital.

### 2. Strategic Risk Grade Consolidation
To make risk tracking easier for the executive team, I grouped the bank's traditional individual letter grades (A through G) into three broad buckets:
*   **Low Risk (Grades A & B)**: The foundation of the portfolio, acting as the primary engine for safe, predictable returns.
*   **Medium Risk (Grades C & D)**: Moderate performance that requires balanced credit limits.
*   **High Risk (Grades E, F, & G)**: Vulnerable accounts monitored closely to see if their higher interest rates successfully offset their high default rates.

### 3. Borrower Profiling Buckets
*   **DTI (Debt-to-Income) Buckets**: Grouped borrowers based on their monthly debt obligations relative to their income. This allowed me to test whether higher DTI directly translates to higher defaults.
*   **Employment Length Buckets**: Structured raw employment years into clean time bands to evaluate whether borrower career stability impacts their ability to repay.
*   **Dynamic Calendar Engine**: Generated a central Date Table connected to `issue_date` and `last_payment_date`. This allows the bank to filter the dashboard by any month or year to track whether default rates are improving over time.


## Key Insights

By interacting with the visual dashboard and filtering across various dimensions, several deep structural patterns become clear regarding how the bank's capital is performing:

* **The Portfolio Baseline**: Out of **38,576 loans issued** totaling **$435.76M**, the bank has recovered **$473.07M**, yielding a healthy global recovery rate of **108.56%**. However, underneath this healthy surface sits a **13.82% default rate**, meaning $66M in unrecovered capital has been written off as "Bad Loans."
* **The High-Yield Engine**: Low-Risk categories (Grades A & B) represent the true powerhouse of the bank's liquidity. They account for over **$211.0M** in fully paid capital with a default rate of just 8.9% on standard 36-month terms. Conversely, High-Risk grades (E, F, & G) account for the vast majority of written-off debt, losing a combined **$26.6M**.
* **The Core Churn Drivers**: 
    * **Loan Purpose**: Small Business loans carry an incredibly dangerous **25.6% default rate**, making it the highest risk category in the entire portfolio.
    * **Contract Term Length**: 60-month terms default at exactly *double* the rate of 36-month terms (**22% vs. 11%**). 
    * **The Geography Risk Trap**: The interactive state lookup shows massive geographic spikes in defaults. For example, while Florida (FL) shows a steady risk profile, Nebraska (NE) exhibits a catastrophic **60% default rate**.
* **The Income Verification Blindspot**: Counterintuitively, the data reveals that borrowers whose incomes were "Verified" actually default at a *higher* rate (**15.7%**) than those who were "Not Verified" (**12.2%**). This highlights a major gap where traditional checklist verifications are missing actual risk.


## Recommendations

Based on the strategic patterns uncovered by the dashboard data, the bank should implement the following three actionable adjustments immediately:

1. **Aggressively Scale the Grade A/B 36-Month Segment**: Offer lower application processing fees and priority automated underwriting approvals for Grade A and B applicants opting for 36-month terms. This segment represents the lowest default risk and guarantees rapid cash liquidity back to the bank.
2. **Revamp Underwriting Policies for High-Risk Buckets**: Tighten credit requirements for high-risk combinations. Specifically, the bank should cap the maximum allowable loan amount for small business ventures, mandate stricter asset collateral for any 60-month loans, and increase interest premiums on Grades E through G to successfully cover the $26.6M default leak.
3. **De-emphasize Standard Income Verification**: Stop relying on simple income verification as a primary safety net. Underwriting models should be adjusted to place heavy statistical weight on Debt-to-Income (DTI) ratios and historical loan grade performance rather than static document checks.


## Conclusion

This project successfully demonstrates how a financial institution can move past rigid, historical summary spreadsheets to gain true strategic clarity over its credit operations. By implementing automated DAX categorization and custom borrower buckets within Power BI, I transformed a massive portfolio registry into an interactive risk diagnostic system.

Through the integration of dynamic filters and structured visual cross-filtering, the bank no longer has to guess where its leakages are. Management now possesses a distinct asset-allocation blueprint to protect the bank's **$435M+ portfolio capital**, maximize cash liquidity, and systematically drive down default metrics.













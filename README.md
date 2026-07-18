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



















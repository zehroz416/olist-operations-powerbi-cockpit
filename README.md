# Olist E-Commerce Operations & Financial Reconciliation Cockpit

![Power BI](https://img.shields.io/badge/Power_BI-Desktop-yellow?logo=powerbi)
![SQL Server](https://img.shields.io/badge/SQL_Server-SSMS-red?logo=microsoftsqlserver)
![Data Audit](https://img.shields.io/badge/Financial_Reconciliation-$15.84M_Tied_Out-green)

An enterprise-grade, 5-page operational diagnostic and financial reconciliation report built in 100% Native Power BI. Designed to track 99,441 orders across Brazilian logistics hubs, identify SLA breach root causes, and audit payment gateway collection streams down to $0.00 unexplained variance.

---

## 📌 Executive Summary & Key Results

* **Financial Reconciliation Tie-Out:** Audited $15,843,553.24 in billed revenue against $15,846,423.24 in payment collection logs, isolating 287 voucher overages (-$4,041.79) and 125 voucher shortfalls (+$1,171.79) to achieve **$0.00 unexplained variance (-0.018% net variance)**.
* **Carrier SLA Capping Logic:** Identified 18 high-volume carriers (>500 orders) operating below 90% OTIF. Established a volume-capping model projected to recover **2.3 percentage points in composite OTIF**, protecting **~$134K in monthly GMV**.
* **Geographic Bottleneck Isolation:** Discovered 5 Northern region states (RR, AP, AM, AL, PA) averaging 20+ delivery days (2x national benchmark) due to last-mile river/air infrastructure constraints.

---

## 📸 Cockpit Architecture

1. **Executive Overview** — GMV $15.84M Billed / $15.85M Collected, 91.89% OTIF, monthly trends.
2. **OTIF & SLA Performance** — Category SLA breach matrix, payment mix, breach velocity.
3. **Lead-Time Analysis** — Delivery lead-time histogram (0-5 to 31+ day bins), top 10 slowest states, Native Decomposition Tree.
4. **Carrier Performance** — Active carrier count (3,095), scorecards, bottom 10 OTIF ranking chart with 95% SLA target line.
5. **Data Quality & Audit** — Financial reconciliation tie-out bridge to $0.00, SQL validation checks table, and issues log.

---

## 🛠️ Data Model & DAX Highlights

```dax
Unexplained Remainder = 
[Reconciliation Variance] - ([Voucher Overages] + [Voucher Shortfalls])

Worst Carrier OTIF % = 
MINX(
    FILTER(
        VALUES(stg_order_items[seller_id]), 
        CALCULATE(COUNTROWS(stg_order_items)) >= 50
    ), 
    [OTIF Rate %]
)
Author
Zehroz Shahzad
Operations Data Analyst & Financial Reconciliation Specialist
